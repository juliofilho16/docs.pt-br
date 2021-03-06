---
title: Acesso thread-safe em expressões regulares
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET Framework regular expressions, threads
- regular expressions, threads
- searching with regular expressions, threads
- parsing text with regular expressions, threads
- pattern-matching with regular expressions, threads
ms.assetid: 7c4a167b-5236-4cde-a2ca-58646230730f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 79ca0b92cf79ca9be023925f064c1c7c16b3c9ac
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="thread-safety-in-regular-expressions"></a>Acesso thread-safe em expressões regulares
A própria classe <xref:System.Text.RegularExpressions.Regex> é thread-safe e imutável (somente leitura). Ou seja, os objetos de **Regex** podem ser criados em qualquer thread e compartilhados entre os threads. Métodos correspondentes podem ser chamados de qualquer thread e nunca alteram nenhum estado global.  
  
 No entanto, os objetos de resultado (**Match** e **MatchCollection**) retornados pela **Regex** devem ser usados em um único thread. Embora muitos desses objetos sejam logicamente imutáveis, suas implementações poderiam atrasar a computação de alguns resultados para melhorar o desempenho e, como resultado, os chamadores devem serializar o acesso a eles.  
  
 Se houver a necessidade de compartilhar os objetos de resultado da **Regex** em vários threads, esses objetos poderão ser convertidos em instâncias thread-safe chamando seus métodos sincronizados. Com exceção dos enumeradores, todas as classes de expressões regulares são thread-safe ou podem ser convertidas em objetos thread-safe por um método sincronizado.  
  
 Os enumeradores são a única exceção. Um aplicativo precisa serializar as chamadas a enumeradores de coleções. A regra é que se uma coleção pode ser enumerada em mais de um thread simultaneamente, você deve sincronizar os métodos do enumerador no objeto raiz da coleção percorrida pelo enumerador.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões regulares do .NET](../../../docs/standard/base-types/regular-expressions.md)
