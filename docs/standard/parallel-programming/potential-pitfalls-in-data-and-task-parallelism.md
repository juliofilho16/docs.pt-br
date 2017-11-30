---
title: Armadilhas em potencial em dados e paralelismo da tarefa
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords: parallel programming, pitfalls
ms.assetid: 1e357177-e699-4b8f-9e49-56d3513ed128
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 54fd201bd4eaef607f8917ea693876aec7fa2923
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="potential-pitfalls-in-data-and-task-parallelism"></a><span data-ttu-id="d49ca-102">Armadilhas em potencial em dados e paralelismo da tarefa</span><span class="sxs-lookup"><span data-stu-id="d49ca-102">Potential Pitfalls in Data and Task Parallelism</span></span>
<span data-ttu-id="d49ca-103">Em muitos casos, <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> e <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> pode oferecer melhorias significativas no desempenho ao longo de loops sequenciais comuns.</span><span class="sxs-lookup"><span data-stu-id="d49ca-103">In many cases, <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> and <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> can provide significant performance improvements over ordinary sequential loops.</span></span> <span data-ttu-id="d49ca-104">No entanto, o trabalho de paralelização do loop apresenta complexidade que pode levar a problemas que, no código sequencial, não são tão comum ou não são encontrados.</span><span class="sxs-lookup"><span data-stu-id="d49ca-104">However, the work of parallelizing the loop introduces complexity that can lead to problems that, in sequential code, are not as common or are not encountered at all.</span></span> <span data-ttu-id="d49ca-105">Este tópico lista algumas práticas recomendadas para evitar quando você escreve loops paralelos.</span><span class="sxs-lookup"><span data-stu-id="d49ca-105">This topic lists some practices to avoid when you write parallel loops.</span></span>  
  
## <a name="do-not-assume-that-parallel-is-always-faster"></a><span data-ttu-id="d49ca-106">Não suponha que paralelo é sempre mais rápido</span><span class="sxs-lookup"><span data-stu-id="d49ca-106">Do Not Assume That Parallel Is Always Faster</span></span>  
 <span data-ttu-id="d49ca-107">Em certos casos um loop paralelo pode ser executado mais lentamente do que seu equivalente sequencial.</span><span class="sxs-lookup"><span data-stu-id="d49ca-107">In certain cases a parallel loop might run slower than its sequential equivalent.</span></span> <span data-ttu-id="d49ca-108">A regra de ouro básica é que loops paralelos que têm alguns iterações e delegados rápida de usuário são improvável de aumento de velocidade muito.</span><span class="sxs-lookup"><span data-stu-id="d49ca-108">The basic rule of thumb is that parallel loops that have few iterations and fast user delegates are unlikely to speedup much.</span></span> <span data-ttu-id="d49ca-109">No entanto, como muitos fatores estão envolvidos no desempenho, recomendamos que você sempre pode medir os resultados reais.</span><span class="sxs-lookup"><span data-stu-id="d49ca-109">However, because many factors are involved in performance, we recommend that you always measure actual results.</span></span>  
  
## <a name="avoid-writing-to-shared-memory-locations"></a><span data-ttu-id="d49ca-110">Evitar gravar em locais de memória compartilhada</span><span class="sxs-lookup"><span data-stu-id="d49ca-110">Avoid Writing to Shared Memory Locations</span></span>  
 <span data-ttu-id="d49ca-111">No código sequencial, não é incomum para ler ou gravar em variáveis estáticas ou campos de classe.</span><span class="sxs-lookup"><span data-stu-id="d49ca-111">In sequential code, it is not uncommon to read from or write to static variables or class fields.</span></span> <span data-ttu-id="d49ca-112">No entanto, sempre que vários threads acessam simultaneamente essas variáveis, há um grande potencial de condições de corrida.</span><span class="sxs-lookup"><span data-stu-id="d49ca-112">However, whenever multiple threads are accessing such variables concurrently, there is a big potential for race conditions.</span></span> <span data-ttu-id="d49ca-113">Embora você possa usar bloqueios para sincronizar o acesso à variável, o custo da sincronização pode prejudicar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="d49ca-113">Even though you can use locks to synchronize access to the variable, the cost of synchronization can hurt performance.</span></span> <span data-ttu-id="d49ca-114">Portanto, é recomendável que você evite, ou pelo menos limita, acesso ao estado em um loop paralelo tanto quanto possível compartilhado.</span><span class="sxs-lookup"><span data-stu-id="d49ca-114">Therefore, we recommend that you avoid, or at least limit, access to shared state in a parallel loop as much as possible.</span></span> <span data-ttu-id="d49ca-115">A melhor maneira de fazer isso é usar as sobrecargas de <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> e <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> que usam um <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> variável para armazenar o estado de local de thread durante a execução do loop.</span><span class="sxs-lookup"><span data-stu-id="d49ca-115">The best way to do this is to use the overloads of <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> and <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> that use a <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> variable to store thread-local state during loop execution.</span></span> <span data-ttu-id="d49ca-116">Para obter mais informações, consulte [Como escrever um loop Parallel.For com variáveis locais de thread](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md) e [Como escrever um loop Parallel.ForEach com variáveis locais de thread](../../../docs/standard/parallel-programming/how-to-write-a-parallel-foreach-loop-with-thread-local-variables.md).</span><span class="sxs-lookup"><span data-stu-id="d49ca-116">For more information, see [How to: Write a Parallel.For Loop with Thread-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md) and [How to: Write a Parallel.ForEach Loop with Thread-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-foreach-loop-with-thread-local-variables.md).</span></span>  
  
