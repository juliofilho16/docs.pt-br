---
title: Design de campo
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- fields, design guidelines
- read-only fields
- member design guidelines, fields
ms.assetid: 7cb4b0f3-7a10-4c93-b84d-733f7134fcf8
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2d47934c3fed17f75a97ef5da0397c6ceba53d68
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="field-design"></a>Design de campo
O princípio de encapsulamento é um dos conceitos mais importantes no design orientado a objeto. Esse princípio afirma que os dados armazenados dentro de um objeto devem ser acessíveis somente para esse objeto.  
  
 Uma maneira útil de interpretar o princípio é dizer que um tipo deve ser projetado para que as alterações aos campos do tipo (alterações de nome ou tipo) podem ser feitas sem quebra de código diferente para os membros do tipo. Essa interpretação imediatamente implica que todos os campos devem ser privados.  
  
 Excluímos constantes e estáticos campos somente leitura dessa restrição estrito, porque esses campos, quase por definição, nunca devem alterar.  
  
 **X não** fornecem campos de instância público ou protegido.  
  
 Você deve fornecer as propriedades para acessar os campos em vez de torná-los público ou protegido.  
  
 **FAZER ✓** usar campos de constantes para constantes que nunca serão alterado.  
  
 O compilador Superexpõe os valores dos campos constantes diretamente no código de chamada. Portanto, os valores constantes nunca podem ser alterados sem o risco de perder a compatibilidade.  
  
 **FAZER ✓** usar estático público `readonly` campos para instâncias de objeto predefinido.  
  
 Se houver instâncias predefinidas do tipo, declará-los como somente leitura estáticos campos públicos do próprio tipo.  
  
 **X não** atribuir instâncias dos tipos mutáveis para `readonly` campos.  
  
 Um tipo mutável é um tipo com instâncias que podem ser modificados depois que eles são instanciados. Por exemplo, os fluxos, a maioria das coleções e matrizes são tipos mutáveis, mas <xref:System.Int32?displayProperty=nameWithType>, <xref:System.Uri?displayProperty=nameWithType>, e <xref:System.String?displayProperty=nameWithType> são todos imutável. O modificador de somente leitura em um campo de tipo de referência impede que a instância armazenada no campo seja substituído, mas não impede que dados da instância do campo que está sendo modificado chamando membros alterando a instância.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*  
  
 *Reimpressas pela permissão de Pearson educação, Inc. de [diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicados 22 de outubro de 2008, Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*  
  
## <a name="see-also"></a>Consulte também  
 [Diretrizes de design de membro](../../../docs/standard/design-guidelines/member.md)  
 [Diretrizes de design do Framework](../../../docs/standard/design-guidelines/index.md)
