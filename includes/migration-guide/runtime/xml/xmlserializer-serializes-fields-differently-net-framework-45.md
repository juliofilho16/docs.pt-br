### <a name="xmlserializer-serializes-fields-differently-in-net-framework-45"></a><span data-ttu-id="f885a-101">O XmlSerializer serializa campos de modo diferente no .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="f885a-101">XmlSerializer serializes fields differently in .NET Framework 4.5</span></span>

|   |   |
|---|---|
|<span data-ttu-id="f885a-102">Detalhes</span><span class="sxs-lookup"><span data-stu-id="f885a-102">Details</span></span>|<span data-ttu-id="f885a-103">Alterações no <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> no .NET Framework 4.5 faziam campos serem formatados de modo diferente no XML serializado.</span><span class="sxs-lookup"><span data-stu-id="f885a-103">Changes in the <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> in .NET Framework 4.5 caused fields to be formatted differently in the serialized XML.</span></span>|
|<span data-ttu-id="f885a-104">Sugestão</span><span class="sxs-lookup"><span data-stu-id="f885a-104">Suggestion</span></span>|<span data-ttu-id="f885a-105">Esse comportamento foi corrigido em uma atualização de serviço do .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f885a-105">This behavior was corrected in a servicing update of .NET Framework 4.5.</span></span> <span data-ttu-id="f885a-106">Atualize o .NET Framework 4.5 ou faça upgrade para o .NET Framework 4.5.1 ou posterior para corrigir esse problema.</span><span class="sxs-lookup"><span data-stu-id="f885a-106">Please update the .NET Framework 4.5, or upgrade to .NET Framework 4.5.1 or later, to fix this issue.</span></span> <span data-ttu-id="f885a-107">Como alternativa, a seguinte configuração será revertida no comportamento <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> 4.0:</span><span class="sxs-lookup"><span data-stu-id="f885a-107">Alternatively, the following config setting will revert to 4.0 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> behavior:</span></span><pre><code>&lt;system.xml.serialization&gt;&#13;&#10;&lt;xmlSerializer useLegacySerializerGeneration=&quot;true&quot; /&gt;&#13;&#10;&lt;/system.xml.serialization&gt;&#13;&#10;</code></pre>|
|<span data-ttu-id="f885a-108">Escopo</span><span class="sxs-lookup"><span data-stu-id="f885a-108">Scope</span></span>|<span data-ttu-id="f885a-109">Principal</span><span class="sxs-lookup"><span data-stu-id="f885a-109">Major</span></span>|
|<span data-ttu-id="f885a-110">Versão</span><span class="sxs-lookup"><span data-stu-id="f885a-110">Version</span></span>|<span data-ttu-id="f885a-111">4.5</span><span class="sxs-lookup"><span data-stu-id="f885a-111">4.5</span></span>|
|<span data-ttu-id="f885a-112">Tipo</span><span class="sxs-lookup"><span data-stu-id="f885a-112">Type</span></span>|<span data-ttu-id="f885a-113">Tempo de execução</span><span class="sxs-lookup"><span data-stu-id="f885a-113">Runtime</span></span>|
|<span data-ttu-id="f885a-114">APIs afetadas</span><span class="sxs-lookup"><span data-stu-id="f885a-114">Affected APIs</span></span>|<ul><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.Stream%2CSystem.Object)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.TextWriter%2CSystem.Object)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Object%2CSystem.Xml.Serialization.XmlSerializationWriter)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter%2CSystem.Object)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.Stream%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.TextWriter%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces%2CSystem.String)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces%2CSystem.String%2CSystem.String)?displayProperty=nameWithType></li></ul>|
