---
title: "Visão geral da animação e do sistema de tempo"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- timing system [WPF]
- animation [WPF]
ms.assetid: 172cd5a8-a333-4c81-9456-fafccc19f382
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 484aa47744de95c849b237112f1a383c2c2cb0b7
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="animation-and-timing-system-overview"></a><span data-ttu-id="f9159-102">Visão geral da animação e do sistema de tempo</span><span class="sxs-lookup"><span data-stu-id="f9159-102">Animation and Timing System Overview</span></span>
<span data-ttu-id="f9159-103">Este tópico descreve como o sistema de tempo usa a animação, <xref:System.Windows.Media.Animation.Timeline>, e <xref:System.Windows.Media.Animation.Clock> classes para animar propriedades.</span><span class="sxs-lookup"><span data-stu-id="f9159-103">This topic describes how the timing system uses the animation, <xref:System.Windows.Media.Animation.Timeline>, and <xref:System.Windows.Media.Animation.Clock> classes to animate properties.</span></span>  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a><span data-ttu-id="f9159-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f9159-104">Prerequisites</span></span>  
 <span data-ttu-id="f9159-105">Para entender esse tópico, você deve ser capaz de usar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] animações para animar propriedades, conforme descrito na [Visão geral da animação](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9159-105">To understand this topic, you should be able to use [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] animations to animate properties, as described in the [Animation Overview](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).</span></span> <span data-ttu-id="f9159-106">Ele também ajuda a se familiarizar com as propriedades de dependência; para obter mais informações, consulte o [visão geral das propriedades de dependência](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9159-106">It also helps to be familiar with dependency properties; for more information, see the [Dependency Properties Overview](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).</span></span>  
  
<a name="timelinesandclocks"></a>   
## <a name="timelines-and-clocks"></a><span data-ttu-id="f9159-107">Linhas de tempo e relógios</span><span class="sxs-lookup"><span data-stu-id="f9159-107">Timelines and Clocks</span></span>  
 <span data-ttu-id="f9159-108">O [visão geral de animação](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md) descrito como um <xref:System.Windows.Media.Animation.Timeline> representa um segmento de tempo e uma animação é um tipo de <xref:System.Windows.Media.Animation.Timeline> que produz valores de saída.</span><span class="sxs-lookup"><span data-stu-id="f9159-108">The [Animation Overview](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md) described how a <xref:System.Windows.Media.Animation.Timeline> represents a segment of time, and an animation is a type of <xref:System.Windows.Media.Animation.Timeline> that produces output values.</span></span> <span data-ttu-id="f9159-109">Por si só, um <xref:System.Windows.Media.Animation.Timeline>, não faz nada além de apenas descrever um segmento de tempo.</span><span class="sxs-lookup"><span data-stu-id="f9159-109">By itself, a <xref:System.Windows.Media.Animation.Timeline>, doesn't do anything other than just describe a segment of time.</span></span> <span data-ttu-id="f9159-110">É o cronograma <xref:System.Windows.Media.Animation.Clock> objeto que faz o trabalho real.</span><span class="sxs-lookup"><span data-stu-id="f9159-110">It's the timeline's <xref:System.Windows.Media.Animation.Clock> object that does the real work.</span></span> <span data-ttu-id="f9159-111">Da mesma forma, animação, na verdade, não anima propriedades: uma classe de animação descreve como valores de saída devem ser calculados, mas é o <xref:System.Windows.Media.Animation.Clock> que foi criado para a animação que conduz a saída da animação e a aplica às propriedades.</span><span class="sxs-lookup"><span data-stu-id="f9159-111">Likewise, animation doesn't actually animate properties: an animation class describes how output values should be calculated, but it’s the <xref:System.Windows.Media.Animation.Clock> that was created for the animation that drives the animation output and applies it to properties.</span></span>  
  
 <span data-ttu-id="f9159-112">Um <xref:System.Windows.Media.Animation.Clock> é um tipo especial de objeto que mantém o estado de tempo de execução relacionadas ao tempo para o <xref:System.Windows.Media.Animation.Timeline>.</span><span class="sxs-lookup"><span data-stu-id="f9159-112">A <xref:System.Windows.Media.Animation.Clock> is a special type of object that maintains timing-related run-time state for the <xref:System.Windows.Media.Animation.Timeline>.</span></span> <span data-ttu-id="f9159-113">Ele fornece três pedaços de informações que são essenciais para a animação e o sistema de tempo: <xref:System.Windows.Media.Animation.Clock.CurrentTime%2A>, <xref:System.Windows.Media.Animation.Clock.CurrentProgress%2A>, e <xref:System.Windows.Media.Animation.Clock.CurrentState%2A>.</span><span class="sxs-lookup"><span data-stu-id="f9159-113">It provides three bits of information that are essential to the animation and timing system: <xref:System.Windows.Media.Animation.Clock.CurrentTime%2A>, <xref:System.Windows.Media.Animation.Clock.CurrentProgress%2A>, and <xref:System.Windows.Media.Animation.Clock.CurrentState%2A>.</span></span> <span data-ttu-id="f9159-114">Um <xref:System.Windows.Media.Animation.Clock> determina sua hora atual, o andamento e o estado usando os comportamentos de temporização descritos por seu <xref:System.Windows.Media.Animation.Timeline>: <xref:System.Windows.Media.Animation.Timeline.Duration%2A>, <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f9159-114">A <xref:System.Windows.Media.Animation.Clock> determines its current time, progress, and state by using the timing behaviors described by its <xref:System.Windows.Media.Animation.Timeline>: <xref:System.Windows.Media.Animation.Timeline.Duration%2A>, <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>, and so on.</span></span>  
  
 <span data-ttu-id="f9159-115">Na maioria dos casos, um <xref:System.Windows.Media.Animation.Clock> é criado automaticamente para a linha do tempo.</span><span class="sxs-lookup"><span data-stu-id="f9159-115">In most cases, a <xref:System.Windows.Media.Animation.Clock> is created automatically for your timeline.</span></span> <span data-ttu-id="f9159-116">Quando você anima usando um <xref:System.Windows.Media.Animation.Storyboard> ou <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> método, relógios são automaticamente criados para suas linhas de tempo e animações e aplicados às suas propriedades de destino.</span><span class="sxs-lookup"><span data-stu-id="f9159-116">When you animate by using a <xref:System.Windows.Media.Animation.Storyboard> or the <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> method, clocks are automatically created for your timelines and animations and applied to their targeted properties.</span></span> <span data-ttu-id="f9159-117">Você também pode criar um <xref:System.Windows.Media.Animation.Clock> explicitamente, usando o <xref:System.Windows.Media.Animation.Timeline.CreateClock%2A> método de sua <xref:System.Windows.Media.Animation.Timeline>.</span><span class="sxs-lookup"><span data-stu-id="f9159-117">You can also create a <xref:System.Windows.Media.Animation.Clock> explicitly by using the <xref:System.Windows.Media.Animation.Timeline.CreateClock%2A> method of your <xref:System.Windows.Media.Animation.Timeline>.</span></span> <span data-ttu-id="f9159-118">O <xref:System.Windows.Media.MediaTimeline.CreateClock%2A?displayProperty=nameWithType> método cria um relógio do tipo apropriado para o <xref:System.Windows.Media.Animation.Timeline> no qual ele é chamado.</span><span class="sxs-lookup"><span data-stu-id="f9159-118">The <xref:System.Windows.Media.MediaTimeline.CreateClock%2A?displayProperty=nameWithType> method creates a clock of the appropriate type for the <xref:System.Windows.Media.Animation.Timeline> on which it is called.</span></span> <span data-ttu-id="f9159-119">Se o <xref:System.Windows.Media.Animation.Timeline> contém linhas de tempo filhas, ele cria <xref:System.Windows.Media.Animation.Clock> objetos para que eles também.</span><span class="sxs-lookup"><span data-stu-id="f9159-119">If the <xref:System.Windows.Media.Animation.Timeline> contains child timelines, it creates <xref:System.Windows.Media.Animation.Clock> objects for them as well.</span></span> <span data-ttu-id="f9159-120">Resultante <xref:System.Windows.Media.Animation.Clock> objetos são organizados em árvores que correspondam à estrutura do <xref:System.Windows.Media.Animation.Timeline> árvore de objetos do qual eles são criados.</span><span class="sxs-lookup"><span data-stu-id="f9159-120">The resulting <xref:System.Windows.Media.Animation.Clock> objects are arranged in trees that match the structure of the <xref:System.Windows.Media.Animation.Timeline> objects tree from which they are created.</span></span>  
  
 <span data-ttu-id="f9159-121">Existem diferentes tipos de relógios para tipos diferentes de linhas de tempo.</span><span class="sxs-lookup"><span data-stu-id="f9159-121">There are different types of clocks for different types of timelines.</span></span> <span data-ttu-id="f9159-122">A tabela a seguir mostra o <xref:System.Windows.Media.Animation.Clock> tipos que correspondem a alguns dos diferentes <xref:System.Windows.Media.Animation.Timeline> tipos.</span><span class="sxs-lookup"><span data-stu-id="f9159-122">The following table shows the <xref:System.Windows.Media.Animation.Clock> types that correspond to some of the different <xref:System.Windows.Media.Animation.Timeline> types.</span></span>  
  
|<span data-ttu-id="f9159-123">Tipo de linha do tempo</span><span class="sxs-lookup"><span data-stu-id="f9159-123">Timeline type</span></span>|<span data-ttu-id="f9159-124">Tipo de Relógio</span><span class="sxs-lookup"><span data-stu-id="f9159-124">Clock type</span></span>|<span data-ttu-id="f9159-125">Finalidade do relógio</span><span class="sxs-lookup"><span data-stu-id="f9159-125">Clock purpose</span></span>|  
|-------------------|----------------|-------------------|  
|<span data-ttu-id="f9159-126">Animação (herda de <xref:System.Windows.Media.Animation.AnimationTimeline>)</span><span class="sxs-lookup"><span data-stu-id="f9159-126">Animation (inherits from <xref:System.Windows.Media.Animation.AnimationTimeline>)</span></span>|<xref:System.Windows.Media.Animation.AnimationClock>|<span data-ttu-id="f9159-127">Gera valores de saída para uma propriedade de dependência.</span><span class="sxs-lookup"><span data-stu-id="f9159-127">Generates output values for a dependency property.</span></span>|  
|<xref:System.Windows.Media.MediaTimeline>|<xref:System.Windows.Media.MediaClock>|<span data-ttu-id="f9159-128">Processa um arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="f9159-128">Processes a media file.</span></span>|  
|<xref:System.Windows.Media.Animation.ParallelTimeline>|<xref:System.Windows.Media.Animation.ClockGroup>|<span data-ttu-id="f9159-129">Agrupa e controla seu filho <xref:System.Windows.Media.Animation.Clock> objetos</span><span class="sxs-lookup"><span data-stu-id="f9159-129">Groups and controls its child <xref:System.Windows.Media.Animation.Clock> objects</span></span>|  
|<xref:System.Windows.Media.Animation.Storyboard>|<xref:System.Windows.Media.Animation.ClockGroup>|<span data-ttu-id="f9159-130">Agrupa e controla seu filho <xref:System.Windows.Media.Animation.Clock> objetos</span><span class="sxs-lookup"><span data-stu-id="f9159-130">Groups and controls its child <xref:System.Windows.Media.Animation.Clock> objects</span></span>|  
  
 <span data-ttu-id="f9159-131">Você pode aplicar qualquer <xref:System.Windows.Media.Animation.AnimationClock> objetos que você criar a propriedades de dependência compatíveis usando o <xref:System.Windows.Media.Animation.IAnimatable.ApplyAnimationClock%2A> método.</span><span class="sxs-lookup"><span data-stu-id="f9159-131">You can apply any <xref:System.Windows.Media.Animation.AnimationClock> objects you create to compatible dependency properties by using the <xref:System.Windows.Media.Animation.IAnimatable.ApplyAnimationClock%2A> method.</span></span>  
  
 <span data-ttu-id="f9159-132">Em cenários de alto desempenho, como animação de grande número de objetos semelhantes, gerenciar suas próprias <xref:System.Windows.Media.Animation.Clock> uso pode fornecer benefícios de desempenho.</span><span class="sxs-lookup"><span data-stu-id="f9159-132">In performance-intensive scenarios, such as animating large numbers of similar objects, managing your own <xref:System.Windows.Media.Animation.Clock> use can provide performance benefits.</span></span>  
  
<a name="timemanager"></a>   
## <a name="clocks-and-the-time-manager"></a><span data-ttu-id="f9159-133">Relógios e o Gerenciador de tempo</span><span class="sxs-lookup"><span data-stu-id="f9159-133">Clocks and the Time Manager</span></span>  
 <span data-ttu-id="f9159-134">Quando você anima objetos no [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], é o Gerenciador de tempo que gerencia o <xref:System.Windows.Media.MediaPlayer.Clock%2A> objetos criados para suas linhas de tempo.</span><span class="sxs-lookup"><span data-stu-id="f9159-134">When you animate objects in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], it’s the time manager that manages the <xref:System.Windows.Media.MediaPlayer.Clock%2A> objects created for your timelines.</span></span> <span data-ttu-id="f9159-135">O Gerenciador de tempo é a raiz de uma árvore de <xref:System.Windows.Media.MediaPlayer.Clock%2A> objetos e controla o fluxo de tempo nesta árvore.</span><span class="sxs-lookup"><span data-stu-id="f9159-135">The time manager is the root of a tree of <xref:System.Windows.Media.MediaPlayer.Clock%2A> objects and controls the flow of time in that tree.</span></span>  <span data-ttu-id="f9159-136">Um Gerenciador de tempo é automaticamente criado para cada [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicativo e é invisível para o desenvolvedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9159-136">A time manager is automatically created for each [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] application and is invisible to the application developer.</span></span> <span data-ttu-id="f9159-137">O Gerenciador de tempo "faz tiques" muitas vezes por segundo; o número real de tiques que ocorrem em cada segundo varia dependendo dos recursos disponíveis no sistema.</span><span class="sxs-lookup"><span data-stu-id="f9159-137">The time manager "ticks" many times per second; the actual number of ticks that occur each second varies depending on available system resources.</span></span> <span data-ttu-id="f9159-138">Durante cada um desses tiques, o Gerenciador de tempo calcula o estado de todos os <xref:System.Windows.Media.Animation.ClockState.Active> <xref:System.Windows.Media.Animation.Clock> objetos na árvore de temporização.</span><span class="sxs-lookup"><span data-stu-id="f9159-138">During each one of these ticks, the time manager computes the state of all <xref:System.Windows.Media.Animation.ClockState.Active> <xref:System.Windows.Media.Animation.Clock> objects in the timing tree.</span></span>  
  
 <span data-ttu-id="f9159-139">A ilustração a seguir mostra a relação entre o Gerenciador de tempo e <xref:System.Windows.Media.Animation.AnimationClock>e uma propriedade de dependência animada.</span><span class="sxs-lookup"><span data-stu-id="f9159-139">The following illustration shows the relationship between the time manager, and <xref:System.Windows.Media.Animation.AnimationClock>, and an animated dependency property.</span></span>  
  
 <span data-ttu-id="f9159-140">![Componentes do sistema de tempo](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clocks-1clock1prop.png "graphicsmm_clocks_1clock1prop")</span><span class="sxs-lookup"><span data-stu-id="f9159-140">![Timing system components](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clocks-1clock1prop.png "graphicsmm_clocks_1clock1prop")</span></span>  
<span data-ttu-id="f9159-141">Animar uma propriedade</span><span class="sxs-lookup"><span data-stu-id="f9159-141">Animating a property</span></span>  
  
 <span data-ttu-id="f9159-142">Quando o Gerenciador de tempo faz um tique, ele atualiza o tempo de cada <xref:System.Windows.Media.Animation.ClockState.Active> <xref:System.Windows.Media.Animation.Clock> no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9159-142">When the time manager ticks, it updates the time of every <xref:System.Windows.Media.Animation.ClockState.Active> <xref:System.Windows.Media.Animation.Clock> in the application.</span></span> <span data-ttu-id="f9159-143">Se o <xref:System.Windows.Media.Animation.Clock> é um <xref:System.Windows.Media.Animation.AnimationClock>, ele usa o <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> método do <xref:System.Windows.Media.Animation.AnimationTimeline> da qual ela foi criada calcular o atual valor de saída.</span><span class="sxs-lookup"><span data-stu-id="f9159-143">If the <xref:System.Windows.Media.Animation.Clock> is an <xref:System.Windows.Media.Animation.AnimationClock>, it uses the <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> method of the <xref:System.Windows.Media.Animation.AnimationTimeline> from which it was created to calculate its current output value.</span></span> <span data-ttu-id="f9159-144">O <xref:System.Windows.Media.Animation.AnimationClock> fornece o <xref:System.Windows.Media.Animation.AnimationTimeline> com a hora local atual, um valor de entrada, que é geralmente o valor base da propriedade e um valor padrão de destino.</span><span class="sxs-lookup"><span data-stu-id="f9159-144">The <xref:System.Windows.Media.Animation.AnimationClock> supplies the <xref:System.Windows.Media.Animation.AnimationTimeline> with the current local time, an input value, which is typically the base value of the property, and a default destination value.</span></span> <span data-ttu-id="f9159-145">Quando você recuperar o valor de uma imagem com o uso da propriedade de <xref:System.Windows.DependencyObject.GetValue%2A> método ou seu acessador CLR, você obtém a saída de seu <xref:System.Windows.Media.Animation.AnimationClock>.</span><span class="sxs-lookup"><span data-stu-id="f9159-145">When you retrieve the value of an animated by property using the <xref:System.Windows.DependencyObject.GetValue%2A> method or its CLR accessor, you get the output of its <xref:System.Windows.Media.Animation.AnimationClock>.</span></span>  
  
#### <a name="clock-groups"></a><span data-ttu-id="f9159-146">Grupos de relógio</span><span class="sxs-lookup"><span data-stu-id="f9159-146">Clock Groups</span></span>  
 <span data-ttu-id="f9159-147">A seção anterior descreveu como existem diferentes tipos de <xref:System.Windows.Media.Animation.Clock> objetos para tipos diferentes de linhas de tempo.</span><span class="sxs-lookup"><span data-stu-id="f9159-147">The preceding section described how there are different types of <xref:System.Windows.Media.Animation.Clock> objects for different types of timelines.</span></span> <span data-ttu-id="f9159-148">A ilustração a seguir mostra a relação entre o Gerenciador de tempo, uma <xref:System.Windows.Media.Animation.ClockGroup>, um <xref:System.Windows.Media.Animation.AnimationClock>e uma propriedade de dependência animada.</span><span class="sxs-lookup"><span data-stu-id="f9159-148">The following illustration shows the relationship between the time manager, a <xref:System.Windows.Media.Animation.ClockGroup>, an <xref:System.Windows.Media.Animation.AnimationClock>, and an animated dependency property.</span></span> <span data-ttu-id="f9159-149">Um <xref:System.Windows.Media.Animation.ClockGroup> é criado para linhas de tempo que agrupam outras linhas de tempo, como o <xref:System.Windows.Media.Animation.Storyboard> classe, que agrupa as animações e outras linhas de tempo.</span><span class="sxs-lookup"><span data-stu-id="f9159-149">A <xref:System.Windows.Media.Animation.ClockGroup> is created for timelines that group other timelines, such as the <xref:System.Windows.Media.Animation.Storyboard> class, which groups animations and other timelines.</span></span>  
  
 <span data-ttu-id="f9159-150">![Componentes do sistema de tempo](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clocks-2clock1clockgroup2prop.png "graphicsmm_clocks_2clock1clockgroup2prop")</span><span class="sxs-lookup"><span data-stu-id="f9159-150">![Timing system components](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clocks-2clock1clockgroup2prop.png "graphicsmm_clocks_2clock1clockgroup2prop")</span></span>  
<span data-ttu-id="f9159-151">Um ClockGroup</span><span class="sxs-lookup"><span data-stu-id="f9159-151">A ClockGroup</span></span>  
  
#### <a name="composition"></a><span data-ttu-id="f9159-152">Composição</span><span class="sxs-lookup"><span data-stu-id="f9159-152">Composition</span></span>  
 <span data-ttu-id="f9159-153">É possível associar vários relógios a uma única propriedade, caso em que cada relógio usa o valor de saída do relógio anterior como seu valor de base.</span><span class="sxs-lookup"><span data-stu-id="f9159-153">It's possible to associate multiple clocks with a single property, in which case each clock uses the output value of the preceding clock as its base value.</span></span> <span data-ttu-id="f9159-154">A ilustração a seguir mostra três <xref:System.Windows.Media.Animation.AnimationClock> objetos aplicada à mesma propriedade.</span><span class="sxs-lookup"><span data-stu-id="f9159-154">The following illustration shows three <xref:System.Windows.Media.Animation.AnimationClock> objects applied to the same property.</span></span> <span data-ttu-id="f9159-155">Relógio1 usa o valor base da propriedade animada como sua entrada e usa-o para gerar a saída.</span><span class="sxs-lookup"><span data-stu-id="f9159-155">Clock1 uses the base value of the animated property as its input and uses it to generate output.</span></span> <span data-ttu-id="f9159-156">Relógio2 usa a saída do Relógio1 como sua entrada e usa-o para gerar a saída.</span><span class="sxs-lookup"><span data-stu-id="f9159-156">Clock2 takes the output from Clock1 as its input and uses it to generate output.</span></span> <span data-ttu-id="f9159-157">Relógio3 usa a saída do Relógio2 como sua entrada e usa-o para gerar a saída.</span><span class="sxs-lookup"><span data-stu-id="f9159-157">Clock3 takes the output from Clock2 as its input and uses it to generate output.</span></span> <span data-ttu-id="f9159-158">Quando vários relógios afetam a mesma propriedade simultaneamente, eles devem estar em uma cadeia de composição.</span><span class="sxs-lookup"><span data-stu-id="f9159-158">When multiple clocks affect the same property simultaneously, they are said to be in a composition chain.</span></span>  
  
 <span data-ttu-id="f9159-159">![Componentes do sistema de tempo](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clocks-2clock1prop.png "graphicsmm_clocks_2clock1prop")</span><span class="sxs-lookup"><span data-stu-id="f9159-159">![Timing system components](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clocks-2clock1prop.png "graphicsmm_clocks_2clock1prop")</span></span>  
<span data-ttu-id="f9159-160">Uma cadeia de composição</span><span class="sxs-lookup"><span data-stu-id="f9159-160">A composition chain</span></span>  
  
 <span data-ttu-id="f9159-161">Observe que, embora uma relação é criada entre a entrada e saída de <xref:System.Windows.Media.Animation.AnimationClock> objetos na cadeia de composição, seus comportamentos de tempo não são afetados; <xref:System.Windows.Media.Animation.Clock> objetos (incluindo <xref:System.Windows.Media.Animation.AnimationClock> objetos) têm uma dependência hierárquica de seus pais <xref:System.Windows.Media.Animation.Clock> objetos.</span><span class="sxs-lookup"><span data-stu-id="f9159-161">Note that although a relationship is created among the input and output of the <xref:System.Windows.Media.Animation.AnimationClock> objects in the composition chain, their timing behaviors are not affected; <xref:System.Windows.Media.Animation.Clock> objects (including <xref:System.Windows.Media.Animation.AnimationClock> objects) have a hierarchical dependency on their parent <xref:System.Windows.Media.Animation.Clock> objects.</span></span>  
  
 <span data-ttu-id="f9159-162">Para aplicar vários relógios à mesma propriedade, use o <xref:System.Windows.Media.Animation.HandoffBehavior.Compose> <xref:System.Windows.Media.Animation.HandoffBehavior> ao aplicar uma <xref:System.Windows.Media.Animation.Storyboard>, animação, ou <xref:System.Windows.Media.Animation.AnimationClock>.</span><span class="sxs-lookup"><span data-stu-id="f9159-162">To apply multiple clocks to the same property, use the <xref:System.Windows.Media.Animation.HandoffBehavior.Compose> <xref:System.Windows.Media.Animation.HandoffBehavior> when applying a <xref:System.Windows.Media.Animation.Storyboard>, animation, or <xref:System.Windows.Media.Animation.AnimationClock>.</span></span>  
  
#### <a name="ticks-and-event-consolidation"></a><span data-ttu-id="f9159-163">Tiques e consolidação de eventos</span><span class="sxs-lookup"><span data-stu-id="f9159-163">Ticks and Event Consolidation</span></span>  
 <span data-ttu-id="f9159-164">Além de calcular valores de saída, o Gerenciador de tempo faz outra tarefa toda vez que ele faz um tique: ele determina o estado de cada relógio e gera eventos conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="f9159-164">In addition to calculating output values, the time manager does other work every time it ticks: it determines the state of each clock and raises events as appropriate.</span></span>  
  
 <span data-ttu-id="f9159-165">Enquanto tiques ocorrerem com frequência, é possível que muitas coisas ocorram entre tiques.</span><span class="sxs-lookup"><span data-stu-id="f9159-165">While ticks occur frequently, it's possible for a lot of things to happen between ticks.</span></span> <span data-ttu-id="f9159-166">Por exemplo, um <xref:System.Windows.Media.Animation.Clock> pode ser interrompido, iniciado e interrompido novamente, caso em que seu <xref:System.Windows.Media.Animation.Clock.CurrentState%2A> valor terá sido alterado três vezes.</span><span class="sxs-lookup"><span data-stu-id="f9159-166">For example, a <xref:System.Windows.Media.Animation.Clock> might be stopped, started, and stopped again, in which case its <xref:System.Windows.Media.Animation.Clock.CurrentState%2A> value will have changed three times.</span></span> <span data-ttu-id="f9159-167">Em teoria, o <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> evento pode ser gerado várias vezes em um único tique; no entanto, o mecanismo de temporização consolida eventos, para que o <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> evento pode ser gerado no máximo uma vez por tique.</span><span class="sxs-lookup"><span data-stu-id="f9159-167">In theory, the <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> event could be raised multiple times in a single tick; however, the timing engine consolidates events, so that the <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> event can be raised at most once per tick.</span></span> <span data-ttu-id="f9159-168">Isso é verdadeiro para todos os eventos de temporização: no máximo um evento de cada tipo é gerado para um determinado <xref:System.Windows.Media.Animation.Clock> objeto.</span><span class="sxs-lookup"><span data-stu-id="f9159-168">This is true for all timing events: at most one event of each type is raised for a given <xref:System.Windows.Media.Animation.Clock> object.</span></span>  
  
 <span data-ttu-id="f9159-169">Quando um <xref:System.Windows.Media.Animation.Clock> alterna estados e retorna ao estado original entre tiques (como alterar de <xref:System.Windows.Media.Animation.ClockState.Active> para <xref:System.Windows.Media.Animation.ClockState.Stopped> e voltar para <xref:System.Windows.Media.Animation.ClockState.Active>), o evento associado ainda ocorre.</span><span class="sxs-lookup"><span data-stu-id="f9159-169">When a <xref:System.Windows.Media.Animation.Clock> switches states and returns back to its original state between ticks (such as changing from <xref:System.Windows.Media.Animation.ClockState.Active> to <xref:System.Windows.Media.Animation.ClockState.Stopped> and back to <xref:System.Windows.Media.Animation.ClockState.Active>), the associated event still occurs.</span></span>  
  
 <span data-ttu-id="f9159-170">Para obter mais informações sobre eventos de temporização, consulte a [visão geral dos eventos de tempo](../../../../docs/framework/wpf/graphics-multimedia/timing-events-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9159-170">For more information about timing events, see the [Timing Events Overview](../../../../docs/framework/wpf/graphics-multimedia/timing-events-overview.md).</span></span>  
  
<a name="currentvaluesbasevaluesofproperties"></a>   
## <a name="current-values-and-base-values-of-properties"></a><span data-ttu-id="f9159-171">Valores atuais e valores base de propriedades</span><span class="sxs-lookup"><span data-stu-id="f9159-171">Current Values and Base Values of Properties</span></span>  
 <span data-ttu-id="f9159-172">Uma propriedade animável pode ter dois valores: um valor base e um valor atual.</span><span class="sxs-lookup"><span data-stu-id="f9159-172">An animatable property can have two values: a base value and a current value.</span></span> <span data-ttu-id="f9159-173">Quando você define a propriedade usando seu acessador CLR ou <xref:System.Windows.DependencyObject.SetValue%2A> método, defina o valor de base.</span><span class="sxs-lookup"><span data-stu-id="f9159-173">When you set property using its CLR accessor or the <xref:System.Windows.DependencyObject.SetValue%2A> method, you set its base value.</span></span> <span data-ttu-id="f9159-174">Quando uma propriedade não é animada, seus valores atuais e base são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="f9159-174">When a property is not animated, its base and current values are the same.</span></span>  
  
 <span data-ttu-id="f9159-175">Quando você anima uma propriedade, o <xref:System.Windows.Media.Animation.AnimationClock> define a propriedade *atual* valor.</span><span class="sxs-lookup"><span data-stu-id="f9159-175">When you animate a property, the <xref:System.Windows.Media.Animation.AnimationClock> sets the property's *current* value.</span></span> <span data-ttu-id="f9159-176">Recuperar o valor da propriedade por meio de seu acessador CLR ou <xref:System.Windows.DependencyObject.GetValue%2A> método retorna a saída do <xref:System.Windows.Media.Animation.AnimationClock> quando o <xref:System.Windows.Media.Animation.AnimationClock> é <xref:System.Windows.Media.Animation.ClockState.Active> ou <xref:System.Windows.Media.Animation.ClockState.Filling>.</span><span class="sxs-lookup"><span data-stu-id="f9159-176">Retrieving the property's value through its CLR accessor or the <xref:System.Windows.DependencyObject.GetValue%2A> method returns the output of the <xref:System.Windows.Media.Animation.AnimationClock> when the <xref:System.Windows.Media.Animation.AnimationClock> is <xref:System.Windows.Media.Animation.ClockState.Active> or <xref:System.Windows.Media.Animation.ClockState.Filling>.</span></span> <span data-ttu-id="f9159-177">Você pode recuperar o valor da propriedade base usando o <xref:System.Windows.Media.Animation.IAnimatable.GetAnimationBaseValue%2A> método.</span><span class="sxs-lookup"><span data-stu-id="f9159-177">You can retrieve the property's base value by using the <xref:System.Windows.Media.Animation.IAnimatable.GetAnimationBaseValue%2A> method.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f9159-178">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f9159-178">See Also</span></span>  
 [<span data-ttu-id="f9159-179">Visão geral da animação</span><span class="sxs-lookup"><span data-stu-id="f9159-179">Animation Overview</span></span>](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)  
 [<span data-ttu-id="f9159-180">Visão geral de eventos de tempo</span><span class="sxs-lookup"><span data-stu-id="f9159-180">Timing Events Overview</span></span>](../../../../docs/framework/wpf/graphics-multimedia/timing-events-overview.md)  
 [<span data-ttu-id="f9159-181">Visão geral dos comportamentos de tempo</span><span class="sxs-lookup"><span data-stu-id="f9159-181">Timing Behaviors Overview</span></span>](../../../../docs/framework/wpf/graphics-multimedia/timing-behaviors-overview.md)