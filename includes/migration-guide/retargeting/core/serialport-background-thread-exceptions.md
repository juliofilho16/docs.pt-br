### <a name="serialport-background-thread-exceptions"></a><span data-ttu-id="d8cae-101">Exceções de thread de tela de fundo de SerialPort</span><span class="sxs-lookup"><span data-stu-id="d8cae-101">SerialPort background thread exceptions</span></span>

|   |   |
|---|---|
|<span data-ttu-id="d8cae-102">Detalhes</span><span class="sxs-lookup"><span data-stu-id="d8cae-102">Details</span></span>|<span data-ttu-id="d8cae-103">Threads criados com fluxos <xref:System.IO.Ports.SerialPort> em segundo plano não terminam mais o processo quando exceções de sistema operacional são lançadas. Em aplicativos destinados ao .NET Framework 4.7 e a versões anteriores, um processo é terminado quando uma exceção do sistema operacional é gerada em um thread de segundo plano criado com um fluxo <xref:System.IO.Ports.SerialPort>. Em aplicativos destinados ao .NET Framework 4.7.1 ou a uma versão posterior, threads em segundo plano esperam eventos do sistema operacional relacionadas à porta serial ativa e podem falhar em alguns casos, como no caso de remoção repentina da porta serial.</span><span class="sxs-lookup"><span data-stu-id="d8cae-103">Background threads created with <xref:System.IO.Ports.SerialPort> streams no longer terminate the process when OS exceptions are thrown.In applications that target the .NET Framework 4.7 and earlier versions, a process is terminated when an operating system exception is thrown on a background thread created with a <xref:System.IO.Ports.SerialPort> stream.In applications that target the .NET Framework 4.7.1 or a later version, background threads wait for OS events related to the active serial port and could crash in some cases, such as sudden removal of the serial port.</span></span>|
|<span data-ttu-id="d8cae-104">Sugestão</span><span class="sxs-lookup"><span data-stu-id="d8cae-104">Suggestion</span></span>|<span data-ttu-id="d8cae-105">Para aplicativos destinados ao .NET Framework 4.7.1, será possível recusar a manipulação de exceções se ela não for desejável adicionando o seguinte à seção <code>&lt;runtime&gt;</code> do arquivo <code>app.config</code>:</span><span class="sxs-lookup"><span data-stu-id="d8cae-105">For apps that target the .NET Framework 4.7.1, you can opt out of the exception handling if it is not desirable by adding the following to the <code>&lt;runtime&gt;</code> section of your <code>app.config</code> file:</span></span><pre><code class="language-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.Ports.DoNotCatchSerialStreamThreadExceptions=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre><span data-ttu-id="d8cae-106">Para aplicativos destinados a versões anteriores do .NET Framework mas executados no .NET Framework 4.7.1 ou posterior, é possível aceitar a manipulação de exceções adicionando o seguinte à seção <code>&lt;runtime&gt;</code> do arquivo <code>app.config</code>:</span><span class="sxs-lookup"><span data-stu-id="d8cae-106">For apps that target earlier versions of the .NET Framework but run on the .NET Framework 4.7.1 or later, you can opt in to the exception handling by adding the following to the <code>&lt;runtime&gt;</code> section of your <code>app.config</code> file:</span></span><pre><code class="language-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.Ports.DoNotCatchSerialStreamThreadExceptions=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|<span data-ttu-id="d8cae-107">Escopo</span><span class="sxs-lookup"><span data-stu-id="d8cae-107">Scope</span></span>|<span data-ttu-id="d8cae-108">Secundário</span><span class="sxs-lookup"><span data-stu-id="d8cae-108">Minor</span></span>|
|<span data-ttu-id="d8cae-109">Versão</span><span class="sxs-lookup"><span data-stu-id="d8cae-109">Version</span></span>|<span data-ttu-id="d8cae-110">4.7.1</span><span class="sxs-lookup"><span data-stu-id="d8cae-110">4.7.1</span></span>|
|<span data-ttu-id="d8cae-111">Tipo</span><span class="sxs-lookup"><span data-stu-id="d8cae-111">Type</span></span>|<span data-ttu-id="d8cae-112">Redirecionando</span><span class="sxs-lookup"><span data-stu-id="d8cae-112">Retargeting</span></span>|
|<span data-ttu-id="d8cae-113">APIs afetadas</span><span class="sxs-lookup"><span data-stu-id="d8cae-113">Affected APIs</span></span>|<ul><li><xref:System.IO.Ports.SerialPort?displayProperty=nameWithType></li></ul>|
