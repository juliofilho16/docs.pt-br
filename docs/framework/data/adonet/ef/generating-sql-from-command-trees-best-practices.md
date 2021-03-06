---
title: Gerando SQL das árvores de comando - práticas recomendadas
ms.date: 03/30/2017
ms.assetid: 71ef6a24-4c4f-4254-af3a-ffc0d855b0a8
ms.openlocfilehash: 0087c67b12b4b6ea36cabd5800b7be0a72fc4a90
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="generating-sql-from-command-trees---best-practices"></a>Gerando SQL das árvores de comando - práticas recomendadas
O modelo das árvores de comando de consulta de saída a consulta expressável no SQL. No entanto, há determinados desafios comum para criadores de provedor para gerar o SQL de uma árvore de comando de saída. Este tópico discute esses desafios. No próximo tópico, o provedor exemplo mostra como resolver esses desafios.  
  
## <a name="group-dbexpression-nodes-in-a-sql-select-statement"></a>Os nós de DbExpression do grupo em um SELECIONAM a instrução SQL  
 Uma instrução SQL típica tem uma estrutura aninhada da seguinte maneira:  
  
```  
SELECT …  
FROM …  
WHERE …  
GROUP BY …  
ORDER BY …  
```  
  
 Uma ou mais cláusulas podem estar vazios.  Uma instrução SELECT aninhada pode ocorrer em algumas linhas.  
  
 Uma conversão possível de uma árvore de comando de consulta em uma instrução SQL SELECT de um subconsulta para cada operador relacional. No entanto, isso resultaria a subconsultas aninhados desnecessários que poderiam ser difíceis de ler.  Em alguns armazenamentos de dados, a consulta pode executar de maneira distorcida.  
  
 Como exemplo, considere a seguinte árvore de comando de consulta  
  
```  
Project (  
a.x,  
   a = Filter(  
      b.y = 5,   
      b = Scan("TableA")  
   )  
)  
```  
  
 Uma conversão não geraria:  
  
```  
SELECT a.x  
FROM (   SELECT *  
         FROM TableA as b  
         WHERE b.y = 5) as a  
```  
  
 Observe que cada nó da expressão relacional se torna uma nova declaração SELECT SQL.  
  
 Portanto, é importante agregar muitas como nós de expressão como possível em uma única instrução SQL SELECT para preservar a exatidão.  
  
 O resultado de uma agregação para o exemplo anterior apresentado seria:  
  
```  
SELECT b.x   
FROM TableA as b  
WHERE b.y = 5  
```  
  
## <a name="flatten-joins-in-a-sql-select-statement"></a>Aplaine join em uma instrução SQL SELECT  
 Um caso de agregar vários nós em uma única instrução SQL SELECT é agregar várias condições a expressões em uma única instrução SQL SELECT. DbJoinExpression representa um único join entre duas entradas. No entanto, como parte de uma única instrução SQL SELECT, mais de uma join pode ser especificado. Em que os casos join são executados na ordem especificada.  
  
 A espinha esquerda, join (joins que aparece como um filho de outro esquerdo joins) pode ser mais facilmente aplainada em uma única instrução SQL SELECT. Por exemplo, considere a seguinte árvore de comando de consulta:  
  
```  
InnerJoin(  
   a = LeftOuterJoin(  
   b = Extent("TableA")  
   c = Extent("TableB")  
   ON b.y = c.x ),  
   d = Extent("TableC")   
   ON a.b.y = d.z  
)  
```  
  
 Isso pode ser convertido em corretamente:  
  
```  
SELECT *  
FROM TableA as b  
LEFT OUTER JOIN TableB as c ON b.y = c.x  
INNER JOIN TableC as d ON b.y = d.z  
```  
  
 No entanto, a espinha não esquerda join não pode ser facilmente aplainada, e você não deve tentar aplainá-los. Por exemplo, join na árvore de comando de consulta:  
  
```  
InnerJoin(  
   a = Extent("TableA")   
   b = LeftOuterJoin(  
   c = Extent("TableB")  
   d = Extent("TableC")  
   ON c.y = d.x),  
   ON a.z = b.c.y  
)  
```  
  
 É convertido para uma instrução SQL SELECT com subpropriedades uma consulta.  
  
