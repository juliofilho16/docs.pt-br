---
title: 'Diretrizes de design do componente F #'
description: 'Aprenda as diretrizes para escrever componentes F # destinados ao consumo por outros chamadores.'
ms.date: 05/14/2018
ms.openlocfilehash: 7859baac76be01b2cfbdc8602b6cc417cfe5106f
ms.sourcegitcommit: 89c93d05c2281b4c834f48f6c8df1047e1410980
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2018
---
# <a name="f-component-design-guidelines"></a><span data-ttu-id="16c3e-103">Diretrizes de design do componente F #</span><span class="sxs-lookup"><span data-stu-id="16c3e-103">F# component design guidelines</span></span>

<span data-ttu-id="16c3e-104">Este documento é um conjunto de diretrizes de design do componente para F # de programação, com base no F # componente diretrizes de Design, v14, Microsoft Research, e [outra versão](https://fsharp.org/specs/component-design-guidelines/) curadoria e mantido pela F # Software Foundation originalmente.</span><span class="sxs-lookup"><span data-stu-id="16c3e-104">This document is a set of component design guidelines for F# programming, based on the F# Component Design Guidelines, v14, Microsoft Research, and [another version](https://fsharp.org/specs/component-design-guidelines/) originally curated and maintained by the F# Software Foundation.</span></span>

<span data-ttu-id="16c3e-105">Este documento pressupõe que você esteja familiarizado com a programação F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-105">This document assumes you are familiar with F# programming.</span></span> <span data-ttu-id="16c3e-106">Muito obrigado a comunidade do F # para suas contribuições e comentários úteis em diversas versões deste guia.</span><span class="sxs-lookup"><span data-stu-id="16c3e-106">Many thanks to the F# community for their contributions and helpful feedback on various versions of this guide.</span></span>

## <a name="overview"></a><span data-ttu-id="16c3e-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="16c3e-107">Overview</span></span>

<span data-ttu-id="16c3e-108">Este documento examina alguns dos problemas relacionados ao design de componente do F # e a codificação.</span><span class="sxs-lookup"><span data-stu-id="16c3e-108">This document looks at some of the issues related to F# component design and coding.</span></span> <span data-ttu-id="16c3e-109">Um componente pode significar qualquer um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="16c3e-109">A component can mean any of the following:</span></span>

