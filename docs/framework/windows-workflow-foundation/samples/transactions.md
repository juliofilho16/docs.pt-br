---
title: Transactions2
ms.date: 03/30/2017
ms.assetid: 51212219-a39e-448e-bff3-10064ff5de64
ms.openlocfilehash: 361022851d971c0b9350899e1fee6a27c557d666
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="transactions"></a>Transações
Esta seção contém exemplos que demonstram as transações de fluxo de trabalho no Windows Workflow Foundation (WF).  
  
## <a name="in-this-section"></a>Nesta seção  
 [TransactionScope básico](../../../../docs/framework/windows-workflow-foundation/samples/basic-transactionscope.md)  
 Consiste em quatro cenários que mostram como aninhar instâncias de <xref:System.Activities.Statements.TransactionScope> .  
  
 [Uso de TransactedReceiveScope](../../../../docs/framework/windows-workflow-foundation/samples/use-of-transactedreceivescope.md)  
 Demonstra como fluir uma transação de um cliente a um servidor usando <xref:System.Activities.Statements.TransactionScope> para criar uma nova transação no cliente e em <xref:System.ServiceModel.Activities.TransactedReceiveScope> para receber uma mensagem com uma transação fluída e definir o escopo o tempo de vida de transação no servidor.  
  
 [Aninhamento de TransactionScope em um serviço](../../../../docs/framework/windows-workflow-foundation/samples/nesting-of-transactionscope-within-a-service.md)  
 Consiste de dois cenários que mostram como manipular instâncias de atividade de <xref:System.Activities.Statements.TransactionScope> em um serviço.