## <a name="avoid-over-parallelization"></a><span data-ttu-id="d49ca-117">Evitar excesso de paralelização</span><span class="sxs-lookup"><span data-stu-id="d49ca-117">Avoid Over-Parallelization</span></span>  
 <span data-ttu-id="d49ca-118">Usando loops paralelos, incorre em dos custos indiretos de particionamento a coleção de origem e a sincronização de threads de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d49ca-118">By using parallel loops, you incur the overhead costs of partitioning the source collection and synchronizing the worker threads.</span></span> <span data-ttu-id="d49ca-119">Os benefícios de paralelização ainda estão limitados pelo número de processadores no computador.</span><span class="sxs-lookup"><span data-stu-id="d49ca-119">The benefits of parallelization are further limited by the number of processors on the computer.</span></span> <span data-ttu-id="d49ca-120">Não há nenhum aumento de velocidade a ser obtido executando vários threads vinculada à computação em apenas um processador.</span><span class="sxs-lookup"><span data-stu-id="d49ca-120">There is no speedup to be gained by running multiple compute-bound threads on just one processor.</span></span> <span data-ttu-id="d49ca-121">Portanto, você deve ser cuidado para não sobrescrever paralelizar um loop.</span><span class="sxs-lookup"><span data-stu-id="d49ca-121">Therefore, you must be careful not to over-parallelize a loop.</span></span>  
  
 <span data-ttu-id="d49ca-122">O cenário mais comum no qual paralelização excessiva pode ocorrer é em loops aninhados.</span><span class="sxs-lookup"><span data-stu-id="d49ca-122">The most common scenario in which over-parallelization can occur is in nested loops.</span></span> <span data-ttu-id="d49ca-123">Na maioria dos casos, é melhor paralelizar apenas o loop externo, a menos que uma ou mais das seguintes condições se aplicam:</span><span class="sxs-lookup"><span data-stu-id="d49ca-123">In most cases, it is best to parallelize only the outer loop unless one or more of the following conditions apply:</span></span>  
  
-   <span data-ttu-id="d49ca-124">O loop interno é conhecido por ser muito longos.</span><span class="sxs-lookup"><span data-stu-id="d49ca-124">The inner loop is known to be very long.</span></span>  
  
-   <span data-ttu-id="d49ca-125">Você está executando uma computação cara em cada pedido.</span><span class="sxs-lookup"><span data-stu-id="d49ca-125">You are performing an expensive computation on each order.</span></span> <span data-ttu-id="d49ca-126">(A operação mostrada no exemplo não é cara).</span><span class="sxs-lookup"><span data-stu-id="d49ca-126">(The operation shown in the example is not expensive.)</span></span>  
  
-   <span data-ttu-id="d49ca-127">O sistema de destino é conhecido por ter processadores suficientes para controlar o número de threads que será produzido pela paralelizar a consulta em `cust.Orders`.</span><span class="sxs-lookup"><span data-stu-id="d49ca-127">The target system is known to have enough processors to handle the number of threads that will be produced by parallelizing the query on `cust.Orders`.</span></span>  
  
 <span data-ttu-id="d49ca-128">Em todos os casos, a melhor maneira de determinar a forma de consulta ideal é testar e medidas.</span><span class="sxs-lookup"><span data-stu-id="d49ca-128">In all cases, the best way to determine the optimum query shape is to test and measure.</span></span>  
  