* <span data-ttu-id="16c3e-110">Uma camada em seu projeto F # com consumidores externos no projeto.</span><span class="sxs-lookup"><span data-stu-id="16c3e-110">A layer in your F# project that has external consumers within that project.</span></span>
* <span data-ttu-id="16c3e-111">Uma biblioteca destinada ao consumo por código F # em limites de assembly.</span><span class="sxs-lookup"><span data-stu-id="16c3e-111">A library intended for consumption by F# code across assembly boundaries.</span></span>
* <span data-ttu-id="16c3e-112">Uma biblioteca destinada ao consumo por qualquer linguagem .NET em limites de assembly.</span><span class="sxs-lookup"><span data-stu-id="16c3e-112">A library intended for consumption by any .NET language across assembly boundaries.</span></span>
* <span data-ttu-id="16c3e-113">Uma biblioteca se destina para distribuição por meio de um repositório de pacotes, tais como [NuGet](https://nuget.org).</span><span class="sxs-lookup"><span data-stu-id="16c3e-113">A library intended for distribution via a package repository, such as [NuGet](https://nuget.org).</span></span>

<span data-ttu-id="16c3e-114">Execute as técnicas descritas neste artigo o [cinco princípios de BOM código F #](index.md#five-principles-of-good-f-code)e, portanto, utilizar funcionais e objetos de programação conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="16c3e-114">Techniques described in this article follow the [Five principles of good F# code](index.md#five-principles-of-good-f-code), and thus utilize both functional and object programming as appropriate.</span></span>

<span data-ttu-id="16c3e-115">Independentemente da metodologia, o designer do componente e a biblioteca enfrentará uma série de práticas e prosaico problemas ao tentar criar uma API que pode ser facilmente usada por desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="16c3e-115">Regardless of the methodology, the component and library designer faces a number of practical and prosaic issues when trying to craft an API that is most easily usable by developers.</span></span> <span data-ttu-id="16c3e-116">Aplicativo consciência do [diretrizes de Design de biblioteca do .NET](../../standard/design-guidelines/index.md) voltar para a criação de um conjunto consistente de APIs que são agradável consumir.</span><span class="sxs-lookup"><span data-stu-id="16c3e-116">Conscientious application of the [.NET Library Design Guidelines](../../standard/design-guidelines/index.md) will steer you towards creating a consistent set of APIs that are pleasant to consume.</span></span>

## <a name="general-guidelines"></a><span data-ttu-id="16c3e-117">Diretrizes gerais</span><span class="sxs-lookup"><span data-stu-id="16c3e-117">General guidelines</span></span>

<span data-ttu-id="16c3e-118">Há algumas diretrizes universais que se aplicam a F # bibliotecas, independentemente do público-alvo para a biblioteca.</span><span class="sxs-lookup"><span data-stu-id="16c3e-118">There are a few universal guidelines that apply to F# libraries, regardless of the intended audience for the library.</span></span>

### <a name="learn-the-net-library-design-guidelines"></a><span data-ttu-id="16c3e-119">Aprenda as diretrizes de Design de biblioteca do .NET</span><span class="sxs-lookup"><span data-stu-id="16c3e-119">Learn the .NET Library Design Guidelines</span></span>

<span data-ttu-id="16c3e-120">Independentemente do tipo de F # estão fazendo de codificação, é importante ter um conhecimento prático do [diretrizes de Design de biblioteca do .NET](../../standard/design-guidelines/index.md).</span><span class="sxs-lookup"><span data-stu-id="16c3e-120">Regardless of the kind of F# coding you are doing, it is valuable to have a working knowledge of the [.NET Library Design Guidelines](../../standard/design-guidelines/index.md).</span></span> <span data-ttu-id="16c3e-121">A maioria das outras F # e programadores do .NET serão estar familiarizado com estas diretrizes e esperar que o código .NET de acordo com a eles.</span><span class="sxs-lookup"><span data-stu-id="16c3e-121">Most other F# and .NET programmers will be familiar with these guidelines, and expect .NET code to conform to them.</span></span>

<span data-ttu-id="16c3e-122">As diretrizes de Design de biblioteca .NET fornecem diretrizes gerais sobre nomenclatura, projetando classes e interfaces, design de membros (propriedades, métodos, eventos, etc.) e muito mais e são úteis primeiro ponto de referência para uma variedade de diretrizes de design.</span><span class="sxs-lookup"><span data-stu-id="16c3e-122">The .NET Library Design Guidelines provide general guidance regarding naming, designing classes and interfaces, member design (properties, methods, events, etc.) and more, and are a useful first point of reference for a variety of design guidance.</span></span>

### <a name="add-xml-documentation-comments-to-your-code"></a><span data-ttu-id="16c3e-123">Adicionar comentários de documentação XML ao seu código</span><span class="sxs-lookup"><span data-stu-id="16c3e-123">Add XML documentation comments to your code</span></span>

<span data-ttu-id="16c3e-124">Documentação XML em APIs públicas Certifique-se de que os usuários podem obter ótimo Intellisense e Inforapida ao usar esses tipos e membros e documentação de construção habilitar arquivos para a biblioteca.</span><span class="sxs-lookup"><span data-stu-id="16c3e-124">XML documentation on public APIs ensure that users can get great Intellisense and Quickinfo when using these types and members, and enable building documentation files for the library.</span></span> <span data-ttu-id="16c3e-125">Consulte o [documentação XML](../language-reference/xml-documentation.md) sobre várias marcas xml que podem ser usadas para marcação adicional em xmldoc comentários.</span><span class="sxs-lookup"><span data-stu-id="16c3e-125">See the [XML Documentation](../language-reference/xml-documentation.md) about various xml tags that can be used for additional markup within xmldoc comments.</span></span>

```fsharp
/// A class for representing (x,y) coordinates
type Point =

    /// Computes the distance between this point and another
    member DistanceTo : otherPoint:Point -> float
```

<span data-ttu-id="16c3e-126">Você pode usar os comentários XML de forma abreviada (`/// comment`), ou os comentários XML padrão (`///<summary>comment</summary>`).</span><span class="sxs-lookup"><span data-stu-id="16c3e-126">You can use either the short form XML comments (`/// comment`), or standard XML comments (`///<summary>comment</summary>`).</span></span>

### <a name="consider-using-explicit-signature-files-fsi-for-stable-library-and-component-apis"></a><span data-ttu-id="16c3e-127">Considere o uso de arquivos de assinatura explícita (. FSI) para a biblioteca estável e APIs de componente</span><span class="sxs-lookup"><span data-stu-id="16c3e-127">Consider using explicit signature files (.fsi) for stable library and component APIs</span></span>

<span data-ttu-id="16c3e-128">Usando arquivos de assinaturas explícita em uma biblioteca F # fornece um resumo sucinto do API pública, que ajuda a garantir que você sabe a superfície pública completa da biblioteca, bem como fornece uma separação clara entre documentação pública e internos detalhes de implementação.</span><span class="sxs-lookup"><span data-stu-id="16c3e-128">Using explicit signatures files in an F# library provides a succinct summary of public API, which both helps to ensure that you know the full public surface of your library, as well as provides a clean separation between public documentation and internal implementation details.</span></span> <span data-ttu-id="16c3e-129">Observe que os arquivos de assinatura adicionar fricção para alterar a API pública, exigindo que as alterações sejam feitas em arquivos de assinatura e implementação.</span><span class="sxs-lookup"><span data-stu-id="16c3e-129">Note that signature files add friction to changing the public API, by requiring changes to be made in both the implementation and signature files.</span></span> <span data-ttu-id="16c3e-130">Como resultado, os arquivos de assinatura devem normalmente ser introduzidos somente quando uma API se tornam consolidou e não deve alterar significativamente.</span><span class="sxs-lookup"><span data-stu-id="16c3e-130">As a result, signature files should typically only be introduced when an API has become solidified and is no longer expected to change significantly.</span></span>

### <a name="always-follow-best-practices-for-using-strings-in-net"></a><span data-ttu-id="16c3e-131">Sempre siga as práticas recomendadas para o uso de cadeias de caracteres no .NET</span><span class="sxs-lookup"><span data-stu-id="16c3e-131">Always follow best practices for using strings in .NET</span></span>

<span data-ttu-id="16c3e-132">Execute [práticas recomendadas para usar cadeias de caracteres no .NET](../../standard/base-types/best-practices-strings.md) orientação.</span><span class="sxs-lookup"><span data-stu-id="16c3e-132">Follow [Best Practices for Using Strings in .NET](../../standard/base-types/best-practices-strings.md) guidance.</span></span> <span data-ttu-id="16c3e-133">Em particular, sempre claramente *intenção cultura* na conversão e comparação de cadeias de caracteres (quando aplicável).</span><span class="sxs-lookup"><span data-stu-id="16c3e-133">In particular, always explicitly state *cultural intent* in the conversion and comparison of strings (where applicable).</span></span>

## <a name="guidelines-for-f-facing-libraries"></a><span data-ttu-id="16c3e-134">Diretrizes para F #-voltada para bibliotecas</span><span class="sxs-lookup"><span data-stu-id="16c3e-134">Guidelines for F#-facing libraries</span></span>

<span data-ttu-id="16c3e-135">Esta seção apresenta recomendações para o desenvolvimento de F # pública-voltada para bibliotecas; ou seja, as bibliotecas expor APIs públicas que são destinados a serem consumidos por desenvolvedores de F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-135">This section presents recommendations for developing public F#-facing libraries; that is, libraries exposing public APIs that are intended to be consumed by F# developers.</span></span> <span data-ttu-id="16c3e-136">Há uma variedade de recomendações de design de biblioteca aplicável especificamente para F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-136">There are a variety of library-design recommendations applicable specifically to F#.</span></span> <span data-ttu-id="16c3e-137">Na ausência das recomendações específicas que execute, as diretrizes de Design de biblioteca do .NET estão as diretrizes de fallback.</span><span class="sxs-lookup"><span data-stu-id="16c3e-137">In the absence of the specific recommendations that follow, the .NET Library Design Guidelines are the fallback guidance.</span></span>

### <a name="naming-conventions"></a><span data-ttu-id="16c3e-138">Convenções de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="16c3e-138">Naming conventions</span></span>

#### <a name="use-net-naming-and-capitalization-conventions"></a><span data-ttu-id="16c3e-139">Use convenções de nomenclatura e capitalização do .NET</span><span class="sxs-lookup"><span data-stu-id="16c3e-139">Use .NET naming and capitalization conventions</span></span>

<span data-ttu-id="16c3e-140">A tabela a seguir segue convenções de nomenclatura e capitalização do .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-140">The following table follows .NET naming and capitalization conventions.</span></span> <span data-ttu-id="16c3e-141">Há pequenas adições para incluir também as construções de linguagem F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-141">There are small additions to also include F# constructs.</span></span>

| <span data-ttu-id="16c3e-142">Constructo</span><span class="sxs-lookup"><span data-stu-id="16c3e-142">Construct</span></span> | <span data-ttu-id="16c3e-143">Caso</span><span class="sxs-lookup"><span data-stu-id="16c3e-143">Case</span></span> | <span data-ttu-id="16c3e-144">Parte</span><span class="sxs-lookup"><span data-stu-id="16c3e-144">Part</span></span> | <span data-ttu-id="16c3e-145">Exemplos</span><span class="sxs-lookup"><span data-stu-id="16c3e-145">Examples</span></span> | <span data-ttu-id="16c3e-146">Observações</span><span class="sxs-lookup"><span data-stu-id="16c3e-146">Notes</span></span> |
|-----------|------|------|----------|-------|
| <span data-ttu-id="16c3e-147">Tipos concretos</span><span class="sxs-lookup"><span data-stu-id="16c3e-147">Concrete types</span></span> | <span data-ttu-id="16c3e-148">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-148">PascalCase</span></span> | <span data-ttu-id="16c3e-149">Substantivo / adjetivo</span><span class="sxs-lookup"><span data-stu-id="16c3e-149">Noun/ adjective</span></span> | <span data-ttu-id="16c3e-150">Lista, duplo, complexo</span><span class="sxs-lookup"><span data-stu-id="16c3e-150">List, Double, Complex</span></span> | <span data-ttu-id="16c3e-151">Tipos concretos são estruturas, classes, enumerações, delegados, registros e uniões.</span><span class="sxs-lookup"><span data-stu-id="16c3e-151">Concrete types are structs, classes, enumerations, delegates, records, and unions.</span></span> <span data-ttu-id="16c3e-152">Embora os nomes de tipo são tradicionalmente minúsculos em OCaml, F # adotou o esquema de nomenclatura do .NET para tipos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-152">Though type names are traditionally lowercase in OCaml, F# has adopted the .NET naming scheme for types.</span></span>
| <span data-ttu-id="16c3e-153">DLLs</span><span class="sxs-lookup"><span data-stu-id="16c3e-153">DLLs</span></span>           | <span data-ttu-id="16c3e-154">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-154">PascalCase</span></span> |                 | <span data-ttu-id="16c3e-155">Fabrikam.Core.dll</span><span class="sxs-lookup"><span data-stu-id="16c3e-155">Fabrikam.Core.dll</span></span> |  |
| <span data-ttu-id="16c3e-156">Marcas de união</span><span class="sxs-lookup"><span data-stu-id="16c3e-156">Union tags</span></span>     | <span data-ttu-id="16c3e-157">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-157">PascalCase</span></span> | <span data-ttu-id="16c3e-158">substantivo</span><span class="sxs-lookup"><span data-stu-id="16c3e-158">Noun</span></span> | <span data-ttu-id="16c3e-159">Alguns, adicionar, sucesso</span><span class="sxs-lookup"><span data-stu-id="16c3e-159">Some, Add, Success</span></span> | <span data-ttu-id="16c3e-160">Não use um prefixo em APIs públicas.</span><span class="sxs-lookup"><span data-stu-id="16c3e-160">Do not use a prefix in public APIs.</span></span> <span data-ttu-id="16c3e-161">Opcionalmente, use um prefixo ao interna, como ' ' Digite equipes = TAlpha</span><span class="sxs-lookup"><span data-stu-id="16c3e-161">Optionally use a prefix when internal, such as \`\`\`type Teams = TAlpha</span></span> | <span data-ttu-id="16c3e-162">TBeta</span><span class="sxs-lookup"><span data-stu-id="16c3e-162">TBeta</span></span> | <span data-ttu-id="16c3e-163">TDelta. ' '</span><span class="sxs-lookup"><span data-stu-id="16c3e-163">TDelta.\`\`\`</span></span> |
| <span data-ttu-id="16c3e-164">evento</span><span class="sxs-lookup"><span data-stu-id="16c3e-164">Event</span></span>          | <span data-ttu-id="16c3e-165">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-165">PascalCase</span></span> | <span data-ttu-id="16c3e-166">Verbo</span><span class="sxs-lookup"><span data-stu-id="16c3e-166">Verb</span></span> | <span data-ttu-id="16c3e-167">ValueChanged / ValueChanging</span><span class="sxs-lookup"><span data-stu-id="16c3e-167">ValueChanged / ValueChanging</span></span> |  |
| <span data-ttu-id="16c3e-168">Exceções</span><span class="sxs-lookup"><span data-stu-id="16c3e-168">Exceptions</span></span>     | <span data-ttu-id="16c3e-169">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-169">PascalCase</span></span> |      | <span data-ttu-id="16c3e-170">WebException</span><span class="sxs-lookup"><span data-stu-id="16c3e-170">WebException</span></span> | <span data-ttu-id="16c3e-171">Nome deve terminar com "Exception".</span><span class="sxs-lookup"><span data-stu-id="16c3e-171">Name should end with “Exception”.</span></span> |
| <span data-ttu-id="16c3e-172">Campo</span><span class="sxs-lookup"><span data-stu-id="16c3e-172">Field</span></span>          | <span data-ttu-id="16c3e-173">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-173">PascalCase</span></span> | <span data-ttu-id="16c3e-174">substantivo</span><span class="sxs-lookup"><span data-stu-id="16c3e-174">Noun</span></span> | <span data-ttu-id="16c3e-175">CurrentName</span><span class="sxs-lookup"><span data-stu-id="16c3e-175">CurrentName</span></span>  | |
| <span data-ttu-id="16c3e-176">Tipos de interface</span><span class="sxs-lookup"><span data-stu-id="16c3e-176">Interface types</span></span> |  <span data-ttu-id="16c3e-177">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-177">PascalCase</span></span> | <span data-ttu-id="16c3e-178">Substantivo / adjetivo</span><span class="sxs-lookup"><span data-stu-id="16c3e-178">Noun/ adjective</span></span> | <span data-ttu-id="16c3e-179">IDisposable</span><span class="sxs-lookup"><span data-stu-id="16c3e-179">IDisposable</span></span> | <span data-ttu-id="16c3e-180">Nome deve começar com "I".</span><span class="sxs-lookup"><span data-stu-id="16c3e-180">Name should start with “I”.</span></span> |
| <span data-ttu-id="16c3e-181">Método</span><span class="sxs-lookup"><span data-stu-id="16c3e-181">Method</span></span> |  <span data-ttu-id="16c3e-182">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-182">PascalCase</span></span> |  <span data-ttu-id="16c3e-183">Verbo</span><span class="sxs-lookup"><span data-stu-id="16c3e-183">Verb</span></span> | <span data-ttu-id="16c3e-184">ToString</span><span class="sxs-lookup"><span data-stu-id="16c3e-184">ToString</span></span> | |
| <span data-ttu-id="16c3e-185">Namespace</span><span class="sxs-lookup"><span data-stu-id="16c3e-185">Namespace</span></span> | <span data-ttu-id="16c3e-186">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-186">PascalCase</span></span> | | <span data-ttu-id="16c3e-187">FSharp</span><span class="sxs-lookup"><span data-stu-id="16c3e-187">Microsoft.FSharp.Core</span></span> | <span data-ttu-id="16c3e-188">Geralmente usa `<Organization>.<Technology>[.<Subnamespace>]`, embora drop da organização se a tecnologia é independente da organização.</span><span class="sxs-lookup"><span data-stu-id="16c3e-188">Generally use `<Organization>.<Technology>[.<Subnamespace>]`, though drop the organization if the technology is independent of organization.</span></span> |
| <span data-ttu-id="16c3e-189">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="16c3e-189">Parameters</span></span> | <span data-ttu-id="16c3e-190">camelCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-190">camelCase</span></span> | <span data-ttu-id="16c3e-191">substantivo</span><span class="sxs-lookup"><span data-stu-id="16c3e-191">Noun</span></span> |  <span data-ttu-id="16c3e-192">typeName, transform, intervalo</span><span class="sxs-lookup"><span data-stu-id="16c3e-192">typeName, transform, range</span></span> | |
| <span data-ttu-id="16c3e-193">permitir que os valores (internos)</span><span class="sxs-lookup"><span data-stu-id="16c3e-193">let values (internal)</span></span> | <span data-ttu-id="16c3e-194">camelCase ou PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-194">camelCase or PascalCase</span></span> | <span data-ttu-id="16c3e-195">Substantivo / verbo</span><span class="sxs-lookup"><span data-stu-id="16c3e-195">Noun/ verb</span></span> |  <span data-ttu-id="16c3e-196">getValue, myTable</span><span class="sxs-lookup"><span data-stu-id="16c3e-196">getValue, myTable</span></span> |
| <span data-ttu-id="16c3e-197">permitir que os valores (externo)</span><span class="sxs-lookup"><span data-stu-id="16c3e-197">let values (external)</span></span> | <span data-ttu-id="16c3e-198">camelCase ou PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-198">camelCase or PascalCase</span></span> | <span data-ttu-id="16c3e-199">Substantivo/verbo</span><span class="sxs-lookup"><span data-stu-id="16c3e-199">Noun/verb</span></span>  | <span data-ttu-id="16c3e-200">List.map, Dates.Today</span><span class="sxs-lookup"><span data-stu-id="16c3e-200">List.map, Dates.Today</span></span> | <span data-ttu-id="16c3e-201">os valores associados a Let geralmente são públicos ao seguir os padrões de design funcional tradicional.</span><span class="sxs-lookup"><span data-stu-id="16c3e-201">let-bound values are often public when following traditional functional design patterns.</span></span> <span data-ttu-id="16c3e-202">No entanto, geralmente usa PascalCase quando o identificador pode ser usado em outras linguagens .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-202">However, generally use PascalCase when the identifier can be used from other .NET languages.</span></span> |
| <span data-ttu-id="16c3e-203">Propriedade</span><span class="sxs-lookup"><span data-stu-id="16c3e-203">Property</span></span>  | <span data-ttu-id="16c3e-204">PascalCase</span><span class="sxs-lookup"><span data-stu-id="16c3e-204">PascalCase</span></span>  | <span data-ttu-id="16c3e-205">Substantivo / adjetivo</span><span class="sxs-lookup"><span data-stu-id="16c3e-205">Noun/ adjective</span></span>  | <span data-ttu-id="16c3e-206">IsEndOfFile, BackColor</span><span class="sxs-lookup"><span data-stu-id="16c3e-206">IsEndOfFile, BackColor</span></span>  | <span data-ttu-id="16c3e-207">Propriedades Boolianas geralmente uso é e pode e deve ser afirmativa, como IsEndOfFile, não IsNotEndOfFile.</span><span class="sxs-lookup"><span data-stu-id="16c3e-207">Boolean properties generally use Is and Can and should be affirmative, as in IsEndOfFile, not IsNotEndOfFile.</span></span>

#### <a name="avoid-abbreviations"></a><span data-ttu-id="16c3e-208">Evite abreviações</span><span class="sxs-lookup"><span data-stu-id="16c3e-208">Avoid abbreviations</span></span>

<span data-ttu-id="16c3e-209">As diretrizes do .NET evitar o uso de abreviações (por exemplo, "usar `OnButtonClick` em vez de `OnBtnClick`").</span><span class="sxs-lookup"><span data-stu-id="16c3e-209">The .NET guidelines discourage the use of abbreviations (for example, “use `OnButtonClick` rather than `OnBtnClick`”).</span></span> <span data-ttu-id="16c3e-210">Abreviações comuns, como `Async` para "Assíncrona" tolerado.</span><span class="sxs-lookup"><span data-stu-id="16c3e-210">Common abbreviations, such as `Async` for “Asynchronous”, are tolerated.</span></span> <span data-ttu-id="16c3e-211">Esta diretriz às vezes é ignorada para programação funcional; Por exemplo, `List.iter` usa uma abreviação para "Repetir".</span><span class="sxs-lookup"><span data-stu-id="16c3e-211">This guideline is sometimes ignored for functional programming; for example, `List.iter` uses an abbreviation for “iterate”.</span></span> <span data-ttu-id="16c3e-212">Por esse motivo, usar abreviações tende a ser tolerada para um nível mais alto em F #-para-programação F #, mas ainda geralmente devem ser evitadas no design do componente público.</span><span class="sxs-lookup"><span data-stu-id="16c3e-212">For this reason, using abbreviations tends to be tolerated to a greater degree in F#-to-F# programming, but should still generally be avoided in public component design.</span></span>

#### <a name="avoid-casing-name-collisions"></a><span data-ttu-id="16c3e-213">Evitar conflitos de nome de maiusculas e minúsculas</span><span class="sxs-lookup"><span data-stu-id="16c3e-213">Avoid casing name collisions</span></span>

<span data-ttu-id="16c3e-214">As diretrizes do .NET que se maiusculas e minúsculas sozinho não podem ser usado para resolver a ambiguidade conflitos de nome, pois alguns idiomas de cliente (por exemplo, o Visual Basic) diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="16c3e-214">The .NET guidelines say that casing alone cannot be used to disambiguate name collisions, since some client languages (for example, Visual Basic) are case-insensitive.</span></span>

#### <a name="use-acronyms-where-appropriate"></a><span data-ttu-id="16c3e-215">Use acrônimos quando apropriado</span><span class="sxs-lookup"><span data-stu-id="16c3e-215">Use acronyms where appropriate</span></span>

<span data-ttu-id="16c3e-216">Acrônimos como XML não são abreviações e são amplamente usados em bibliotecas do .NET no formulário uncapitalized (Xml).</span><span class="sxs-lookup"><span data-stu-id="16c3e-216">Acronyms such as XML are not abbreviations and are widely used in .NET libraries in uncapitalized form (Xml).</span></span> <span data-ttu-id="16c3e-217">Somente acrônimos bem conhecidos e amplamente reconhecidos devem ser usados.</span><span class="sxs-lookup"><span data-stu-id="16c3e-217">Only well-known, widely recognized acronyms should be used.</span></span>

#### <a name="use-pascalcase-for-generic-parameter-names"></a><span data-ttu-id="16c3e-218">Use PascalCase para nomes de parâmetro genérico</span><span class="sxs-lookup"><span data-stu-id="16c3e-218">Use PascalCase for generic parameter names</span></span>

<span data-ttu-id="16c3e-219">Use PascalCase para nomes de parâmetro genérico em APIs públicas, inclusive para F #-voltada para bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="16c3e-219">Do use PascalCase for generic parameter names in public APIs, including for F#-facing libraries.</span></span> <span data-ttu-id="16c3e-220">Em particular, usar nomes como `T`, `U`, `T1`, `T2` para parâmetros genéricos arbitrários, e quando nomes específicos fazem sentido, em seguida, para F #-bibliotecas voltado para usam nomes como `Key`, `Value`, `Arg`(mas não por exemplo, `TKey`).</span><span class="sxs-lookup"><span data-stu-id="16c3e-220">In particular, use names like `T`, `U`, `T1`, `T2` for arbitrary generic parameters, and when specific names make sense, then for F#-facing libraries use names like `Key`, `Value`, `Arg` (but not for example, `TKey`).</span></span>

#### <a name="use-either-pascalcase-or-camelcase-for-public-functions-and-values-in-f-modules"></a><span data-ttu-id="16c3e-221">Use PascalCase ou camelCase para valores em F # módulos e funções públicas</span><span class="sxs-lookup"><span data-stu-id="16c3e-221">Use either PascalCase or camelCase for public functions and values in F# modules</span></span>

<span data-ttu-id="16c3e-222">camelCase é usado para funções públicas que são projetadas para serem usados não qualificado (por exemplo, `invalidArg`) e para as "funções de coleção padrão" (por exemplo, List.map).</span><span class="sxs-lookup"><span data-stu-id="16c3e-222">camelCase is used for public functions that are designed to be used unqualified (for example, `invalidArg`), and for the “standard collection functions” (for example, List.map).</span></span> <span data-ttu-id="16c3e-223">Ambos nesses casos, os nomes de função muito atuam como palavras-chave no idioma.</span><span class="sxs-lookup"><span data-stu-id="16c3e-223">In both these cases, the function names act much like keywords in the language.</span></span>

### <a name="object-type-and-module-design"></a><span data-ttu-id="16c3e-224">Design de objeto, o tipo e o módulo</span><span class="sxs-lookup"><span data-stu-id="16c3e-224">Object, Type, and Module design</span></span>

#### <a name="use-namespaces-or-modules-to-contain-your-types-and-modules"></a><span data-ttu-id="16c3e-225">Use módulos ou namespaces para conter seus tipos e módulos</span><span class="sxs-lookup"><span data-stu-id="16c3e-225">Use namespaces or modules to contain your types and modules</span></span>

<span data-ttu-id="16c3e-226">Cada arquivo de F # em um componente deve começar com uma declaração de namespace ou uma declaração de módulo.</span><span class="sxs-lookup"><span data-stu-id="16c3e-226">Each F# file in a component should begin with either a namespace declaration or a module declaration.</span></span>

```fsharp
namespace Fabrikam.BasicOperationsAndTypes

type ObjectType1() =
    ...

type ObjectType2() =
     ...

module CommonOperations =
    ...
```

<span data-ttu-id="16c3e-227">ou</span><span class="sxs-lookup"><span data-stu-id="16c3e-227">or</span></span>

```fsharp
module Fabrikam.BasicOperationsAndTypes

type ObjectType1() =
    ...

type ObjectType2() =
    ...

module CommonOperations =
    ...
```

<span data-ttu-id="16c3e-228">As diferenças entre usar módulos e namespaces para organizar o código no nível superior são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="16c3e-228">The differences between using modules and namespaces to organize code at the top level are as follows:</span></span>

* <span data-ttu-id="16c3e-229">Namespaces pode abranger vários arquivos</span><span class="sxs-lookup"><span data-stu-id="16c3e-229">Namespaces can span multiple files</span></span>
* <span data-ttu-id="16c3e-230">Namespaces não podem conter funções F #, a menos que eles estão dentro de um módulo interno</span><span class="sxs-lookup"><span data-stu-id="16c3e-230">Namespaces cannot contain F# functions unless they are within an inner module</span></span>
* <span data-ttu-id="16c3e-231">O código de qualquer módulo especificado deve estar contido em um único arquivo</span><span class="sxs-lookup"><span data-stu-id="16c3e-231">The code for any given module must be contained within a single file</span></span>
* <span data-ttu-id="16c3e-232">Módulos de nível superior podem conter funções de F # sem a necessidade de um módulo interno</span><span class="sxs-lookup"><span data-stu-id="16c3e-232">Top-level modules can contain F# functions without the need for an inner module</span></span>

<span data-ttu-id="16c3e-233">A escolha entre um namespace de nível superior ou o módulo afeta a forma compilada do código e, portanto, afetam o modo de exibição de outras linguagens .NET deve sua API, eventualmente, ser consumida fora do código F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-233">The choice between a top-level namespace or module affects the compiled form of the code, and thus will affect the view from other .NET languages should your API eventually be consumed outside of F# code.</span></span>

#### <a name="use-methods-and-properties-for-operations-intrinsic-to-object-types"></a><span data-ttu-id="16c3e-234">Use os métodos e propriedades para operações intrínsecas para tipos de objeto</span><span class="sxs-lookup"><span data-stu-id="16c3e-234">Use methods and properties for operations intrinsic to object types</span></span>

<span data-ttu-id="16c3e-235">Ao trabalhar com objetos, é melhor certificar-se de que a funcionalidade consumível é implementada como métodos e propriedades no tipo.</span><span class="sxs-lookup"><span data-stu-id="16c3e-235">When working with objects, it is best to ensure that consumable functionality is implemented as methods and properties on that type.</span></span>

```fsharp
type HardwareDevice() =

    member this.ID = ...

    member this.SupportedProtocols = ...

type HashTable<'Key,'Value>(comparer: IEqualityComparer<'Key>) =

    member this.Add(key, value) = ...

    member this.ContainsKey(key) = ...

    member this.ContainsValue(value) = ...
```

<span data-ttu-id="16c3e-236">A maior parte da funcionalidade para um determinado membro não precisa necessariamente implementada em que o membro, mas o consumo essa funcionalidade deve estar.</span><span class="sxs-lookup"><span data-stu-id="16c3e-236">The bulk of functionality for a given member need not necessarily be implemented in that member, but the consumable piece of that functionality should be.</span></span>

#### <a name="use-classes-to-encapsulate-mutable-state"></a><span data-ttu-id="16c3e-237">Usar classes para encapsular estado mutável</span><span class="sxs-lookup"><span data-stu-id="16c3e-237">Use classes to encapsulate mutable state</span></span>

<span data-ttu-id="16c3e-238">Em F #, isso só precisa ser feito onde que estado já não é encapsulado por outra construção de linguagem, como um fechamento, expressão de sequência ou computação assíncrona.</span><span class="sxs-lookup"><span data-stu-id="16c3e-238">In F#, this only needs to be done where that state is not already encapsulated by another language construct, such as a closure, sequence expression, or asynchronous computation.</span></span>

```fsharp
type Counter() =
    // let-bound values are private in classes.
    let mutable count = 0

    member this.Next() =
        count <- count + 1
        count
```

#### <a name="use-interfaces-to-group-related-operations"></a><span data-ttu-id="16c3e-239">Usar interfaces para agrupar operações relacionadas</span><span class="sxs-lookup"><span data-stu-id="16c3e-239">Use interfaces to group related operations</span></span>

<span data-ttu-id="16c3e-240">Use tipos de interface para representar um conjunto de operações.</span><span class="sxs-lookup"><span data-stu-id="16c3e-240">Use interface types to represent a set of operations.</span></span> <span data-ttu-id="16c3e-241">Isso é preferível para outras opções, como registros de funções ou tuplas de funções.</span><span class="sxs-lookup"><span data-stu-id="16c3e-241">This is preferred to other options, such as tuples of functions or records of functions.</span></span>

```fsharp
type Serializer =
    abstract Serialize<'T> : preserveRefEq: bool -> value: 'T -> string
    abstract Deserialize<'T> : preserveRefEq: bool -> pickle: string -> 'T
```

<span data-ttu-id="16c3e-242">Preferencialmente a:</span><span class="sxs-lookup"><span data-stu-id="16c3e-242">In preference to:</span></span>

```fsharp
type Serializer<'T> = {
    Serialize : bool -> 'T -> string
    Deserialize : bool -> string -> 'T
}
```

<span data-ttu-id="16c3e-243">Interfaces são conceitos de primeira classe do .NET, que você pode usar para obter o que Functors normalmente seria.</span><span class="sxs-lookup"><span data-stu-id="16c3e-243">Interfaces are first-class concepts in .NET, which you can use to achieve what Functors would normally give you.</span></span> <span data-ttu-id="16c3e-244">Além disso, eles podem ser usados para codificar tipos existential em seu programa, que não é possível de registros de funções.</span><span class="sxs-lookup"><span data-stu-id="16c3e-244">Additionally, they can be used to encode existential types into your program, which records of functions cannot.</span></span>

#### <a name="use-a-module-to-group-functions-which-act-on-collections"></a><span data-ttu-id="16c3e-245">Usar um módulo para funções do grupo que atuam em coleções</span><span class="sxs-lookup"><span data-stu-id="16c3e-245">Use a module to group functions which act on collections</span></span>

<span data-ttu-id="16c3e-246">Quando você define um tipo de coleção, considere fornecer um conjunto padrão de operações, como `CollectionType.map` e `CollectionType.iter`) para novos tipos de coleção.</span><span class="sxs-lookup"><span data-stu-id="16c3e-246">When you define a collection type, consider providing a standard set of operations like `CollectionType.map` and `CollectionType.iter`) for new collection types.</span></span>

