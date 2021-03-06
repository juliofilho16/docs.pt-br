---
title: Como controlar o preenchimento de uma forma composta
ms.date: 03/30/2017
helpviewer_keywords:
- shapes [WPF], composite [WPF], controlling fill
- composite shapes [WPF], controlling fill
- graphics [WPF], composite shapes
- fill [WPF], controlling
ms.assetid: c1c94575-9eca-48a5-a49a-2ec65259f229
ms.openlocfilehash: a9a17434f11f432f6446e09bd853ed0d2f23fbe8
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-control-the-fill-of-a-composite-shape"></a>Como controlar o preenchimento de uma forma composta
O <xref:System.Windows.Media.GeometryGroup.FillRule%2A> propriedade de um <xref:System.Windows.Media.GeometryGroup> ou <xref:System.Windows.Media.PathGeometry>, especifica uma "regra" que a forma de composição usa para determinar se um determinado ponto é parte da geometria. Há dois valores possíveis para <xref:System.Windows.Media.FillRule>: <xref:System.Windows.Media.FillRule.EvenOdd> e <xref:System.Windows.Media.FillRule.Nonzero>. As seções a seguir descreverão como usar essas duas regras.  
  
 **EvenOdd**: essa regra que determina se um ponto está na região de preenchimento desenhando um raio desse ponto até o infinito em qualquer direção e contando o número de segmentos de caminho dentro da forma especificada que o raio cruza. Se esse número for ímpar, o ponto estará dentro, se for par, o ponto estará fora.  
  
 Por exemplo, o XAML abaixo cria uma forma de composição composta de uma série de anéis (destino) com um <xref:System.Windows.Media.GeometryGroup.FillRule%2A> definido como <xref:System.Windows.Media.FillRule.EvenOdd>.  
  
 [!code-xaml[GeometriesMiscSnippets_snip#FillRuleEvenOddValue](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/FillRuleExample.xaml#fillruleevenoddvalue)]  
  
 A ilustração a seguir mostra a forma criada no exemplo anterior.  
  
 ![Captura de tela: propriedade FillRule de EvenOdd](../../../../docs/framework/wpf/graphics-multimedia/media/fillruleevenoddfirstone.png "FillRuleEvenOddFirstOne")  
  
 Na ilustração acima, observe que o centro e o terceiro anel não estão preenchidos. Isso ocorre porque um raio desenhado de qualquer ponto dentro de qualquer um desses dois anéis passa por um número par de segmentos. Veja a ilustração a seguir:  
  
 ![Diagrama: valor da propriedade FillRule de EvenOdd](../../../../docs/framework/wpf/graphics-multimedia/media/fillruleevenodd2.png "FillRuleEvenOdd2")  
  
 **NonZero:** essa regra determina se um ponto está na região de preenchimento do caminho desenhando um raio desse ponto até o infinito em qualquer direção e então examinando os locais em que um segmento da forma cruza o raio. Começando com uma contagem de zero, adicione um sempre que um segmento cruzar o raio da esquerda para a direita e subtraia um sempre que um segmento de caminho cruzar o raio da direita para a esquerda. Após a contagem de cruzamentos, se o resultado for zero, o ponto estará fora do caminho. Caso contrário, ele estará dentro.  
  
 [!code-xaml[GeometriesMiscSnippets_snip#FillRuleNonZeroValueEllipseGeometry](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/FillRuleExample.xaml#fillrulenonzerovalueellipsegeometry)]  
  
 Usando o exemplo acima, um valor de <xref:System.Windows.Media.FillRule.Nonzero> para <xref:System.Windows.Media.GeometryGroup.FillRule%2A> fornece a ilustração a seguir como resultado:  
  
 ![Captura de tela: valor FillRule de NonZero](../../../../docs/framework/wpf/graphics-multimedia/media/fillrulenonzero1.png "FillRuleNonZero1")  
  
 Como podemos ver, todos os anéis estão preenchidos. Isso acontece porque todos os segmentos estão indo na mesma direção, assim, um raio desenhado de qualquer ponto cruzará um ou mais segmentos e a soma dos cruzamentos não será igual a zero. Por exemplo, na ilustração abaixo, as setas vermelhas representam a direção em que os segmentos são desenhados e a seta branca representa um raio arbitrário que vai de um ponto até o anel mais interno. Iniciando com um valor de zero, para cada segmento que o raio cruza, um valor de um é adicionado, já que o segmento cruza o raio da esquerda para a direita.  
  
 ![Diagrama: valor da propriedade FillRule igual a NonZero](../../../../docs/framework/wpf/graphics-multimedia/media/fillrulenonzero2.png "FillRuleNonZero2")  
  
 Para melhor demonstrar o comportamento de <xref:System.Windows.Media.FillRule.Nonzero> regra uma forma mais complexa com segmentos indo em direções diferentes é necessária. O código XAML abaixo cria uma forma semelhante ao exemplo anterior, exceto que ela é criada com um <xref:System.Windows.Media.PathGeometry> , em seguida, em vez disso, um <xref:System.Windows.Media.EllipseGeometry> , em seguida, em vez disso, que cria quatro arcos concêntricos fechado totalmente concêntricos círculos.  
  
 [!code-xaml[GeometriesMiscSnippets_snip#FillRuleNonZeroValuePathGeometry](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/FillRuleExample.xaml#fillrulenonzerovaluepathgeometry)]  
  
 A ilustração a seguir mostra a forma criada no exemplo anterior.  
  
 ![Captura de tela: valor NonZero da propriedade FillRule](../../../../docs/framework/wpf/graphics-multimedia/media/fillrulenonzero3.png "FillRuleNonZero3")  
  
 Observe que o terceiro arco partindo do centro não está preenchido. A ilustração a seguir mostra por que isso é assim. Na ilustração, as setas vermelhas representam a direção em que os segmentos são desenhados. As duas setas brancas representam dois raios arbitrários que se movem para fora de um ponto na região "não preenchida". Como podemos ver na ilustração, a soma dos valores de um determinado raio que cruza os segmentos no seu caminho é zero. Conforme definido acima, uma soma zero significa que o ponto não faz parte da geometria (não faz parte do preenchimento), enquanto uma soma que *não* é zero, incluindo um valor negativo, faz parte da geometria.  
  
 ![Diagrama: valor NonZero da propriedade FillRule](../../../../docs/framework/wpf/graphics-multimedia/media/fillrulenonzero4.png "FillRuleNonZero4")  
  
 **Observação:** para fins de <xref:System.Windows.Media.FillRule>, todas as formas são consideradas fechadas. Se houver uma lacuna em um segmento, desenhe uma linha imaginária para fechá-la. No exemplo acima, existem pequenas lacunas nos anéis. Devido a isso, seria possível erar que um raio que passasse pela lacuna gerasse um resultado diferente que um raio indo para outra direção. Abaixo está uma ilustração ampliada de uma desses buracos e o "segmento imaginário" (segmento que é desenhado para fins de aplicar o <xref:System.Windows.Media.FillRule>) que o fecha.  
  
 ![Diagrama: para FillRule, segmentos estão sempre fechados](../../../../docs/framework/wpf/graphics-multimedia/media/fillruleclosedshapes.png "FillRuleClosedShapes")  
  
## <a name="example"></a>Exemplo  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma forma composta](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-shape.md)  
 [Visão geral de geometria](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)
