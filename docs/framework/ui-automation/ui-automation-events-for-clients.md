---
title: Automação de Eventos de Interface de Usuário para Clientes.
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, events for clients
- events, UI Automation clients
ms.assetid: b909e388-3f24-4997-b6d4-bd9c35c2dc27
author: Xansky
ms.author: mhopkins
manager: markl
ms.openlocfilehash: d471ee08f60d6fdd029b2057d629ad824ae9fdcf
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="ui-automation-events-for-clients"></a>Automação de Eventos de Interface de Usuário para Clientes.
> [!NOTE]
>  Esta documentação destina-se a desenvolvedores do .NET Framework que querem usar as classes da [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gerenciadas definidas no namespace <xref:System.Windows.Automation>. Para obter as informações mais recentes sobre a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746) (API de Automação do Windows: Automação da Interface do Usuário).  
  
 Este tópico descreve como [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] eventos são usados por clientes de automação de interface do usuário.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] permite que os clientes assinar eventos de interesse. Esse recurso melhora o desempenho, eliminando a necessidade de continuamente pegar todos os [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] elementos no sistema para ver se qualquer informação, a estrutura ou o estado mudou.  
  
 Eficiência também é aprimorada pela capacidade de monitorar eventos somente dentro de um escopo definido. Por exemplo, um cliente pode escutar eventos de alteração de foco em todos os [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] elementos na árvore ou em apenas um elemento e seus descendentes.  
  
> [!NOTE]
>  Não suponha que todos os possíveis eventos são gerados por um [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] provedor. Por exemplo, nem todas as alterações de propriedade causam eventos a serem gerados pelos provedores de proxy padrão para [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] controles.  
  
 Para uma visão mais ampla de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] eventos, consulte [visão geral sobre eventos de automação de interface do usuário](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
<a name="Subscribing_to_Events"></a>   
## <a name="subscribing-to-events"></a>Assinando eventos  
 Aplicativos cliente assinam eventos de um determinado tipo Registrando um manipulador de eventos, usando um dos métodos a seguir.  
  
|Método|Tipo de evento|Tipo de argumentos de evento|Tipo de representante|  
|------------|----------------|--------------------------|-------------------|  
|<xref:System.Windows.Automation.Automation.AddAutomationFocusChangedEventHandler%2A>|Alteração de foco|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|<xref:System.Windows.Automation.AutomationFocusChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>|Alteração de propriedade|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|<xref:System.Windows.Automation.AutomationPropertyChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddStructureChangedEventHandler%2A>|Alteração da estrutura|<xref:System.Windows.Automation.StructureChangedEventArgs>|<xref:System.Windows.Automation.StructureChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>|Todos os outros eventos, identificados por um <xref:System.Windows.Automation.AutomationEvent>|<xref:System.Windows.Automation.AutomationEventArgs> ou <xref:System.Windows.Automation.WindowClosedEventArgs>|<xref:System.Windows.Automation.AutomationEventHandler>|  
  
 Antes de chamar o método, você deve criar um método delegado para manipular o evento. Se preferir, você pode lidar com diferentes tipos de eventos em um único método e passar este método em várias chamadas para um dos métodos na tabela. Por exemplo, um único <xref:System.Windows.Automation.AutomationEventHandler> pode ser configurado para manipular vários eventos diferentemente acordo com o <xref:System.Windows.Automation.AutomationEventArgs.EventId%2A>.  
  
> [!NOTE]
>  Para processar eventos de fechamento de janela, converter o tipo de argumento que é passado para o manipulador de eventos como <xref:System.Windows.Automation.WindowClosedEventArgs>. Porque o [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] elemento para a janela não é mais válido, você não pode usar o `sender` parâmetro para recuperar informações; use <xref:System.Windows.Automation.WindowClosedEventArgs.GetRuntimeId%2A> em vez disso.  
  
> [!CAUTION]
>  Se seu aplicativo pode receber eventos da própria [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)], não use seu aplicativo [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] thread para assinar eventos de ou para cancelar a assinatura. Isso pode resultar em comportamento imprevisível. Para obter mais informações, consulte [problemas de Threading de automação de interface do usuário](../../../docs/framework/ui-automation/ui-automation-threading-issues.md).  
  
 No fechamento, ou quando [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] eventos não são de interesse para o aplicativo, os clientes de automação de interface do usuário devem chamar um dos métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationEventHandler%2A>|Cancela o registro de um manipulador de eventos que foi registrado usando <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>.|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationFocusChangedEventHandler%2A>|Cancela o registro de um manipulador de eventos que foi registrado usando <xref:System.Windows.Automation.Automation.AddAutomationFocusChangedEventHandler%2A>.|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationPropertyChangedEventHandler%2A>|Cancela o registro de um manipulador de eventos que foi registrado usando <xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>.|  
|<xref:System.Windows.Automation.Automation.RemoveAllEventHandlers%2A>|Cancela o registro de todos os manipuladores de eventos registrados.|  
  
 Por exemplo de código, consulte [assinar eventos de automação de interface do usuário](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md).  
  
## <a name="see-also"></a>Consulte também  
 [Assinar eventos de automação de interface do usuário](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md)  
 [Visão geral sobre eventos de automação de interface do usuário](../../../docs/framework/ui-automation/ui-automation-events-overview.md)  
 [Visão geral de propriedades de automação de interface do usuário](../../../docs/framework/ui-automation/ui-automation-properties-overview.md)  
 [Exemplo de TrackFocus](http://msdn.microsoft.com/library/4a91c0af-6bb5-4d38-a743-cf136f268fc9)