```fsharp
module CollectionType =
    let map f c =
        ...
    let iter f c =
        ...
```

<span data-ttu-id="16c3e-247">Se você incluir esse um módulo, siga as convenções de nomenclatura padrão para funções encontradas em FSharp. Core.</span><span class="sxs-lookup"><span data-stu-id="16c3e-247">If you include such a module, follow the standard naming conventions for functions found in FSharp.Core.</span></span>

#### <a name="use-a-module-to-group-functions-for-common-canonical-functions-especially-in-math-and-dsl-libraries"></a><span data-ttu-id="16c3e-248">Usar um módulo para funções de grupo para as funções comuns, canônicas, especialmente em matemática e bibliotecas DSL</span><span class="sxs-lookup"><span data-stu-id="16c3e-248">Use a module to group functions for common, canonical functions, especially in math and DSL libraries</span></span>

<span data-ttu-id="16c3e-249">Por exemplo, `Microsoft.FSharp.Core.Operators` é uma coleção automaticamente aberta de funções de nível superior (como `abs` e `sin`) fornecidas pelo FSharp.Core.dll.</span><span class="sxs-lookup"><span data-stu-id="16c3e-249">For example, `Microsoft.FSharp.Core.Operators` is an automatically opened collection of top-level functions (like `abs` and `sin`) provided by FSharp.Core.dll.</span></span>

<span data-ttu-id="16c3e-250">Da mesma forma, uma biblioteca de estatísticas pode incluir um módulo com funções `erf` e `erfc`, em que esse módulo é projetado para ser explicitamente ou automaticamente aberto.</span><span class="sxs-lookup"><span data-stu-id="16c3e-250">Likewise, a statistics library might include a module with functions `erf` and `erfc`, where this module is designed to be explicitly or automatically opened.</span></span>

#### <a name="consider-using-requirequalifiedaccess-and-carefully-apply-autoopen-attributes"></a><span data-ttu-id="16c3e-251">Considere o uso de RequireQualifiedAccess e aplicar cuidadosamente AutoOpen atributos</span><span class="sxs-lookup"><span data-stu-id="16c3e-251">Consider using RequireQualifiedAccess and carefully apply AutoOpen attributes</span></span>

<span data-ttu-id="16c3e-252">Adicionando o `[<RequireQualifiedAccess>]` atributo para um módulo indica que o módulo não pode ser aberto e que as referências aos elementos do módulo exigem explícita qualificado acesso.</span><span class="sxs-lookup"><span data-stu-id="16c3e-252">Adding the `[<RequireQualifiedAccess>]` attribute to a module indicates that the module may not be opened and that references to the elements of the module require explicit qualified access.</span></span> <span data-ttu-id="16c3e-253">Por exemplo, o `Microsoft.FSharp.Collections.List` módulo tem esse atributo.</span><span class="sxs-lookup"><span data-stu-id="16c3e-253">For example, the `Microsoft.FSharp.Collections.List` module has this attribute.</span></span>

<span data-ttu-id="16c3e-254">Isso é útil quando funções e os valores no módulo têm nomes que possam entrar em conflito com nomes em outros módulos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-254">This is useful when functions and values in the module have names that are likely to conflict with names in other modules.</span></span> <span data-ttu-id="16c3e-255">Exigir acesso qualificado pode aumentar significativamente a facilidade de manutenção de longo prazo e evolvability de uma biblioteca.</span><span class="sxs-lookup"><span data-stu-id="16c3e-255">Requiring qualified access can greatly increase the long-term maintainability and evolvability of a library.</span></span>

<span data-ttu-id="16c3e-256">Adicionando o `[<AutoOpen>]` atributo para um módulo significa que o módulo seja aberto quando o namespace que contém é aberto.</span><span class="sxs-lookup"><span data-stu-id="16c3e-256">Adding the `[<AutoOpen>]` attribute to a module means the module will be opened when the containing namespace is opened.</span></span> <span data-ttu-id="16c3e-257">O `[<AutoOpen>]` atributo também pode ser aplicado a um assembly para indicar um módulo que é aberto automaticamente quando o assembly é referenciado.</span><span class="sxs-lookup"><span data-stu-id="16c3e-257">The `[<AutoOpen>]` attribute may also be applied to an assembly to indicate a module that is automatically opened when the assembly is referenced.</span></span>

<span data-ttu-id="16c3e-258">Por exemplo, uma biblioteca de estatísticas **MathsHeaven.Statistics** pode conter um `module MathsHeaven.Statistics.Operators` que contêm funções `erf` e `erfc`.</span><span class="sxs-lookup"><span data-stu-id="16c3e-258">For example, a statistics library **MathsHeaven.Statistics** might contain a `module MathsHeaven.Statistics.Operators` containing functions `erf` and `erfc`.</span></span> <span data-ttu-id="16c3e-259">É aconselhável marcar este módulo como `[<AutoOpen>]`.</span><span class="sxs-lookup"><span data-stu-id="16c3e-259">It is reasonable to mark this module as `[<AutoOpen>]`.</span></span> <span data-ttu-id="16c3e-260">Isso significa `open MathsHeaven.Statistics` também abrir este módulo e colocar os nomes `erf` e `erfc` no escopo.</span><span class="sxs-lookup"><span data-stu-id="16c3e-260">This means `open MathsHeaven.Statistics` will also open this module and bring the names `erf` and `erfc` into scope.</span></span> <span data-ttu-id="16c3e-261">Usa outro bom `[<AutoOpen>]` para módulos que contêm métodos de extensão.</span><span class="sxs-lookup"><span data-stu-id="16c3e-261">Another good use of `[<AutoOpen>]` is for modules containing extension methods.</span></span>

