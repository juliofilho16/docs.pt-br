---
title: Funções de retorno de chamada
ms.date: 03/30/2017
helpviewer_keywords:
- callback function
- platform invoke, calling unmanaged functions
ms.assetid: c0aa8533-3b3b-42e8-9f60-84919793098c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e4494eda29ca6065a157869ec2f93b4875391824
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="callback-functions"></a>Funções de retorno de chamada
Uma função de retorno de chamada é o código em um aplicativo gerenciado que ajuda uma função de DLL não gerenciada a concluir uma tarefa. As chamadas a uma função de retorno de chamada passam indiretamente de um aplicativo gerenciado, por meio de uma função de DLL e novamente para a implementação gerenciada. Algumas das muitas funções de DLL chamadas com a invocação de plataforma exigem que uma função de retorno de chamada no código gerenciado seja executada corretamente.  
  
 Para chamar a maioria das funções de DLL por meio do código gerenciado, crie uma definição gerenciada da função e, em seguida, chame-a. O processo é simples.  
  
 O uso de uma função de DLL que exige uma função de retorno de chamada apresenta algumas etapas adicionais. Primeiro, você deve determinar se a função exige um retorno de chamada examinando a documentação da função. Em seguida, você precisa criar a função de retorno de chamada no aplicativo gerenciado. Por fim, chame a função de DLL, passando um ponteiro para a função de retorno de chamada como um argumento. A ilustração a seguir resume essas etapas.  
  
 ![Retorno de chamada de invocação de plataforma](../../../docs/framework/interop/media/pinvokecallback.gif "pinvokecallback")  
Função de retorno de chamada e implementação  
  
 As funções de retorno de chamada são ideais para uso em situações em que uma tarefa é executada repetidamente. Outro uso comum é com funções de enumeração, como **EnumFontFamilies**, **EnumPrinters** e **EnumWindows** na API do Win32. A função **EnumWindows** enumera por meio de todas as janelas existentes no computador, chamando a função de retorno de chamada para executar uma tarefa em cada janela. Para obter instruções e um exemplo, consulte [Como implementar funções de retorno de chamada](../../../docs/framework/interop/how-to-implement-callback-functions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como implementar funções de retorno de chamada](../../../docs/framework/interop/how-to-implement-callback-functions.md)  
 [Chamando uma função de DLL](../../../docs/framework/interop/calling-a-dll-function.md)
