---
title: Erro ao acessar arquivo de caminho
ms.date: 07/20/2015
f1_keywords:
- vbrID75
ms.assetid: 6ce3a161-7316-46bd-a785-0d50e5414020
ms.openlocfilehash: 83ce8615b173a6f5835347ebc561a793655ec8f7
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="pathfile-access-error"></a>Erro de acesso ao demarcador/arquivo
Durante uma operação de acesso a arquivos ou o acesso ao disco, o sistema operacional não pôde fazer uma conexão entre o caminho e o nome do arquivo.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1.  Verifique se que a especificação de arquivo está formatada corretamente. Um nome de arquivo pode conter um (absoluto) totalmente qualificado ou relativo ao caminho. Um caminho totalmente qualificado inicia com o nome da unidade (se o caminho está em outra unidade) e lista o caminho específico da raiz para o arquivo. Qualquer caminho que não é totalmente qualificado é relativo a unidade atual e a pasta.  
  
2.  Certifique-se de que você não tentou salvar um arquivo que substitua um arquivo existente de somente leitura. Se esse for o caso, altere o atributo somente leitura do arquivo de destino ou salve o arquivo com um nome de arquivo diferente.  
  
3.  Certifique-se de que não houve tentativa de abrir um arquivo somente leitura em sequencial `Output` ou `Append` modo. Se esse for o caso, abra o arquivo no `Input` modo ou alterar o atributo somente leitura do arquivo.  
  
4.  Certifique-se de que não houve tentativa de alterar um projeto do Visual Basic dentro de um banco de dados ou documento.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de Erro](../../../visual-basic/programming-guide/language-features/error-types.md)