<span data-ttu-id="16c3e-262">Uso excessivo de `[<AutoOpen>]` leva a namespaces poluído e o atributo deve ser usada com cuidado.</span><span class="sxs-lookup"><span data-stu-id="16c3e-262">Overuse of `[<AutoOpen>]` leads to polluted namespaces, and the attribute should be used with care.</span></span> <span data-ttu-id="16c3e-263">Para bibliotecas específicas em domínios específicos, uso criterioso de `[<AutoOpen>]` pode levar à melhor utilização.</span><span class="sxs-lookup"><span data-stu-id="16c3e-263">For specific libraries in specific domains, judicious use of `[<AutoOpen>]` can lead to better usability.</span></span>

#### <a name="consider-defining-operator-members-on-classes-where-using-well-known-operators-is-appropriate"></a><span data-ttu-id="16c3e-264">Considere definir membros de operador em classes em que é apropriado usar operadores conhecidos</span><span class="sxs-lookup"><span data-stu-id="16c3e-264">Consider defining operator members on classes where using well-known operators is appropriate</span></span>

<span data-ttu-id="16c3e-265">Às vezes, as classes são usadas para construções de matemáticas como vetores de modelo.</span><span class="sxs-lookup"><span data-stu-id="16c3e-265">Sometimes classes are used to model mathematical constructs such as Vectors.</span></span> <span data-ttu-id="16c3e-266">Quando o domínio que está sendo modelado tem operadores conhecidos, defini-los como membros intrínsecos para a classe é útil.</span><span class="sxs-lookup"><span data-stu-id="16c3e-266">When the domain being modeled has well-known operators, defining them as members intrinsic to the class is helpful.</span></span>

```fsharp
type Vector(x:float) =

    member v.X = x

    static member (*) (vector:Vector, scalar:float) = Vector(vector.X * scalar)

    static member (+) (vector1:Vector, vector2:Vector) = Vector(vector1.X + vector2.X)

let v = Vector(5.0)

let u = v * 10.0
```

<span data-ttu-id="16c3e-267">Este guia corresponde a diretrizes gerais do .NET para esses tipos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-267">This guidance corresponds to general .NET guidance for these types.</span></span> <span data-ttu-id="16c3e-268">No entanto, ele pode ser importante adicionalmente em F # de codificação, pois isso permite que esses tipos a serem usados em conjunto com as funções de F # e métodos com restrições de membro, como sumby.</span><span class="sxs-lookup"><span data-stu-id="16c3e-268">However, it can be additionally important in F# coding as this allows these types to be used in conjunction with F# functions and methods with member constraints, such as List.sumBy.</span></span>

#### <a name="consider-using-compiledname-to-provide-a-net-friendly-name-for-other-net-language-consumers"></a><span data-ttu-id="16c3e-269">Considere o uso de CompiledName para fornecer uma. Nome amigável do NET para outros consumidores de linguagem do .NET</span><span class="sxs-lookup"><span data-stu-id="16c3e-269">Consider using CompiledName to provide a .NET-friendly name for other .NET language consumers</span></span>

<span data-ttu-id="16c3e-270">Às vezes, talvez você queira atribuir um nome em um estilo para consumidores de F # (como um membro estático em letras minúsculas para que ele apareça como se fosse uma função associada de módulo), mas tem um estilo diferente para o nome quando ele é compilado em um assembly.</span><span class="sxs-lookup"><span data-stu-id="16c3e-270">Sometimes you may wish to name something in one style for F# consumers (such as a static member in lower case so that it appears as if it were a module-bound function), but have a different style for the name when it is compiled into an assembly.</span></span> <span data-ttu-id="16c3e-271">Você pode usar o `[<CompiledName>]` atributo para fornecer um estilo diferente para F # não consumindo o assembly de código.</span><span class="sxs-lookup"><span data-stu-id="16c3e-271">You can use the `[<CompiledName>]` attribute to provide a different style for non F# code consuming the assembly.</span></span>

```fsharp
type Vector(x:float, y:float) =

    member v.X = x
    member v.Y = y

    [<CompiledName("Create")>]
    static member create x y = Vector (x, y)

let v = Vector.create 5.0 3.0
```

<span data-ttu-id="16c3e-272">Usando `[<CompiledName>]`, você pode usar as convenções de nomenclatura do .NET para F # não consumidores do assembly.</span><span class="sxs-lookup"><span data-stu-id="16c3e-272">By using `[<CompiledName>]`, you can use .NET naming conventions for non F# consumers of the assembly.</span></span>

#### <a name="use-method-overloading-for-member-functions-if-doing-so-provides-a-simpler-api"></a><span data-ttu-id="16c3e-273">Use a sobrecarga de método para funções de membro, se isso proporciona uma API simples</span><span class="sxs-lookup"><span data-stu-id="16c3e-273">Use method overloading for member functions, if doing so provides a simpler API</span></span>

<span data-ttu-id="16c3e-274">Sobrecarga de método é uma ferramenta poderosa para simplificar uma API que pode precisar executar uma funcionalidade semelhante, mas com diferentes opções ou argumentos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-274">Method overloading is a powerful tool for simplifying an API that may need to perform similar functionality, but with different options or arguments.</span></span>

```fsharp
type Logger() =

    member this.Log(message) =
        ...
    member this.Log(message, retryPolicy) =
        ...
```

<span data-ttu-id="16c3e-275">Em F #, é mais comum de sobrecarga no número de argumentos, em vez dos tipos de argumentos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-275">In F#, it is more common to overload on number of arguments rather than types of arguments.</span></span>

#### <a name="hide-the-representations-of-record-and-union-types-if-the-design-of-these-types-is-likely-to-evolve"></a><span data-ttu-id="16c3e-276">Ocultar as representações de registro e tipos de união, se o design desses tipos é mais provável de envolver</span><span class="sxs-lookup"><span data-stu-id="16c3e-276">Hide the representations of record and union types if the design of these types is likely to evolve</span></span>

<span data-ttu-id="16c3e-277">Evite revelar concretas representações de objetos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-277">Avoid revealing concrete representations of objects.</span></span> <span data-ttu-id="16c3e-278">Por exemplo, a representação concreta de <xref:System.DateTime> valores não é revelado pela API externa, público do design da biblioteca do .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-278">For example, the concrete representation of <xref:System.DateTime> values is not revealed by the external, public API of the .NET library design.</span></span> <span data-ttu-id="16c3e-279">Em tempo de execução, o Common Language Runtime sabe a implementação de confirmado que será utilizada durante a execução.</span><span class="sxs-lookup"><span data-stu-id="16c3e-279">At run time, the Common Language Runtime knows the committed implementation that will be used throughout execution.</span></span> <span data-ttu-id="16c3e-280">No entanto, código compilado não próprio acompanhar dependências na representação concreta.</span><span class="sxs-lookup"><span data-stu-id="16c3e-280">However, compiled code doesn't itself pick up dependencies on the concrete representation.</span></span>

#### <a name="avoid-the-use-of-implementation-inheritance-for-extensibility"></a><span data-ttu-id="16c3e-281">Evite o uso de herança de implementação para extensibilidade</span><span class="sxs-lookup"><span data-stu-id="16c3e-281">Avoid the use of implementation inheritance for extensibility</span></span>

<span data-ttu-id="16c3e-282">Herança de implementação raramente é usada em F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-282">In F#, implementation inheritance is rarely used.</span></span> <span data-ttu-id="16c3e-283">Além disso, hierarquias de herança são geralmente complexos e difíceis de alterar quando chegarem novos requisitos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-283">Furthermore, inheritance hierarchies are often complex and difficult to change when new requirements arrive.</span></span> <span data-ttu-id="16c3e-284">Implementação de herança ainda existe em F # para compatibilidade e raros casos em que é a melhor solução para um problema, mas técnicas alternativas a ser procuradas em seus programas F # ao criar para polimorfismo, como a implementação de interface.</span><span class="sxs-lookup"><span data-stu-id="16c3e-284">Inheritance implementation still exists in F# for compatibility and rare cases where it is the best solution to a problem, but alternative techniques should be sought in your F# programs when designing for polymorphism, such as interface implementation.</span></span>

### <a name="function-and-member-signatures"></a><span data-ttu-id="16c3e-285">Assinaturas de função e membro</span><span class="sxs-lookup"><span data-stu-id="16c3e-285">Function and member signatures</span></span>

#### <a name="use-tuples-for-return-values-when-returning-a-small-number-of-multiple-unrelated-values"></a><span data-ttu-id="16c3e-286">Use tuplas para valores de retorno ao retornar um número pequeno de vários valores relacionados</span><span class="sxs-lookup"><span data-stu-id="16c3e-286">Use tuples for return values when returning a small number of multiple unrelated values</span></span>

<span data-ttu-id="16c3e-287">Aqui está um bom exemplo do uso de uma coleção de itens em um tipo de retorno:</span><span class="sxs-lookup"><span data-stu-id="16c3e-287">Here is a good example of using a tuple in a return type:</span></span>

```fsharp
val divrem : BigInteger -> BigInteger -> BigInteger * BigInteger
```

<span data-ttu-id="16c3e-288">Para retornar tipos que contém vários componentes, ou onde os componentes estiverem relacionados a uma única entidade de identificação, considere o uso de um tipo nomeado em vez de uma tupla.</span><span class="sxs-lookup"><span data-stu-id="16c3e-288">For return types containing many components, or where the components are related to a single identifiable entity, consider using a named type instead of a tuple.</span></span>

#### <a name="use-asynct-for-async-programming-at-f-api-boundaries"></a><span data-ttu-id="16c3e-289">Use `Async<T>` para programação assíncrona em limites de API do F #</span><span class="sxs-lookup"><span data-stu-id="16c3e-289">Use `Async<T>` for async programming at F# API boundaries</span></span>

<span data-ttu-id="16c3e-290">Se houver uma operação síncrona correspondente chamada `Operation` que retorna um `T`, em seguida, a operação assíncrona deve ser nomeada `AsyncOperation` se ele retorna `Async<T>` ou `OperationAsync` se ele retorna `Task<T>`.</span><span class="sxs-lookup"><span data-stu-id="16c3e-290">If there is a corresponding synchronous operation named `Operation` that returns a `T`, then the async operation should be named `AsyncOperation` if it returns `Async<T>` or `OperationAsync` if it returns `Task<T>`.</span></span> <span data-ttu-id="16c3e-291">Para tipos de .NET comumente usados que expõem métodos Begin/End, considere o uso `Async.FromBeginEnd` para gravar os métodos de extensão como uma fachada para fornecer o F # modelo de programação assíncrona para essas APIs .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-291">For commonly used .NET types that expose Begin/End methods, consider using `Async.FromBeginEnd` to write extension methods as a façade to provide the F# async programming model to those .NET APIs.</span></span>

```fsharp
type SomeType =
    member this.Compute(x:int) : int =
        ...
    member this.AsyncCompute(x:int) : Async<int> =
        ...

type System.ServiceModel.Channels.IInputChannel with
    member this.AsyncReceive() =
        ...
```

### <a name="exceptions"></a><span data-ttu-id="16c3e-292">Exceções</span><span class="sxs-lookup"><span data-stu-id="16c3e-292">Exceptions</span></span>

<span data-ttu-id="16c3e-293">As exceções são excepcionais no .NET; ou seja, eles não devem ocorrer com frequência em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="16c3e-293">Exceptions are exceptional in .NET; that is, they should not occur frequently at runtime.</span></span> <span data-ttu-id="16c3e-294">Quando isso acontece, as informações que eles contêm serão valiosas.</span><span class="sxs-lookup"><span data-stu-id="16c3e-294">When they do, the information they contain is valuable.</span></span> <span data-ttu-id="16c3e-295">As exceções são um conceito de primeira classe do .NET; de núcleo IT, portanto, de maneira que apropriado aplicativo das exceções deve ser usadas como parte do design de interface de um componente.</span><span class="sxs-lookup"><span data-stu-id="16c3e-295">Exceptions are a core first class concept of .NET; it hence follows that appropriate application of the Exceptions should be used as part of the design of the interface of a component.</span></span>

#### <a name="follow-the-net-guidelines-for-exceptions"></a><span data-ttu-id="16c3e-296">Siga as diretrizes do .NET para exceções</span><span class="sxs-lookup"><span data-stu-id="16c3e-296">Follow the .NET guidelines for exceptions</span></span>

<span data-ttu-id="16c3e-297">O [diretrizes de Design de biblioteca do .NET](../../standard/design-guidelines/exceptions.md) dar ótimo conselho sobre o uso de exceções no contexto de programação do .NET todos os.</span><span class="sxs-lookup"><span data-stu-id="16c3e-297">The [.NET Library Design Guidelines](../../standard/design-guidelines/exceptions.md) give excellent advice on the use of exceptions in the context of all .NET programming.</span></span> <span data-ttu-id="16c3e-298">Algumas dessas diretrizes são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="16c3e-298">Some of these guidelines are as follows:</span></span>

* <span data-ttu-id="16c3e-299">Não use exceções para o fluxo normal de controle.</span><span class="sxs-lookup"><span data-stu-id="16c3e-299">Do not use exceptions for normal flow of control.</span></span> <span data-ttu-id="16c3e-300">Embora essa técnica é geralmente usada em idiomas como OCaml, ele é propensa a erros e pode ser ineficiente no .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-300">Although this technique is often used in languages such as OCaml, it is bug-prone and can be inefficient on .NET.</span></span> <span data-ttu-id="16c3e-301">Em vez disso, considere a possibilidade de retornar um `None` valor para indicar uma falha que é uma ocorrência comum ou esperada de opção.</span><span class="sxs-lookup"><span data-stu-id="16c3e-301">Instead, consider returning a `None` option value to indicate a failure that is a common or expected occurrence.</span></span>

* <span data-ttu-id="16c3e-302">Documente as exceções lançadas por componentes do seu quando uma função é usada incorretamente.</span><span class="sxs-lookup"><span data-stu-id="16c3e-302">Document exceptions thrown by your components when a function is used incorrectly.</span></span>