```  
SELECT *  
FROM TableA as a  
INNER JOIN (SELECT *   
   FROM TableB as c   
   LEFT OUTER JOIN TableC as d  
   ON c.y = d.x) as b  
ON b.y = d.z  
```  
  
## <a name="input-alias-redirecting"></a>Entre o redirecionamento alias  
 Para explicar o alias de entrada que redirecionem, considere a estrutura das expressões relacionais, como DbFilterExpression, DbProjectExpression, DbCrossJoinExpression, DbJoinExpression, DbSortExpression, DbGroupByExpression, DbApplyExpression, e DbSkipExpression.  
  
 Cada um desses tipos tem uma ou mais propriedades de entrada que descrevem uma coleção de entrada, e corresponder a variável de associação para cada entrada é usado para representar cada elemento da entrada durante uma passagem de coleção. A variável de associação é usado para se referir ao elemento de entrada, por exemplo na propriedade de predicado de um DbFilterExpression ou propriedade de projeção de um DbProjectExpression.  
  
 Para agregar uma expressão mais relacional nós em um único SELECIONAM a instrução SQL, e avaliar uma expressão que é parte de uma expressão relacional (por exemplo parte da projeção de um DbProjectExpression) a variável de associação que usa não pode ser o mesmo que o alias de entrada, porque várias associações de expressão precisariam ser redirecionada para uma única extensão.  Esse problema é chamado renomear alias.  
  
 Considere o primeiro exemplo deste tópico. Se fazendo a conversão de naïve e traduzir a projeção a.x (DbPropertyExpression (a, x)), está correto para converter em `a.x` porque nós com a entrada como “a” para corresponder a variável de associação.  No entanto, para agregar ambos os nós em um único SELECIONAM a instrução SQL, você precisará converter o mesmo DbPropertyExpression em `b.x`, porque a entrada com com “b”.  
  
## <a name="join-alias-flattening"></a>Adição a ajuste alias  
 Ao contrário de alguma outra expressão relacional em uma árvore de comando de saída, a saída de DbJoinExpression um tipo de resultado que é uma linha que consiste em duas colunas, cada um deless corresponde a uma das entradas. Quando um DbPropertyExpresssion é compilado para acessar uma propriedade escalar que se origina de uma união, está sobre um outro DbPropertyExpresssion.  
  
 Os exemplos incluem “no exemplo a.b.y” 2 “e” no exemplo b.c.y 3. No entanto nas instruções SQL correspondentes esses são referidos como “b.y”. Esta novamente serrilha é chamada join a ajuste alias.  
  
## <a name="column-name-and-extent-alias-renaming"></a>Renomear alias o nome da coluna e de extensão  
 Se uma consulta SQL SELECT que tenha uma união tem que ser concluída com uma projeção, para enumerar todas as colunas de participação de entradas, uma colisão de nome pode ocorrer, desde que mais de uma entrada pode ter o mesmo nome de coluna. Use um nome diferente para que a coluna evite a colisão.  
  
 Além disso, quando ajuste joins, as tabelas de participação (ou os subconsultas) podem ter alias de colisão nesse caso essas precisam ser renomeados.  
  
## <a name="avoid-select-"></a>Evite SELECT *  
 Não use `SELECT *` para selecionar as tabelas de base. O modelo de armazenamento em um [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] aplicativo pode incluir somente um subconjunto das colunas que estão na tabela de banco de dados. Nesse caso, `SELECT *` pode produzir um resultado incorreto. Em vez disso, você deve especificar todas as colunas de participação usando os nomes de coluna tipo do resultado das expressões de participação.  
  
## <a name="reuse-of-expressions"></a>Reutilização de expressões  
 Expressões podem ser reutilizadas na árvore de comando de consulta passado pelo [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]. Não suponha que cada expressão aparece apenas uma vez na árvore de comando de consulta.  
  
## <a name="mapping-primitive-types"></a>Tipos primitivos de mapeamento  
 Quando mapear conceitual (EDM) tipos para tipos de provedor, você deve mapear para o tipo o maior (Int32) para que todos os possíveis valores caber. Além disso, evite o mapeamento para tipos que não pode ser usado para várias operações, como tipos BLOB (por exemplo, `ntext` no SQL Server).  
  
## <a name="see-also"></a>Consulte também  
 [Geração de SQL](../../../../../docs/framework/data/adonet/ef/sql-generation.md)
