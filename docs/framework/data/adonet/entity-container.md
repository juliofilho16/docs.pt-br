---
title: contêiner da entidade
ms.date: 03/30/2017
ms.assetid: 16e80405-2c75-42fc-b0e4-b1df53b1c584
ms.openlocfilehash: ed2123629c61b179e07e86effa0c39d9a3222b62
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="entity-container"></a>contêiner da entidade
Um *contêiner de entidade* é um agrupamento lógico de [conjuntos de entidades](../../../../docs/framework/data/adonet/entity-set.md), [AssociationSets](../../../../docs/framework/data/adonet/association-set.md), e [importações de função](../../../../docs/framework/data/adonet/model-declared-function.md).  
  
 O seguinte deve ser verdadeiro de um contêiner de entidade definido em um modelo conceitual:  
  
-   Pelo menos um contêiner de entidade deve ser definido em cada modelo conceitual.  
  
-   O contêiner de entidade deve ter um nome exclusivo dentro de cada modelo conceitual.  
  
 Um contêiner de entidade pode definir os conjuntos de entidades ou conjuntos de associações que usam os tipos de entidade ou as associações definidos em um ou mais namespaces. Para obter mais informações, consulte [modelo de dados de entidade: Namespaces](../../../../docs/framework/data/adonet/entity-data-model-namespaces.md).  
  
## <a name="example"></a>Exemplo  
 O diagrama a seguir mostra um modelo conceitual com três tipos de entidade: `Book`, `Publisher`, e `Author`.  Consulte o próximo exemplo para obter mais informações.  
  
 ![Modelo de exemplo](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 Embora o diagrama não transmite informações do contêiner de entidade, o modelo conceitual deve definir um contêiner de entidade. O [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) usa uma DSL chamada linguagem de definição de esquema conceitual ([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)) para definir modelos conceituais. CSDL seguir define um contêiner de entidade para o modelo conceitual mostrado no diagrama anterior. Observe que o nome de contêiner de entidade é definido em um atributo XML.  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
## <a name="see-also"></a>Consulte também  
 [Principais conceitos do Modelo de Dados de Entidade](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)  
 [Modelo de Dados de Entidade](../../../../docs/framework/data/adonet/entity-data-model.md)