* <span data-ttu-id="16c3e-303">Sempre que possível, usar exceções existentes dos namespaces System.</span><span class="sxs-lookup"><span data-stu-id="16c3e-303">Where possible, employ existing exceptions from the System namespaces.</span></span> <span data-ttu-id="16c3e-304">Evite <xref:System.ApplicationException>, embora.</span><span class="sxs-lookup"><span data-stu-id="16c3e-304">Avoid <xref:System.ApplicationException>, though.</span></span>

* <span data-ttu-id="16c3e-305">Não emitem <xref:System.Exception> quando ele um caractere de escape ao código do usuário.</span><span class="sxs-lookup"><span data-stu-id="16c3e-305">Do not throw <xref:System.Exception> when it will escape to user code.</span></span> <span data-ttu-id="16c3e-306">Isso inclui a evitar o uso de `failwith`, `failwithf`, que são funções úteis para uso em scripts e código em desenvolvimento, mas devem ser removido de código da biblioteca F # em favor lançando um tipo de exceção mais específico.</span><span class="sxs-lookup"><span data-stu-id="16c3e-306">This includes avoiding the use of `failwith`, `failwithf`, which are handy functions for use in scripting and for code under development, but should be removed from F# library code in favor of throwing a more specific exception type.</span></span>

* <span data-ttu-id="16c3e-307">Use `nullArg`, `invalidArg`, e `invalidOp` como o mecanismo para lançar <xref:System.ArgumentNullException>, <xref:System.ArgumentException>, e <xref:System.InvalidOperationException> quando apropriado.</span><span class="sxs-lookup"><span data-stu-id="16c3e-307">Use `nullArg`, `invalidArg`, and `invalidOp` as the mechanism to throw <xref:System.ArgumentNullException>, <xref:System.ArgumentException>, and <xref:System.InvalidOperationException> when appropriate.</span></span>

#### <a name="consider-using-option-values-for-return-types-when-failure-is-not-an-exceptional-scenario"></a><span data-ttu-id="16c3e-308">Considere o uso de valores de opção para tipos de retorno quando a falha não é um cenário excepcional</span><span class="sxs-lookup"><span data-stu-id="16c3e-308">Consider using option values for return types when failure is not an exceptional scenario</span></span>

<span data-ttu-id="16c3e-309">A abordagem de .NET para exceções é que eles devem ser "excepcionais"; ou seja, eles devem ocorrer relativamente com pouca frequência.</span><span class="sxs-lookup"><span data-stu-id="16c3e-309">The .NET approach to exceptions is that they should be “exceptional”; that is, they should occur relatively infrequently.</span></span> <span data-ttu-id="16c3e-310">No entanto, algumas operações (por exemplo, uma tabela) podem falhar com frequência.</span><span class="sxs-lookup"><span data-stu-id="16c3e-310">However, some operations (for example, searching a table) may fail frequently.</span></span> <span data-ttu-id="16c3e-311">Os valores de opção F # são uma maneira excelente para representar os tipos de retorno dessas operações.</span><span class="sxs-lookup"><span data-stu-id="16c3e-311">F# option values are an excellent way to represent the return types of these operations.</span></span> <span data-ttu-id="16c3e-312">Essas operações convencionalmente começam com o prefixo de nome "try":</span><span class="sxs-lookup"><span data-stu-id="16c3e-312">These operations conventionally start with the name prefix “try”:</span></span>

```fsharp
// bad: throws exception if no element meets criteria
member this.FindFirstIndex(pred : 'T -> bool) : int =
    ...

// bad: returns -1 if no element meets criteria
member this.FindFirstIndex(pred : 'T -> bool) : int =
    ...

// good: returns None if no element meets criteria
member this.TryFindFirstIndex(pred : 'T -> bool) : int option =
    ...
```

### <a name="extension-members"></a><span data-ttu-id="16c3e-313">Membros de extensão</span><span class="sxs-lookup"><span data-stu-id="16c3e-313">Extension Members</span></span>

#### <a name="carefully-apply-f-extension-members-in-f-to-f-components"></a><span data-ttu-id="16c3e-314">Aplicar cuidadosamente os membros de extensão F # em F #-a-F # componentes</span><span class="sxs-lookup"><span data-stu-id="16c3e-314">Carefully apply F# extension members in F#-to-F# components</span></span>

<span data-ttu-id="16c3e-315">Membros de extensão do F #, geralmente, só devem ser usados para operações que estão no fechamento das operações intrínsecos associadas a um tipo na maioria dos modos de uso.</span><span class="sxs-lookup"><span data-stu-id="16c3e-315">F# extension members should generally only be used for operations that are in the closure of intrinsic operations associated with a type in the majority of its modes of use.</span></span> <span data-ttu-id="16c3e-316">Um uso comum é fornecer APIs que são mais idiomática para F # para vários tipos de .NET:</span><span class="sxs-lookup"><span data-stu-id="16c3e-316">One common use is to provide APIs that are more idiomatic to F# for various .NET types:</span></span>

```fsharp
type System.ServiceModel.Channels.IInputChannel with
    member this.AsyncReceive() =
        Async.FromBeginEnd(this.BeginReceive, this.EndReceive)

type System.Collections.Generic.IDictionary<'Key,'Value> with
    member this.TryGet key =
        let ok, v = this.TryGetValue key
        if ok then Some v else None
```

### <a name="union-types"></a><span data-ttu-id="16c3e-317">Tipos de união</span><span class="sxs-lookup"><span data-stu-id="16c3e-317">Union Types</span></span>

#### <a name="use-discriminated-unions-instead-of-class-hierarchies-for-tree-structured-data"></a><span data-ttu-id="16c3e-318">Use uniões discriminadas em vez de hierarquias de classe para dados estruturados em árvore</span><span class="sxs-lookup"><span data-stu-id="16c3e-318">Use discriminated unions instead of class hierarchies for tree-structured data</span></span>

<span data-ttu-id="16c3e-319">Estruturas de árvore são definidos recursivamente.</span><span class="sxs-lookup"><span data-stu-id="16c3e-319">Tree-like structures are recursively defined.</span></span> <span data-ttu-id="16c3e-320">Isso é complicado com herança, mas elegante com uniões discriminada.</span><span class="sxs-lookup"><span data-stu-id="16c3e-320">This is awkward with inheritance, but elegant with Discriminated Unions.</span></span>

```fsharp
type BST<'T> =
    | Empty
    | Node of 'T * BST<'T> * BST<'T>
```

<span data-ttu-id="16c3e-321">Que representa dados de árvore com uniões discriminada também permite que você se beneficiar de exhaustiveness na correspondência de padrões.</span><span class="sxs-lookup"><span data-stu-id="16c3e-321">Representing tree-like data with Discriminated Unions also allows you to benefit from exhaustiveness in pattern matching.</span></span>

#### <a name="use-requirequalifiedaccess-on-union-types-whose-case-names-are-not-sufficiently-unique"></a><span data-ttu-id="16c3e-322">Use `[<RequireQualifiedAccess>]` em tipos de união cujos nomes casos não forem suficientemente exclusivos</span><span class="sxs-lookup"><span data-stu-id="16c3e-322">Use `[<RequireQualifiedAccess>]` on union types whose case names are not sufficiently unique</span></span>

<span data-ttu-id="16c3e-323">Você pode perceber que está em um domínio onde o mesmo nome é o melhor nome para coisas diferentes, como casos união discriminada.</span><span class="sxs-lookup"><span data-stu-id="16c3e-323">You may find yourself in a domain where the same name is the best name for different things, such as Discriminated Union cases.</span></span> <span data-ttu-id="16c3e-324">Você pode usar `[<RequireQualifiedAccess>]` para resolver a ambiguidade de nomes com maiusculas para evitar disparar erros confusos devido ao sombreamento dependentes a ordenação de `open` instruções</span><span class="sxs-lookup"><span data-stu-id="16c3e-324">You can use `[<RequireQualifiedAccess>]` to disambiguate case names in order to avoid triggering confusing errors due to shadowing dependent on the ordering of `open` statements</span></span>

#### <a name="hide-the-representations-of-discriminated-unions-for-binary-compatible-apis-if-the-design-of-these-types-is-likely-to-evolve"></a><span data-ttu-id="16c3e-325">Ocultar as representações de uniões discriminadas binário APIs compatível se o design desses tipos é mais provável de envolver</span><span class="sxs-lookup"><span data-stu-id="16c3e-325">Hide the representations of discriminated unions for binary compatible APIs if the design of these types is likely to evolve</span></span>

<span data-ttu-id="16c3e-326">Tipos de uniões dependem de F # correspondência formulários para um modelo de programação sucinto.</span><span class="sxs-lookup"><span data-stu-id="16c3e-326">Unions types rely on F# pattern-matching forms for a succinct programming model.</span></span> <span data-ttu-id="16c3e-327">Conforme mencionado anteriormente, você deve evitar revelar representações de dados concretos se mais provável de envolver o design desses tipos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-327">As mentioned previously, you should avoid revealing concrete data representations if the design of these types is likely to evolve.</span></span>

<span data-ttu-id="16c3e-328">Por exemplo, a representação de uma união discriminada pode ser ocultada usando uma declaração privada ou interna, ou usando um arquivo de assinatura.</span><span class="sxs-lookup"><span data-stu-id="16c3e-328">For example, the representation of a discriminated union can be hidden using a private or internal declaration, or by using a signature file.</span></span>

```fsharp
type Union =
    private
    | CaseA of int
    | CaseB of string
```

<span data-ttu-id="16c3e-329">Se você revelar uniões discriminadas modo indiscriminado, talvez seja difícil versão sua biblioteca sem quebrar o código do usuário.</span><span class="sxs-lookup"><span data-stu-id="16c3e-329">If you reveal discriminated unions indiscriminately, you may find it hard to version your library without breaking user code.</span></span> <span data-ttu-id="16c3e-330">Em vez disso, considere a possibilidade de revelar um ou mais padrões ativos para permitir correspondência sobre os valores do seu tipo de padrão.</span><span class="sxs-lookup"><span data-stu-id="16c3e-330">Instead, consider revealing one or more active patterns to permit pattern matching over values of your type.</span></span>

<span data-ttu-id="16c3e-331">Padrões ativos fornecem uma maneira alternativa para oferecer aos consumidores de F # padrão de correspondência, evitando a exposição de tipos de união F # diretamente.</span><span class="sxs-lookup"><span data-stu-id="16c3e-331">Active patterns provide an alternate way to provide F# consumers with pattern matching while avoiding exposing F# Union Types directly.</span></span>

### <a name="inline-functions-and-member-constraints"></a><span data-ttu-id="16c3e-332">Funções embutidas e restrições de membro</span><span class="sxs-lookup"><span data-stu-id="16c3e-332">Inline Functions and Member Constraints</span></span>

#### <a name="define-generic-numeric-algorithms-using-inline-functions-with-implied-member-constraints-and-statically-resolved-generic-types"></a><span data-ttu-id="16c3e-333">Definir genéricos algoritmos numéricos usando funções embutidas com restrições de membro implícito e tipos genéricos resolvidos estaticamente</span><span class="sxs-lookup"><span data-stu-id="16c3e-333">Define generic numeric algorithms using inline functions with implied member constraints and statically resolved generic types</span></span>

<span data-ttu-id="16c3e-334">Membro aritmético restrições e F # comparação são um padrão de programação F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-334">Arithmetic member constraints and F# comparison constraints are a standard for F# programming.</span></span> <span data-ttu-id="16c3e-335">Por exemplo, considere o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="16c3e-335">For example, consider the following code:</span></span>

```fsharp
let inline highestCommonFactor a b =
    let rec loop a b =
        if a = LanguagePrimitives.GenericZero<_> then b
        elif a < b then loop a (b - a)
        else loop (a - b) b
    loop a b
```

<span data-ttu-id="16c3e-336">O tipo dessa função é como segue:</span><span class="sxs-lookup"><span data-stu-id="16c3e-336">The type of this function is as follows:</span></span>

```fsharp
val inline highestCommonFactor : ^T -> ^T -> ^T
                when ^T : (static member Zero : ^T)
                and ^T : (static member ( - ) : ^T * ^T -> ^T)
                and ^T : equality
                and ^T : comparison
```

<span data-ttu-id="16c3e-337">Essa é uma função adequada para uma API pública em uma biblioteca de matemática.</span><span class="sxs-lookup"><span data-stu-id="16c3e-337">This is a suitable function for a public API in a mathematical library.</span></span>

#### <a name="avoid-using-member-constraints-to-simulate-type-classes-and-duck-typing"></a><span data-ttu-id="16c3e-338">Evite usar restrições de membro para simular classes de tipo e digitação pato</span><span class="sxs-lookup"><span data-stu-id="16c3e-338">Avoid using member constraints to simulate type classes and duck typing</span></span>

<span data-ttu-id="16c3e-339">É possível simular "Jantar digitando" usando as restrições de membro F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-339">It is possible to simulate “duck typing” using F# member constraints.</span></span> <span data-ttu-id="16c3e-340">No entanto, os membros que usam esse geral não deve ser usada em F #-para-designs de biblioteca F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-340">However, members that make use of this should not in general be used in F#-to-F# library designs.</span></span> <span data-ttu-id="16c3e-341">Isso ocorre porque os designs de biblioteca com base em restrições implícita desconhecidas ou não-padrão tendem a fazer com que o código do usuário se tornar inflexíveis e associado ao padrão de uma estrutura específica.</span><span class="sxs-lookup"><span data-stu-id="16c3e-341">This is because library designs based on unfamiliar or non-standard implicit constraints tend to cause user code to become inflexible and tied to one particular framework pattern.</span></span>

<span data-ttu-id="16c3e-342">Além disso, há uma boa chance de uso intenso de restrições de membro dessa maneira pode resultar em tempo de compilação muito longo.</span><span class="sxs-lookup"><span data-stu-id="16c3e-342">Additionally, there is a good chance that heavy use of member constraints in this manner can result in very long compile times.</span></span>