## <a name="avoid-calls-to-non-thread-safe-methods"></a><span data-ttu-id="d49ca-129">Evite chamadas para métodos de Non-Thread-Safe</span><span class="sxs-lookup"><span data-stu-id="d49ca-129">Avoid Calls to Non-Thread-Safe Methods</span></span>  
 <span data-ttu-id="d49ca-130">Gravando para métodos de instância non-thread-safe de um loop paralelo pode levar à corrupção de dados que podem ou não pode ser detectados em seu programa.</span><span class="sxs-lookup"><span data-stu-id="d49ca-130">Writing to non-thread-safe instance methods from a parallel loop can lead to data corruption which may or may not go undetected in your program.</span></span> <span data-ttu-id="d49ca-131">Isso também poderá resultar em exceções.</span><span class="sxs-lookup"><span data-stu-id="d49ca-131">It can also lead to exceptions.</span></span> <span data-ttu-id="d49ca-132">No exemplo a seguir, vários threads é tentar chamar o <xref:System.IO.FileStream.WriteByte%2A?displayProperty=nameWithType> método simultaneamente, que não é compatível com a classe.</span><span class="sxs-lookup"><span data-stu-id="d49ca-132">In the following example, multiple threads would be attempting to call the <xref:System.IO.FileStream.WriteByte%2A?displayProperty=nameWithType> method simultaneously, which is not supported by the class.</span></span>  
  
 [!code-csharp[TPL_Pitfalls#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_pitfalls/cs/pitfalls.cs#04)]
 [!code-vb[TPL_Pitfalls#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_pitfalls/vb/pitfalls_vb.vb#04)]  
  
## <a name="limit-calls-to-thread-safe-methods"></a><span data-ttu-id="d49ca-133">Limite de chamadas para métodos de Thread-Safe</span><span class="sxs-lookup"><span data-stu-id="d49ca-133">Limit Calls to Thread-Safe Methods</span></span>  
 <span data-ttu-id="d49ca-134">Os métodos mais estáticos no .NET Framework são thread-safe e podem ser chamados de vários threads simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="d49ca-134">Most static methods in the .NET Framework are thread-safe and can be called from multiple threads concurrently.</span></span> <span data-ttu-id="d49ca-135">No entanto, até mesmo nesses casos, a sincronização envolvidos pode levar a diminuição significativa na consulta.</span><span class="sxs-lookup"><span data-stu-id="d49ca-135">However, even in these cases, the synchronization involved can lead to significant slowdown in the query.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d49ca-136">Você pode testar isso por conta própria, inserindo algumas chamadas para <xref:System.Console.WriteLine%2A> em suas consultas.</span><span class="sxs-lookup"><span data-stu-id="d49ca-136">You can test for this yourself by inserting some calls to <xref:System.Console.WriteLine%2A> in your queries.</span></span> <span data-ttu-id="d49ca-137">Embora esse método é usado nos exemplos a documentação para fins de demonstração, não usá-lo em loops paralelos, a menos que necessário.</span><span class="sxs-lookup"><span data-stu-id="d49ca-137">Although this method is used in the documentation examples for demonstration purposes, do not use it in parallel loops unless necessary.</span></span>  
  
## <a name="be-aware-of-thread-affinity-issues"></a><span data-ttu-id="d49ca-138">Estar ciente das questões de afinidade de Thread</span><span class="sxs-lookup"><span data-stu-id="d49ca-138">Be Aware of Thread Affinity Issues</span></span>  
 <span data-ttu-id="d49ca-139">Algumas tecnologias, por exemplo, a interoperabilidade COM para componentes de Single-Threaded Apartment (STA), formulários do Windows e Windows Presentation Foundation (WPF), impõem restrições de afinidade de thread que exigem o código para executar em um thread específico.</span><span class="sxs-lookup"><span data-stu-id="d49ca-139">Some technologies, for example, COM interoperability for Single-Threaded Apartment (STA) components, Windows Forms, and Windows Presentation Foundation (WPF), impose thread affinity restrictions that require code to run on a specific thread.</span></span> <span data-ttu-id="d49ca-140">Por exemplo, no Windows Forms e WPF, um controle só pode ser acessado no thread no qual ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="d49ca-140">For example, in both Windows Forms and WPF, a control can only be accessed on the thread on which it was created.</span></span> <span data-ttu-id="d49ca-141">Por exemplo, isso significa que você não pode atualizar um controle de lista de um loop paralelo, a menos que você configurar o Agendador de thread para agendar o trabalho somente no thread da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d49ca-141">This means, for example, that you cannot update a list control from a parallel loop unless you configure the thread scheduler to schedule work only on the UI thread.</span></span> <span data-ttu-id="d49ca-142">Para obter mais informações, consulte [como: agenda de trabalho no Thread da Interface do usuário (UI)](http://msdn.microsoft.com/library/32a846a5-d628-4933-907b-4888ff72c663).</span><span class="sxs-lookup"><span data-stu-id="d49ca-142">For more information, see [How to: Schedule Work on the User Interface (UI) Thread](http://msdn.microsoft.com/library/32a846a5-d628-4933-907b-4888ff72c663).</span></span>  
  
## <a name="use-caution-when-waiting-in-delegates-that-are-called-by-parallelinvoke"></a><span data-ttu-id="d49ca-143">Tenha cuidado quando aguardando delegados que são chamados pelo Parallel. Invoke</span><span class="sxs-lookup"><span data-stu-id="d49ca-143">Use Caution When Waiting in Delegates That Are Called by Parallel.Invoke</span></span>  
 <span data-ttu-id="d49ca-144">Em determinadas circunstâncias, a biblioteca paralela de tarefas será embutido uma tarefa, o que significa que ele é executado na tarefa no thread em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="d49ca-144">In certain circumstances, the Task Parallel Library will inline a task, which means it runs on the task on the currently executing thread.</span></span> <span data-ttu-id="d49ca-145">(Para obter mais informações, consulte [agendadores de tarefa](http://msdn.microsoft.com/library/638f8ea5-21db-47a2-a934-86e1e961bf65).) Essa otimização de desempenho pode resultar em deadlock em determinados casos.</span><span class="sxs-lookup"><span data-stu-id="d49ca-145">(For more information, see [Task Schedulers](http://msdn.microsoft.com/library/638f8ea5-21db-47a2-a934-86e1e961bf65).) This performance optimization can lead to deadlock in certain cases.</span></span> <span data-ttu-id="d49ca-146">Por exemplo, duas tarefas podem executar o mesmo delegado código, que indica quando ocorre um evento, e, em seguida, aguarda a outra tarefa sinalizar.</span><span class="sxs-lookup"><span data-stu-id="d49ca-146">For example, two tasks might run the same delegate code, which signals when an event occurs, and then waits for the other task to signal.</span></span> <span data-ttu-id="d49ca-147">Se a segunda tarefa é embutida no mesmo thread que o primeiro e o primeiro entra em um estado de espera, a segunda tarefa nunca poderá sinalizar o evento.</span><span class="sxs-lookup"><span data-stu-id="d49ca-147">If the second task is inlined on the same thread as the first, and the first goes into a Wait state, the second task will never be able to signal its event.</span></span> <span data-ttu-id="d49ca-148">Para evitar tal uma ocorrência, você pode especificar um tempo limite na operação de espera ou construtores de thread explícita de uso para ajudar a garantir que uma tarefa não podem bloquear a outra.</span><span class="sxs-lookup"><span data-stu-id="d49ca-148">To avoid such an occurrence, you can specify a timeout on the Wait operation, or use explicit thread constructors to help ensure that one task cannot block the other.</span></span>  
  
## <a name="do-not-assume-that-iterations-of-foreach-for-and-forall-always-execute-in-parallel"></a><span data-ttu-id="d49ca-149">Não suponha que iterações de ForEach, para e ForAll sempre executar em paralelo</span><span class="sxs-lookup"><span data-stu-id="d49ca-149">Do Not Assume that Iterations of ForEach, For and ForAll Always Execute in Parallel</span></span>  
 <span data-ttu-id="d49ca-150">É importante ter em mente que iterações individuais em um <xref:System.Threading.Tasks.Parallel.For%2A>, <xref:System.Threading.Tasks.Parallel.ForEach%2A> ou <xref:System.Linq.ParallelEnumerable.ForAll%2A> pode executar um loop, mas não é necessário que executar em paralelo.</span><span class="sxs-lookup"><span data-stu-id="d49ca-150">It is important to keep in mind that individual iterations in a <xref:System.Threading.Tasks.Parallel.For%2A>, <xref:System.Threading.Tasks.Parallel.ForEach%2A> or <xref:System.Linq.ParallelEnumerable.ForAll%2A> loop may but do not have to execute in parallel.</span></span> <span data-ttu-id="d49ca-151">Portanto, você deve evitar gravar qualquer código que depende de correção de execução paralela de iterações ou na execução de iterações em nenhuma ordem específica.</span><span class="sxs-lookup"><span data-stu-id="d49ca-151">Therefore, you should avoid writing any code that depends for correctness on parallel execution of iterations or on the execution of iterations in any particular order.</span></span> <span data-ttu-id="d49ca-152">Por exemplo, esse código é provavelmente um deadlock:</span><span class="sxs-lookup"><span data-stu-id="d49ca-152">For example, this code is likely to deadlock:</span></span>  
  
 [!code-csharp[TPL_Pitfalls#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_pitfalls/cs/pitfalls.cs#01)]
 [!code-vb[TPL_Pitfalls#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_pitfalls/vb/pitfalls_vb.vb#01)]  
  
 <span data-ttu-id="d49ca-153">Neste exemplo, uma iteração define um evento, e todas as outras iterações esperar o evento.</span><span class="sxs-lookup"><span data-stu-id="d49ca-153">In this example, one iteration sets an event, and all other iterations wait on the event.</span></span> <span data-ttu-id="d49ca-154">Nenhuma das iterações espera pode concluir até que a iteração de configuração de evento foi concluída.</span><span class="sxs-lookup"><span data-stu-id="d49ca-154">None of the waiting iterations can complete until the event-setting iteration has completed.</span></span> <span data-ttu-id="d49ca-155">No entanto, é possível que as iterações espera bloqueiam todos os threads que são usados para executar o loop paralelo, antes da iteração de configuração de evento teve a chance de executar.</span><span class="sxs-lookup"><span data-stu-id="d49ca-155">However, it is possible that the waiting iterations block all threads that are used to execute the parallel loop, before the event-setting iteration has had a chance to execute.</span></span> <span data-ttu-id="d49ca-156">Isso resulta em um deadlock – a iteração de configuração de evento nunca será executado e as iterações espera nunca serão ativada.</span><span class="sxs-lookup"><span data-stu-id="d49ca-156">This results in a deadlock – the event-setting iteration will never execute, and the waiting iterations will never wake up.</span></span>  
  
 <span data-ttu-id="d49ca-157">Em particular, uma iteração de um loop paralelo nunca deve aguardar outra iteração do loop para tornar o progresso.</span><span class="sxs-lookup"><span data-stu-id="d49ca-157">In particular, one iteration of a parallel loop should never wait on another iteration of the loop to make progress.</span></span> <span data-ttu-id="d49ca-158">Se o loop paralelo decidir agendar as iterações sequencialmente, mas em ordem oposta, ocorrerá um deadlock.</span><span class="sxs-lookup"><span data-stu-id="d49ca-158">If the parallel loop decides to schedule the iterations sequentially but in the opposite order, a deadlock will occur.</span></span>  
  
## <a name="avoid-executing-parallel-loops-on-the-ui-thread"></a><span data-ttu-id="d49ca-159">Evitar Loops paralelos em execução no Thread da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="d49ca-159">Avoid Executing Parallel Loops on the UI Thread</span></span>  
 <span data-ttu-id="d49ca-160">É importante manter a interface do usuário do aplicativo (UI) responsiva.</span><span class="sxs-lookup"><span data-stu-id="d49ca-160">It is important to keep your application's user interface (UI) responsive.</span></span> <span data-ttu-id="d49ca-161">Se uma operação contém suficiente trabalho para garantir a paralelização, em seguida, ele provavelmente não deve ser executado essa operação no thread da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d49ca-161">If an operation contains enough work to warrant parallelization, then it likely should not be run that operation on the UI thread.</span></span>  <span data-ttu-id="d49ca-162">Em vez disso, ele deve descarregar essa operação para ser executado em um thread em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="d49ca-162">Instead, it should offload that operation to be run on a background thread.</span></span> <span data-ttu-id="d49ca-163">Por exemplo, se você quiser usar um loop paralelo para calcular alguns dados que devem ser renderizados em um controle de interface do usuário, convém executar o loop dentro de uma instância de tarefa, em vez de diretamente em um manipulador de eventos de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d49ca-163">For example, if you want to use a parallel loop to compute some data that should then be rendered into a UI control, you should consider executing the loop within a task instance rather than directly in a UI event handler.</span></span>  <span data-ttu-id="d49ca-164">Somente quando o cálculo Central foi concluída deve você, em seguida, empacotar a atualização de interface do usuário para o thread de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d49ca-164">Only when the core computation has completed should you then marshal the UI update back to the UI thread.</span></span>  
  
 <span data-ttu-id="d49ca-165">Se você executar loops paralelos no thread da interface do usuário, tenha cuidado para evitar a atualização de controles de interface do usuário de dentro do loop.</span><span class="sxs-lookup"><span data-stu-id="d49ca-165">If you do run parallel loops on the UI thread, be careful to avoid updating UI controls from within the loop.</span></span> <span data-ttu-id="d49ca-166">Controles de dentro de um loop paralelo que está em execução no thread da interface do usuário tentando atualizar a interface do usuário podem levar a corrupção de estado, exceções, atualizações atrasadas e até mesmo deadlocks, dependendo de como a atualização de interface do usuário é chamada.</span><span class="sxs-lookup"><span data-stu-id="d49ca-166">Attempting to update UI controls from within a parallel loop that is executing on the UI thread can lead to state corruption, exceptions, delayed updates, and even deadlocks, depending on how the UI update is invoked.</span></span> <span data-ttu-id="d49ca-167">No exemplo a seguir, o loop paralelo bloqueia o thread de interface do usuário no qual ele está em execução até que todas as iterações sejam concluídas.</span><span class="sxs-lookup"><span data-stu-id="d49ca-167">In the following example, the parallel loop blocks the UI thread on which it’s executing until all iterations are complete.</span></span> <span data-ttu-id="d49ca-168">No entanto, se uma iteração do loop está em execução em um thread em segundo plano (como <xref:System.Threading.Tasks.Parallel.For%2A> pode fazer), a chamada a Invoke faz com que uma mensagem a ser enviado para o thread de interface do usuário e a blocos aguardando a mensagem a ser processado.</span><span class="sxs-lookup"><span data-stu-id="d49ca-168">However, if an iteration of the loop is running on a background thread (as <xref:System.Threading.Tasks.Parallel.For%2A> may do), the call to Invoke causes a message to be submitted to the UI thread and blocks waiting for that message to be processed.</span></span> <span data-ttu-id="d49ca-169">Desde que o thread de interface do usuário é bloqueado executando o <xref:System.Threading.Tasks.Parallel.For%2A>, a mensagem nunca pode ser processada e os deadlocks de thread de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d49ca-169">Since the UI thread is blocked running the <xref:System.Threading.Tasks.Parallel.For%2A>, the message can never be processed, and the UI thread deadlocks.</span></span>  
  
 [!code-csharp[TPL_Pitfalls#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_pitfalls/cs/pitfalls.cs#02)]
 [!code-vb[TPL_Pitfalls#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_pitfalls/vb/pitfalls_vb.vb#02)]  
  
 <span data-ttu-id="d49ca-170">O exemplo a seguir mostra como evitar o deadlock, executando o loop dentro de uma instância de tarefa.</span><span class="sxs-lookup"><span data-stu-id="d49ca-170">The following example shows how to avoid the deadlock, by running the loop inside a task instance.</span></span> <span data-ttu-id="d49ca-171">O thread de interface do usuário não é bloqueado pelo loop e a mensagem pode ser processada.</span><span class="sxs-lookup"><span data-stu-id="d49ca-171">The UI thread is not blocked by the loop, and the message can be processed.</span></span>  
  
 [!code-csharp[TPL_Pitfalls#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_pitfalls/cs/pitfalls.cs#03)]
 [!code-vb[TPL_Pitfalls#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_pitfalls/vb/pitfalls_vb.vb#03)]  
  
## <a name="see-also"></a><span data-ttu-id="d49ca-172">Consulte também</span><span class="sxs-lookup"><span data-stu-id="d49ca-172">See Also</span></span>  
 [<span data-ttu-id="d49ca-173">Programação paralela</span><span class="sxs-lookup"><span data-stu-id="d49ca-173">Parallel Programming</span></span>](../../../docs/standard/parallel-programming/index.md)  
 [<span data-ttu-id="d49ca-174">Possíveis armadilhas com PLINQ</span><span class="sxs-lookup"><span data-stu-id="d49ca-174">Potential Pitfalls with PLINQ</span></span>](../../../docs/standard/parallel-programming/potential-pitfalls-with-plinq.md)  
 [<span data-ttu-id="d49ca-175">Padrões de programação paralela: compreender e aplicar paralela padrões com o .NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="d49ca-175">Patterns for Parallel Programming: Understanding and Applying Parallel Patterns with the .NET Framework 4</span></span>](http://go.microsoft.com/fwlink/?LinkID=185142)