### <a name="operator-definitions"></a><span data-ttu-id="16c3e-343">Definições de operador</span><span class="sxs-lookup"><span data-stu-id="16c3e-343">Operator Definitions</span></span>

#### <a name="avoid-defining-custom-symbolic-operators"></a><span data-ttu-id="16c3e-344">Evite definir operadores simbólicos personalizados</span><span class="sxs-lookup"><span data-stu-id="16c3e-344">Avoid defining custom symbolic operators</span></span>

<span data-ttu-id="16c3e-345">Operadores personalizados são essenciais em algumas situações e altamente útil dispositivos notação dentro de um corpo grande do código de implementação.</span><span class="sxs-lookup"><span data-stu-id="16c3e-345">Custom operators are essential in some situations and are highly useful notational devices within a large body of implementation code.</span></span> <span data-ttu-id="16c3e-346">Para novos usuários de uma biblioteca, denominado funções geralmente são mais fáceis de usar.</span><span class="sxs-lookup"><span data-stu-id="16c3e-346">For new users of a library, named functions are often easier to use.</span></span> <span data-ttu-id="16c3e-347">Além disso, operadores simbólicos personalizados podem ser difíceis de documento e os usuários encontram mais difícil procurar ajuda sobre operadores, devido a limitações existentes nos mecanismos IDE e pesquisa.</span><span class="sxs-lookup"><span data-stu-id="16c3e-347">In addition, custom symbolic operators can be hard to document, and users find it more difficult to look up help on operators, due to existing limitations in IDE and search engines.</span></span>

<span data-ttu-id="16c3e-348">Como resultado, é melhor publicar sua funcionalidade como funções nomeadas e membros e Além disso expor operadores para essa funcionalidade somente se os benefícios de notação superam a documentação e o custo cognitivo de tê-los.</span><span class="sxs-lookup"><span data-stu-id="16c3e-348">As a result, it is best to publish your functionality as named functions and members, and additionally expose operators for this functionality only if the notational benefits outweigh the documentation and cognitive cost of having them.</span></span>

### <a name="units-of-measure"></a><span data-ttu-id="16c3e-349">Unidades de medida</span><span class="sxs-lookup"><span data-stu-id="16c3e-349">Units of Measure</span></span>

#### <a name="carefully-use-units-of-measure-for-added-type-safety-in-f-code"></a><span data-ttu-id="16c3e-350">Cuidadosamente usar unidades de medida de segurança de tipo adicionados no código F #</span><span class="sxs-lookup"><span data-stu-id="16c3e-350">Carefully use units of measure for added type safety in F# code</span></span>

<span data-ttu-id="16c3e-351">Informações adicionais de digitação para as unidades de medida são apagadas quando vistos por outras linguagens .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-351">Additional typing information for units of measure is erased when viewed by other .NET languages.</span></span> <span data-ttu-id="16c3e-352">Lembre-se de reflexão, ferramentas e componentes do .NET Consulte tipos sans unidades.</span><span class="sxs-lookup"><span data-stu-id="16c3e-352">Be aware that .NET components, tools, and reflection will see types-sans-units.</span></span> <span data-ttu-id="16c3e-353">Por exemplo, verá c# consumidores `float` em vez de `float<kg>`.</span><span class="sxs-lookup"><span data-stu-id="16c3e-353">For example, C# consumers will see `float` rather than `float<kg>`.</span></span>

### <a name="type-abbreviations"></a><span data-ttu-id="16c3e-354">Abreviações de tipo</span><span class="sxs-lookup"><span data-stu-id="16c3e-354">Type Abbreviations</span></span>

#### <a name="carefully-use-type-abbreviations-to-simplify-f-code"></a><span data-ttu-id="16c3e-355">Use com cuidado abreviações de tipo para simplificar o código F #</span><span class="sxs-lookup"><span data-stu-id="16c3e-355">Carefully use type abbreviations to simplify F# code</span></span>

<span data-ttu-id="16c3e-356">Reflexão, ferramentas e componentes do .NET não verá nomes abreviados de tipos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-356">.NET components, tools, and reflection will not see abbreviated names for types.</span></span> <span data-ttu-id="16c3e-357">Uso significativo de abreviações de tipo também pode fazer um domínio aparecem mais complicado do que na verdade é, que pode confundir os consumidores.</span><span class="sxs-lookup"><span data-stu-id="16c3e-357">Significant usage of type abbreviations can also make a domain appear more complex than it actually is, which could confuse consumers.</span></span>

#### <a name="avoid-type-abbreviations-for-public-types-whose-members-and-properties-should-be-intrinsically-different-to-those-available-on-the-type-being-abbreviated"></a><span data-ttu-id="16c3e-358">Evite abreviações de tipo para os tipos públicos cujos membros e propriedades devem ser intrinsecamente diferentes daqueles disponível no tipo sendo abreviado</span><span class="sxs-lookup"><span data-stu-id="16c3e-358">Avoid type abbreviations for public types whose members and properties should be intrinsically different to those available on the type being abbreviated</span></span>

<span data-ttu-id="16c3e-359">Nesse caso, o tipo sendo abreviado revela muito sobre a representação do tipo real que está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="16c3e-359">In this case, the type being abbreviated reveals too much about the representation of the actual type being defined.</span></span> <span data-ttu-id="16c3e-360">Em vez disso, considere a abreviação em um tipo de classe ou uma união discriminada único caso de encapsulamento (ou, quando o desempenho é essencial, considere o uso de um tipo struct para encapsular a abreviação).</span><span class="sxs-lookup"><span data-stu-id="16c3e-360">Instead, consider wrapping the abbreviation in a class type or a single-case discriminated union (or, when performance is essential, consider using a struct type to wrap the abbreviation).</span></span>

<span data-ttu-id="16c3e-361">Por exemplo, é tentador para definir um multi-mapa de como um caso especial de um mapa de F #, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="16c3e-361">For example, it is tempting to define a multi-map as a special case of an F# map, for example:</span></span>

```fsharp
type MultiMap<'Key,'Value> = Map<'Key,'Value list>
```

<span data-ttu-id="16c3e-362">No entanto, as operações lógicas de notação de ponto neste tipo não são as mesmas operações em um mapa — por exemplo, é razoável de que o operador de pesquisa do mapa. [chave] retornar uma lista vazia se a chave não estiver no dicionário, em vez de gerar uma exceção.</span><span class="sxs-lookup"><span data-stu-id="16c3e-362">However, the logical dot-notation operations on this type are not the same as the operations on a Map – for example, it is reasonable that the lookup operator map.[key] return the empty list if the key is not in the dictionary, rather than raising an exception.</span></span>

## <a name="guidelines-for-libraries-for-use-from-other-net-languages"></a><span data-ttu-id="16c3e-363">Diretrizes para bibliotecas para uso em outras linguagens .NET</span><span class="sxs-lookup"><span data-stu-id="16c3e-363">Guidelines for libraries for Use from other .NET Languages</span></span>

<span data-ttu-id="16c3e-364">Durante a criação de bibliotecas para uso em outras linguagens .NET, é importante seguir o [diretrizes de Design de biblioteca do .NET](../../standard/design-guidelines/index.md).</span><span class="sxs-lookup"><span data-stu-id="16c3e-364">When designing libraries for use from other .NET languages, it is important to adhere to the [.NET Library Design Guidelines](../../standard/design-guidelines/index.md).</span></span> <span data-ttu-id="16c3e-365">Neste documento, essas bibliotecas são rotuladas como baunilha bibliotecas .NET, em vez de F #-voltada para bibliotecas que usam F # constrói sem restrição.</span><span class="sxs-lookup"><span data-stu-id="16c3e-365">In this document, these libraries are labeled as vanilla .NET libraries, as opposed to F#-facing libraries that use F# constructs without restriction.</span></span> <span data-ttu-id="16c3e-366">Criar bibliotecas do .NET baunilha significa fornecendo familiar e idiomática APIs consistentes com o restante do .NET Framework, reduzindo o uso da linguagem F #-construções específicas na API pública.</span><span class="sxs-lookup"><span data-stu-id="16c3e-366">Designing vanilla .NET libraries means providing familiar and idiomatic APIs consistent with the rest of the .NET Framework by minimizing the use of F#-specific constructs in the public API.</span></span> <span data-ttu-id="16c3e-367">As regras são explicadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="16c3e-367">The rules are explained in the following sections.</span></span>

### <a name="namespace-and-type-sesign-for-libraries-for-use-from-other-net-languages"></a><span data-ttu-id="16c3e-368">Namespace e tipo sesign (para bibliotecas para uso em outras linguagens .NET)</span><span class="sxs-lookup"><span data-stu-id="16c3e-368">Namespace and Type sesign (for libraries for use from other .NET Languages)</span></span>

#### <a name="apply-the-net-naming-conventions-to-the-public-api-of-your-components"></a><span data-ttu-id="16c3e-369">Aplicar as convenções de nomenclatura do .NET para a API pública de seus componentes</span><span class="sxs-lookup"><span data-stu-id="16c3e-369">Apply the .NET naming conventions to the public API of your components</span></span>

<span data-ttu-id="16c3e-370">Preste atenção especial para o uso de nomes abreviados e as diretrizes de capitalização do .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-370">Pay special attention to the use of abbreviated names and the .NET capitalization guidelines.</span></span>

```fsharp
type pCoord = ...
    member this.theta = ...

type PolarCoordinate = ...
    member this.Theta = ...
```

#### <a name="use-namespaces-types-and-members-as-the-primary-organizational-structure-for-your-components"></a><span data-ttu-id="16c3e-371">Usar namespaces, tipos e membros como a estrutura organizacional primária para os componentes</span><span class="sxs-lookup"><span data-stu-id="16c3e-371">Use namespaces, types, and members as the primary organizational structure for your components</span></span>

<span data-ttu-id="16c3e-372">Todos os arquivos que contém a funcionalidade de pública devem começar com um `namespace` declaração e as entidades públicos somente namespaces devem ser tipos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-372">All files containing public functionality should begin with a `namespace` declaration, and the only public-facing entities in namespaces should be types.</span></span> <span data-ttu-id="16c3e-373">Não use os módulos de F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-373">Do not use F# modules.</span></span>

<span data-ttu-id="16c3e-374">Use os módulos de não-públicos para manter o código de implementação, utilitário tipos e funções de utilitário.</span><span class="sxs-lookup"><span data-stu-id="16c3e-374">Use non-public modules to hold implementation code, utility types, and utility functions.</span></span>

<span data-ttu-id="16c3e-375">Tipos estáticos devem ser preferidos nos módulos, já que permitem futura evolução da API para usar a sobrecarga e outros conceitos de design API .NET que não podem ser usados dentro de módulos do F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-375">Static types should be preferred over modules, as they allow for future evolution of the API to use overloading and other .NET API design concepts that may not be used within F# modules.</span></span>

<span data-ttu-id="16c3e-376">Por exemplo, em vez da API pública do seguinte:</span><span class="sxs-lookup"><span data-stu-id="16c3e-376">For example, in place of the following public API:</span></span>

```fsharp
module Fabrikam

module Utilities =
    let Name = "Bob"
    let Add2 x y = x + y
    let Add3 x y z = x + y + z
```

<span data-ttu-id="16c3e-377">Em vez disso, considere:</span><span class="sxs-lookup"><span data-stu-id="16c3e-377">Consider instead:</span></span>

```fsharp
namespace Fabrikam

[<AbstractClass; Sealed>]
type Utilities =
    static member Name = "Bob"
    static member Add(x,y) = x + y
    static member Add(x,y,z) = x + y + z
```

#### <a name="use-f-record-types-in-vanilla-net-apis-if-the-design-of-the-types-wont-evolve"></a><span data-ttu-id="16c3e-378">Use os tipos de registro F # baunilha APIs .NET se o design dos tipos não evoluir</span><span class="sxs-lookup"><span data-stu-id="16c3e-378">Use F# record types in vanilla .NET APIs if the design of the types won't evolve</span></span>

<span data-ttu-id="16c3e-379">Tipos de registro F # compilados para uma classe simples do .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-379">F# record types compile to a simple .NET class.</span></span> <span data-ttu-id="16c3e-380">Eles são adequados para alguns tipos simples e estáveis nas APIs.</span><span class="sxs-lookup"><span data-stu-id="16c3e-380">These are suitable for some simple, stable types in APIs.</span></span> <span data-ttu-id="16c3e-381">Você deve considerar o uso de `[<NoEquality>]` e `[<NoComparison>]` atributos para suprimir a geração automática de interfaces.</span><span class="sxs-lookup"><span data-stu-id="16c3e-381">You should consider using the `[<NoEquality>]` and `[<NoComparison>]` attributes to suppress the automatic generation of interfaces.</span></span> <span data-ttu-id="16c3e-382">Além disso, evite usar campos de registro mutável em baunilha APIs .NET como esses expõe um campo público.</span><span class="sxs-lookup"><span data-stu-id="16c3e-382">Also avoid using mutable record fields in vanilla .NET APIs as these exposes a public field.</span></span> <span data-ttu-id="16c3e-383">Sempre considere se uma classe seria fornecem uma opção mais flexível para futuras evolução da API.</span><span class="sxs-lookup"><span data-stu-id="16c3e-383">Always consider whether a class would provide a more flexible option for future evolution of the API.</span></span>

<span data-ttu-id="16c3e-384">Por exemplo, o seguinte código F # expõe a API pública de um consumidor do c#:</span><span class="sxs-lookup"><span data-stu-id="16c3e-384">For example, the following F# code exposes the public API to a C# consumer:</span></span>

<span data-ttu-id="16c3e-385">F #:</span><span class="sxs-lookup"><span data-stu-id="16c3e-385">F#:</span></span>

```fsharp
[<NoEquality; NoComparison>]
type MyRecord =
    { FirstThing : int
        SecondThing : string }
```

<span data-ttu-id="16c3e-386">C#:</span><span class="sxs-lookup"><span data-stu-id="16c3e-386">C#:</span></span>

```csharp
public sealed class MyRecord
{
    public MyRecord(int firstThing, string secondThing);
    public int FirstThing { get; }
    public string SecondThing { get; }
}
```

#### <a name="hide-the-representation-of-f-union-types-in-vanilla-net-apis"></a><span data-ttu-id="16c3e-387">Ocultar a representação de tipos de união F # em baunilha APIs do .NET</span><span class="sxs-lookup"><span data-stu-id="16c3e-387">Hide the representation of F# union types in vanilla .NET APIs</span></span>

<span data-ttu-id="16c3e-388">Tipos de união F # não são normalmente usados nos limites do componente, mesmo para F #-a-F # codificação.</span><span class="sxs-lookup"><span data-stu-id="16c3e-388">F# union types are not commonly used across component boundaries, even for F#-to-F# coding.</span></span> <span data-ttu-id="16c3e-389">Eles são um dispositivo de implementação excelente quando usado internamente no bibliotecas e componentes.</span><span class="sxs-lookup"><span data-stu-id="16c3e-389">They are an excellent implementation device when used internally within components and libraries.</span></span>

<span data-ttu-id="16c3e-390">Durante a criação de uma API .NET baunilha, considere a possibilidade de ocultar a representação de um tipo de união, usando uma declaração privada ou um arquivo de assinatura.</span><span class="sxs-lookup"><span data-stu-id="16c3e-390">When designing a vanilla .NET API, consider hiding the representation of a union type by using either a private declaration or a signature file.</span></span>

```fsharp
type PropLogic =
    private
    | And of PropLogic * PropLogic
    | Not of PropLogic
    | True
```

<span data-ttu-id="16c3e-391">Você também poderá aumentar tipos que usam uma representação de união internamente com membros para fornecer um desejado. API de voltado para a rede.</span><span class="sxs-lookup"><span data-stu-id="16c3e-391">You may also augment types that use a union representation internally with members to provide a desired .NET-facing API.</span></span>

```fsharp
type PropLogic =
    private
    | And of PropLogic * PropLogic
    | Not of PropLogic
    | True

    /// A public member for use from C#
    member x.Evaluate =
        match x with
        | And(a,b) -> a.Evaluate && b.Evaluate
        | Not a -> not a.Evaluate
        | True -> true

    /// A public member for use from C#
    static member CreateAnd(a,b) = And(a,b)
```

#### <a name="design-gui-and-other-components-using-the-design-patterns-of-the-framework"></a><span data-ttu-id="16c3e-392">Design de interface gráfica do usuário e outros componentes usando os padrões de design do framework</span><span class="sxs-lookup"><span data-stu-id="16c3e-392">Design GUI and other components using the design patterns of the framework</span></span>

<span data-ttu-id="16c3e-393">Há muitas estruturas diferentes no .NET, como WinForms, WPF e ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-393">There are many different frameworks available within .NET, such as WinForms, WPF, and ASP.NET.</span></span> <span data-ttu-id="16c3e-394">Convenções de nomenclatura e design para cada um devem ser usadas se você estiver criando componentes para uso nessas estruturas.</span><span class="sxs-lookup"><span data-stu-id="16c3e-394">Naming and design conventions for each should be used if you are designing components for use in these frameworks.</span></span> <span data-ttu-id="16c3e-395">Por exemplo, para WPF de programação, adote padrões de design do WPF para as classes que você está criando.</span><span class="sxs-lookup"><span data-stu-id="16c3e-395">For example, for WPF programming, adopt WPF design patterns for the classes you are designing.</span></span> <span data-ttu-id="16c3e-396">Para modelos de programação de interface do usuário, use padrões de design, como eventos e baseada em notificação coleções, como aqueles encontrados em <xref:System.Collections.ObjectModel>.</span><span class="sxs-lookup"><span data-stu-id="16c3e-396">For models in user interface programming, use design patterns such as events and notification-based collections such as those found in <xref:System.Collections.ObjectModel>.</span></span>

### <a name="object-and-member-design-for-libraries-for-use-from-other-net-languages"></a><span data-ttu-id="16c3e-397">Design de objeto e o membro (para bibliotecas para uso em outras linguagens .NET)</span><span class="sxs-lookup"><span data-stu-id="16c3e-397">Object and Member design (for libraries for use from other .NET Languages)</span></span>

#### <a name="use-the-clievent-attribute-to-expose-net-events"></a><span data-ttu-id="16c3e-398">Use o atributo CLIEvent para expor os eventos do .NET</span><span class="sxs-lookup"><span data-stu-id="16c3e-398">Use the CLIEvent attribute to expose .NET events</span></span>

<span data-ttu-id="16c3e-399">Construir um `DelegateEvent` com .NET específica de tipo que utiliza um objeto delegado e `EventArgs` (em vez de um `Event`, que usa apenas o `FSharpHandler` tipo por padrão) para que os eventos são publicados na maneira familiar de outras linguagens .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-399">Construct a `DelegateEvent` with a specific .NET delegate type that takes an object and `EventArgs` (rather than an `Event`, which just uses the `FSharpHandler` type by default) so that the events are published in the familiar way to other .NET languages.</span></span>

```fsharp
type MyBadType() =
    let myEv = new Event<int>()

    [<CLIEvent>]
    member this.MyEvent = myEv.Publish

type MyEventArgs(x:int) =
    inherit System.EventArgs()
    member this.X = x

    /// A type in a component designed for use from other .NET languages
type MyGoodType() =
    let myEv = new DelegateEvent<EventHandler<MyEventArgs>>()

    [<CLIEvent>]
    member this.MyEvent = myEv.Publish
```

#### <a name="expose-asynchronous-operations-as-methods-which-return-net-tasks"></a><span data-ttu-id="16c3e-400">Expor operações assíncronas como métodos que retornam tarefas do .NET</span><span class="sxs-lookup"><span data-stu-id="16c3e-400">Expose asynchronous operations as methods which return .NET tasks</span></span>

<span data-ttu-id="16c3e-401">Tarefas são usadas em .NET para representar active computações assíncronas.</span><span class="sxs-lookup"><span data-stu-id="16c3e-401">Tasks are used in .NET to represent active asynchronous computations.</span></span> <span data-ttu-id="16c3e-402">Tarefas são em geral composicional menor que F # `Async<T>` objetos, uma vez que representam tarefas "já em execução" e não podem ser compostos juntas de maneiras que realizar a composição de paralela, ou que ocultar a propagação de sinais de cancelamento e outros parâmetros de contextuais.</span><span class="sxs-lookup"><span data-stu-id="16c3e-402">Tasks are in general less compositional than F# `Async<T>` objects, since they represent “already executing” tasks and can’t be composed together in ways that perform parallel composition, or which hide the propagation of cancellation signals and other contextual parameters.</span></span>

<span data-ttu-id="16c3e-403">No entanto, apesar de isso, os métodos que retornam tarefas são a representação padrão de programação assíncrona em .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-403">However, despite this, methods which return Tasks are the standard representation of asynchronous programming on .NET.</span></span>

```fsharp
/// A type in a component designed for use from other .NET languages
type MyType() =

    let compute (x: int) : Async<int> = async { ... }

    member this.ComputeAsync(x) = compute x |> Async.StartAsTask
```

<span data-ttu-id="16c3e-404">Você vai frequentemente também deseja aceitar um token de cancelamento explícita:</span><span class="sxs-lookup"><span data-stu-id="16c3e-404">You will frequently also want to accept an explicit cancellation token:</span></span>

```fsharp
/// A type in a component designed for use from other .NET languages
type MyType() =
    let compute(x:int) : Async<int> = async { ... }
    member this.ComputeAsTask(x, cancellationToken) = Async.StartAsTask(compute x, cancellationToken)
```

#### <a name="use-net-delegate-types-instead-of-f-function-types"></a><span data-ttu-id="16c3e-405">Usar tipos de delegado do .NET em vez de tipos de função do F #</span><span class="sxs-lookup"><span data-stu-id="16c3e-405">Use .NET delegate types instead of F# function types</span></span>

<span data-ttu-id="16c3e-406">Aqui "tipos de função F #" significam "direção" tipos como `int -> int`.</span><span class="sxs-lookup"><span data-stu-id="16c3e-406">Here “F# function types” mean “arrow” types like `int -> int`.</span></span>

<span data-ttu-id="16c3e-407">Em vez de isso:</span><span class="sxs-lookup"><span data-stu-id="16c3e-407">Instead of this:</span></span>

```fsharp
member this.Transform(f:int->int) =
    ...
```

<span data-ttu-id="16c3e-408">Faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="16c3e-408">Do this:</span></span>

```fsharp
member this.Transform(f:Func<int,int>) =
    ...
```

<span data-ttu-id="16c3e-409">O tipo de função do F # aparece como `class FSharpFunc<T,U>` a outras linguagens .NET e é menos adequada para recursos de linguagem e ferramentas que entender os tipos de delegado.</span><span class="sxs-lookup"><span data-stu-id="16c3e-409">The F# function type appears as `class FSharpFunc<T,U>` to other .NET languages, and is less suitable for language features and tooling that understand delegate types.</span></span> <span data-ttu-id="16c3e-410">Ao criar um método de ordem superior direcionamento do .NET Framework 3.5 ou superior, o `System.Func` e `System.Action` delegados são as APIs do direito para publicar para permitir que os desenvolvedores de .NET consumir essas APIs de uma maneira de baixa fricção.</span><span class="sxs-lookup"><span data-stu-id="16c3e-410">When authoring a higher-order method targeting .NET Framework 3.5 or higher, the `System.Func` and `System.Action` delegates are the right APIs to publish to enable .NET developers to consume these APIs in a low-friction manner.</span></span> <span data-ttu-id="16c3e-411">(Durante o direcionamento do .NET Framework 2.0, os tipos de delegado definido pelo sistema são mais limitados; considere o uso de tipos de delegado predefinidos, como `System.Converter<T,U>` ou definição de um tipo específico de delegado.)</span><span class="sxs-lookup"><span data-stu-id="16c3e-411">(When targeting .NET Framework 2.0, the system-defined delegate types are more limited; consider using predefined delegate types such as `System.Converter<T,U>` or defining a specific delegate type.)</span></span>

<span data-ttu-id="16c3e-412">Por outro lado, os delegados do .NET não são naturais para F #-voltada para bibliotecas (consulte a próxima seção em F #-voltada para bibliotecas).</span><span class="sxs-lookup"><span data-stu-id="16c3e-412">On the flip side, .NET delegates are not natural for F#-facing libraries (see the next Section on F#-facing libraries).</span></span> <span data-ttu-id="16c3e-413">Como resultado, uma estratégia de implementação comum ao desenvolver métodos de ordem superior para bibliotecas do .NET baunilha é criar todas a implementação usando tipos de função do F # e, em seguida, crie a API pública usando delegados como uma fachada thin sobre F # real implementação.</span><span class="sxs-lookup"><span data-stu-id="16c3e-413">As a result, a common implementation strategy when developing higher-order methods for vanilla .NET libraries is to author all the implementation using F# function types, and then create the public API using delegates as a thin façade atop the actual F# implementation.</span></span>

#### <a name="use-the-trygetvalue-pattern-instead-of-returning-f-option-values-and-prefer-method-overloading-to-taking-f-option-values-as-arguments"></a><span data-ttu-id="16c3e-414">Use o padrão de TryGetValue em vez de retornar valores de opção de F # e prefere a sobrecarga de método para colocar valores de opção F # como argumentos</span><span class="sxs-lookup"><span data-stu-id="16c3e-414">Use the TryGetValue pattern instead of returning F# option values, and prefer method overloading to taking F# option values as arguments</span></span>

<span data-ttu-id="16c3e-415">Padrões comuns de uso para o tipo de opção F # em APIs são melhores implementado em baunilha APIs do .NET usando .NET padrão técnicas de design.</span><span class="sxs-lookup"><span data-stu-id="16c3e-415">Common patterns of use for the F# option type in APIs are better implemented in vanilla .NET APIs using standard .NET design techniques.</span></span> <span data-ttu-id="16c3e-416">Em vez de retornar um valor de opção F #, considere usar o tipo de retorno booleano mais de um parâmetro de saída como o padrão "TryGetValue".</span><span class="sxs-lookup"><span data-stu-id="16c3e-416">Instead of returning an F# option value, consider using the bool return type plus an out parameter as in the "TryGetValue" pattern.</span></span> <span data-ttu-id="16c3e-417">E, em vez de usar valores de opção F # como parâmetros, considere usar a sobrecarga de método ou argumentos opcionais.</span><span class="sxs-lookup"><span data-stu-id="16c3e-417">And instead of taking F# option values as parameters, consider using method overloading or optional arguments.</span></span>

```fsharp
member this.ReturnOption() = Some 3

member this.ReturnBoolAndOut(outVal : byref<int>) =
    outVal <- 3
    true

member this.ParamOption(x : int, y : int option) =
    match y with
    | Some y2 -> x + y2
    | None -> x

member this.ParamOverload(x : int) = x

member this.ParamOverload(x : int, y : int) = x + y
```

#### <a name="use-the-net-collection-interface-types-ienumerablet-and-idictionarykeyvalue-for-parameters-and-return-values"></a><span data-ttu-id="16c3e-418">Use a interface de coleção do .NET tipos IEnumerable\<T\> e IDictionary\<chave, valor\> para parâmetros e valores de retorno</span><span class="sxs-lookup"><span data-stu-id="16c3e-418">Use the .NET collection interface types IEnumerable\<T\> and IDictionary\<Key,Value\> for parameters and return values</span></span>

<span data-ttu-id="16c3e-419">Evite o uso de tipos de coleção concretos, como matrizes de .NET `T[]`, tipos F # `list<T>`, `Map<Key,Value>` e `Set<T>`, e tipos de coleção concreta do .NET, como `Dictionary<Key,Value>`.</span><span class="sxs-lookup"><span data-stu-id="16c3e-419">Avoid the use of concrete collection types such as .NET arrays `T[]`, F# types `list<T>`, `Map<Key,Value>` and `Set<T>`, and .NET concrete collection types such as `Dictionary<Key,Value>`.</span></span> <span data-ttu-id="16c3e-420">As diretrizes de Design de biblioteca .NET ter conselhos sobre quando usar vários tipos de coleção como `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="16c3e-420">The .NET Library Design Guidelines have good advice regarding when to use various collection types like `IEnumerable<T>`.</span></span> <span data-ttu-id="16c3e-421">Uso de matrizes (`T[]`) é aceitável em algumas circunstâncias, em para terrenos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="16c3e-421">Some use of arrays (`T[]`) is acceptable in some circumstances, on performance grounds.</span></span> <span data-ttu-id="16c3e-422">Observe especialmente que `seq<T>` é apenas o F # alias para `IEnumerable<T>`, e, portanto, seq geralmente é um tipo apropriado para uma API .NET baunilha.</span><span class="sxs-lookup"><span data-stu-id="16c3e-422">Note especially that `seq<T>` is just the F# alias for `IEnumerable<T>`, and thus seq is often an appropriate type for a vanilla .NET API.</span></span>

<span data-ttu-id="16c3e-423">Em vez de F # listas:</span><span class="sxs-lookup"><span data-stu-id="16c3e-423">Instead of F# lists:</span></span>

```fsharp
member this.PrintNames(names : string list) =
    ...
```

<span data-ttu-id="16c3e-424">Use sequências de F #:</span><span class="sxs-lookup"><span data-stu-id="16c3e-424">Use F# sequences:</span></span>

```fsharp
member this.PrintNames(names : seq<string>) =
    ...
```

#### <a name="use-the-unit-type-as-the-only-input-type-of-a-method-to-define-a-zero-argument-method-or-as-the-only-return-type-to-define-a-void-returning-method"></a><span data-ttu-id="16c3e-425">Use o tipo de unidade como o único tipo de entrada de um método para definir um método de argumento de zero ou como o único tipo para definir um método de retorno de void de retorno</span><span class="sxs-lookup"><span data-stu-id="16c3e-425">Use the unit type as the only input type of a method to define a zero-argument method, or as the only return type to define a void-returning method</span></span>

<span data-ttu-id="16c3e-426">Evite a outros usos do tipo de unidade.</span><span class="sxs-lookup"><span data-stu-id="16c3e-426">Avoid other uses of the unit type.</span></span> <span data-ttu-id="16c3e-427">Essas são boas:</span><span class="sxs-lookup"><span data-stu-id="16c3e-427">These are good:</span></span>

```fsharp
✔ member this.NoArguments() = 3

✔ member this.ReturnVoid(x : int) = ()
```

<span data-ttu-id="16c3e-428">Isso é inválido:</span><span class="sxs-lookup"><span data-stu-id="16c3e-428">This is bad:</span></span>

```fsharp
member this.WrongUnit( x:unit, z:int) = ((), ())
```

#### <a name="check-for-null-values-on-vanilla-net-api-boundaries"></a><span data-ttu-id="16c3e-429">Verificar valores nulos em limites de API .NET baunilha</span><span class="sxs-lookup"><span data-stu-id="16c3e-429">Check for null values on vanilla .NET API boundaries</span></span>

<span data-ttu-id="16c3e-430">Código de implementação do F # tende a ter menos valores nulos, devido a restrições no uso de literais nulas para tipos F # e padrões de design imutável.</span><span class="sxs-lookup"><span data-stu-id="16c3e-430">F# implementation code tends to have fewer null values, due to immutable design patterns and restrictions on use of null literals for F# types.</span></span> <span data-ttu-id="16c3e-431">Outras linguagens .NET geralmente usam nulo como um valor muito mais frequentemente.</span><span class="sxs-lookup"><span data-stu-id="16c3e-431">Other .NET languages often use null as a value much more frequently.</span></span> <span data-ttu-id="16c3e-432">Por isso, código F #, que é expor uma API .NET baunilha deve verificar parâmetros de null no limite da API e impedir que esses valores que fluem mais profundo para o código de implementação do F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-432">Because of this, F# code that is exposing a vanilla .NET API should check parameters for null at the API boundary, and prevent these values from flowing deeper into the F# implementation code.</span></span> <span data-ttu-id="16c3e-433">O `isNull` função ou padrões coincidentes no `null` padrão pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="16c3e-433">The `isNull` function or pattern matching on the `null` pattern can be used.</span></span>

```fsharp
let checkNonNull argName (arg: obj) =
    match arg with
    | null -> nullArg argName
    | _ -> ()

let checkNonNull` argName (arg: obj) =
    if isNull arg then nullArg argName
    else ()
```

#### <a name="avoid-using-tuples-as-return-values"></a><span data-ttu-id="16c3e-434">Evite usar tuplas como valores de retorno</span><span class="sxs-lookup"><span data-stu-id="16c3e-434">Avoid using tuples as return values</span></span>

<span data-ttu-id="16c3e-435">Em vez disso, preferir retornando um tipo nomeado, mantendo os dados de agregação, ou usando os parâmetros de saída para retornar vários valores.</span><span class="sxs-lookup"><span data-stu-id="16c3e-435">Instead, prefer returning a named type holding the aggregate data, or using out parameters to return multiple values.</span></span> <span data-ttu-id="16c3e-436">Embora tuplas e struct tuplas existam no .NET (incluindo suporte a linguagem c# para tuplas de struct), eles geralmente não fornecerá a API ideal e esperada para desenvolvedores do .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-436">Although tuples and struct tuples exist in .NET (including C# language support for struct tuples), they will most often not provide the ideal and expected API for .NET developers.</span></span>

#### <a name="avoid-the-use-of-currying-of-parameters"></a><span data-ttu-id="16c3e-437">Evite o uso de currying de parâmetros</span><span class="sxs-lookup"><span data-stu-id="16c3e-437">Avoid the use of currying of parameters</span></span>

<span data-ttu-id="16c3e-438">Em vez disso, use o .NET convenções de chamada ``Method(arg1,arg2,…,argN)``.</span><span class="sxs-lookup"><span data-stu-id="16c3e-438">Instead, use .NET calling conventions ``Method(arg1,arg2,…,argN)``.</span></span>

```fsharp
member this.TupledArguments(str, num) = String.replicate num str
```

<span data-ttu-id="16c3e-439">Dica: Se você estiver criando bibliotecas para uso em qualquer linguagem .NET, em seguida, há nenhum substituto para realmente fazer algumas experimental c# e Visual Basic de programação para garantir que suas bibliotecas "funcionalidade à direita" desses idiomas.</span><span class="sxs-lookup"><span data-stu-id="16c3e-439">Tip: If you’re designing libraries for use from any .NET language, then there’s no substitute for actually doing some experimental C# and Visual Basic programming to ensure that your libraries "feel right" from these languages.</span></span> <span data-ttu-id="16c3e-440">Você também pode usar ferramentas como o .NET Reflector e o Pesquisador de objeto do Visual Studio para garantir que os documentos e bibliotecas aparecem conforme o esperado para os desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="16c3e-440">You can also use tools such as .NET Reflector and the Visual Studio Object Browser to ensure that libraries and their documentation appear as expected to developers.</span></span>

## <a name="appendix"></a><span data-ttu-id="16c3e-441">Anexo</span><span class="sxs-lookup"><span data-stu-id="16c3e-441">Appendix</span></span>

### <a name="end-to-end-example-of-designing-f-code-for-use-by-other-net-languages"></a><span data-ttu-id="16c3e-442">Exemplo de ponta a ponta da criação de código F # para uso por outras linguagens .NET</span><span class="sxs-lookup"><span data-stu-id="16c3e-442">End-to-end example of designing F# code for use by other .NET languages</span></span>

<span data-ttu-id="16c3e-443">Considere a seguinte classe:</span><span class="sxs-lookup"><span data-stu-id="16c3e-443">Consider the following class:</span></span>

```fsharp
open System

type Point1(angle,radius) =
    new() = Point1(angle=0.0, radius=0.0)
    member x.Angle = angle
    member x.Radius = radius
    member x.Stretch(l) = Point1(angle=x.Angle, radius=x.Radius * l)
    member x.Warp(f) = Point1(angle=f(x.Angle), radius=x.Radius)
    static member Circle(n) =
        [ for i in 1..n -> Point1(angle=2.0*Math.PI/float(n), radius=1.0) ]
```

<span data-ttu-id="16c3e-444">O tipo F # deduzido dessa classe é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="16c3e-444">The inferred F# type of this class is as follows:</span></span>

```fsharp
type Point1 =
    new : unit -> Point1
    new : angle:double * radius:double -> Point1
    static member Circle : n:int -> Point1 list
    member Stretch : l:double -> Point1
    member Warp : f:(double -> double) -> Point1
    member Angle : double
    member Radius : double
```

<span data-ttu-id="16c3e-445">Vamos dar uma olhada em como esse tipo de F # é exibido para um programador usando outra linguagem .NET.</span><span class="sxs-lookup"><span data-stu-id="16c3e-445">Let’s take a look at how this F# type appears to a programmer using another .NET language.</span></span> <span data-ttu-id="16c3e-446">Por exemplo, aproximado c# "assinatura" é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="16c3e-446">For example, the approximate C# “signature” is as follows:</span></span>

```csharp
// C# signature for the unadjusted Point1 class
public class Point1
{
    public Point1();

    public Point1(double angle, double radius);

    public static Microsoft.FSharp.Collections.List<Point1> Circle(int count);

    public Point1 Stretch(double factor);

    public Point1 Warp(Microsoft.FSharp.Core.FastFunc<double,double> transform);

    public double Angle { get; }

    public double Radius { get; }
}
```

<span data-ttu-id="16c3e-447">Há alguns pontos importantes a serem observados sobre como F # representa construções aqui.</span><span class="sxs-lookup"><span data-stu-id="16c3e-447">There are some important points to notice about how F# represents constructs here.</span></span> <span data-ttu-id="16c3e-448">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="16c3e-448">For example:</span></span>

* <span data-ttu-id="16c3e-449">Metadados, como nomes de argumento foi preservado.</span><span class="sxs-lookup"><span data-stu-id="16c3e-449">Metadata such as argument names has been preserved.</span></span>

* <span data-ttu-id="16c3e-450">F # métodos que usam dois argumentos se tornar c# métodos que usam dois argumentos.</span><span class="sxs-lookup"><span data-stu-id="16c3e-450">F# methods that take two arguments become C# methods that take two arguments.</span></span>

* <span data-ttu-id="16c3e-451">Funções e listas se tornam as referências aos tipos correspondentes na biblioteca F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-451">Functions and lists become references to corresponding types in the F# library.</span></span>

<span data-ttu-id="16c3e-452">O código a seguir mostra como ajustar esse código para fazer essas coisas em conta.</span><span class="sxs-lookup"><span data-stu-id="16c3e-452">The following code shows how to adjust this code to take these things into account.</span></span>

```fsharp
namespace SuperDuperFSharpLibrary.Types

type RadialPoint(angle:double, radius:double) =

    /// Return a point at the origin
    new() = RadialPoint(angle=0.0, radius=0.0)

    /// The angle to the point, from the x-axis
    member x.Angle = angle

    /// The distance to the point, from the origin
    member x.Radius = radius

    /// Return a new point, with radius multiplied by the given factor
    member x.Stretch(factor) =
        RadialPoint(angle=angle, radius=radius * factor)

    /// Return a new point, with angle transformed by the function
    member x.Warp(transform:Func<_,_>) =
        RadialPoint(angle=transform.Invoke angle, radius=radius)

    /// Return a sequence of points describing an approximate circle using
    /// the given count of points
    static member Circle(count) =
        seq { for i in 1..count ->
                RadialPoint(angle=2.0*Math.PI/float(count), radius=1.0) }
```

<span data-ttu-id="16c3e-453">O tipo F # inferido do código é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="16c3e-453">The inferred F# type of the code is as follows:</span></span>

```fsharp
type RadialPoint =
    new : unit -> RadialPoint
    new : angle:double * radius:double -> RadialPoint
    static member Circle : count:int -> seq<RadialPoint>
    member Stretch : factor:double -> RadialPoint
    member Warp : transform:System.Func<double,double> -> RadialPoint
    member Angle : double
    member Radius : double
```

<span data-ttu-id="16c3e-454">A assinatura c# agora é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="16c3e-454">The C# signature is now as follows:</span></span>

```csharp
public class RadialPoint
{
    public RadialPoint();

    public RadialPoint(double angle, double radius);

    public static System.Collections.Generic.IEnumerable<RadialPoint> Circle(int count);

    public RadialPoint Stretch(double factor);

    public RadialPoint Warp(System.Func<double,double> transform);

    public double Angle { get; }

    public double Radius { get; }
}
```

<span data-ttu-id="16c3e-455">As correções feitas preparar esse tipo para uso como parte de uma biblioteca .NET baunilha são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="16c3e-455">The fixes made to prepare this type for use as part of a vanilla .NET library are as follows:</span></span>

* <span data-ttu-id="16c3e-456">Ajustado vários nomes: `Point1`, `n`, `l`, e `f` tornou-se `RadialPoint`, `count`, `factor`, e `transform`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="16c3e-456">Adjusted several names: `Point1`, `n`, `l`, and `f` became `RadialPoint`, `count`, `factor`, and `transform`, respectively.</span></span>

* <span data-ttu-id="16c3e-457">Usado um tipo de retorno `seq<RadialPoint>` em vez de `RadialPoint list` alterando uma construção de lista usando `[ ... ]` para uma construção de sequência usando `IEnumerable<RadialPoint>`.</span><span class="sxs-lookup"><span data-stu-id="16c3e-457">Used a return type of `seq<RadialPoint>` instead of `RadialPoint list` by changing a list construction using `[ ... ]` to a sequence construction using `IEnumerable<RadialPoint>`.</span></span>

* <span data-ttu-id="16c3e-458">Usar o tipo de delegado .NET `System.Func` em vez de um tipo de função do F #.</span><span class="sxs-lookup"><span data-stu-id="16c3e-458">Used the .NET delegate type `System.Func` instead of an F# function type.</span></span>

<span data-ttu-id="16c3e-459">Isso facilita muito melhor consumir o código c#.</span><span class="sxs-lookup"><span data-stu-id="16c3e-459">This makes it far nicer to consume in C# code.</span></span>