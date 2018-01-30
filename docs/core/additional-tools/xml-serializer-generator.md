---
title: Usando o Microsoft XML Serializer Generator no .NET Core
description: "Uma visão geral sobre o Microsoft XML Serializer Generator."
author: mlacouture
manager: wpickett
ms.author: johalex
ms.date: 01/19/2017
ms.topic: tutorial
ms.prod: .net-core
ms.custom: mvc
ms.openlocfilehash: b2f52a068d128b2eb978c9e086508bd87e103ebc
ms.sourcegitcommit: dd6ea7f0e581ac84e0a90d9b23c463fcf1ec3ce7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="using-microsoft-xml-serializer-generator-on-net-core"></a>Usando o Microsoft XML Serializer Generator no .NET Core

Este tutorial ensina como usar o Microsoft XML Serializer Generator em um aplicativo do .NET Core em C#. Durante este tutorial, você aprenderá:

> [!div class="checklist"]
> * Como criar um aplicativo do .NET Core
> * Como adicionar uma referência ao pacote Microsoft.XmlSerializer.Generator
> * Como editar o MyApp.csproj para adicionar dependências
> * Como adicionar uma classe e um XmlSerializer
> * Como compilar e executar o aplicativo 

Como o [XML Serializer Generator (sgen.exe)](../../standard/serialization/xml-serializer-generator-tool-sgen-exe.md) para o .NET Framework, o [pacote NuGet Microsoft.XmlSerializer.Generator](https://www.nuget.org/packages/Microsoft.XmlSerializer.Generator) é o equivalente para projetos do .NET Core e .NET Standard. Ele cria um assembly de serialização de XML para tipos contidos em um assembly a fim de melhorar o desempenho de inicialização da serialização de XML ao serializar ou desserializar objetos desses tipos usando <xref:System.Xml.Serialization.XmlSerializer>.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este tutorial:

* Instale o [SDK do .NET Core 2.1.3 ou posterior](https://www.microsoft.com/net/download)
* Instale seu editor de código favorito, caso ainda não tenha um.

> [!TIP]
> Precisa instalar um editor de código? Experimente o [Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)!
  
## <a name="use-microsoft-xml-serializer-generator-in-a-net-core-console-application"></a>Usar o Microsoft XML Serializer Generator em um aplicativo de console do .NET Core 

As instruções a seguir mostram como usar o XML Serializer Generator em um aplicativo de console do .NET Core.

### <a name="create-a-net-core-console-application"></a>Criar um aplicativo de console do .NET Core

Abra um prompt de comando e crie uma pasta chamada *MyApp*. Navegue até a pasta criada e digite o seguinte comando:

```console
dotnet new console
```

### <a name="add-a-reference-to-the-microsoftxmlserializergenerator-package-in-the-myapp-project"></a>Adicionar uma referência ao pacote Microsoft.XmlSerializer.Generator no projeto MyApp

Use o comando [`dotnet add package`](../tools//dotnet-add-package.md) para adicionar a referência em seu projeto. 

Tipo:
 
 ```console
 dotnet add package Microsoft.XmlSerializer.Generator -v 1.0.0
 ```
 
### <a name="verify-changes-to-myappcsproj-after-adding-the-package"></a>Verificar alterações ao MyApp.csproj depois de adicionar o pacote

Abra o editor de código e vamos começar! Ainda estamos trabalhando no diretório *MyApp* no qual criamos o aplicativo.

Abra o *MyApp.csproj* em seu editor de texto.

Depois de executar o comando [`dotnet add package`](../tools//dotnet-add-package.md), as seguintes linhas são adicionadas ao seu arquivo de projeto *MyApp.csproj*:

 ```xml
 <ItemGroup>
    <PackageReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```
 
### <a name="add-another-itemgroup-section-for-net-core-cli-tool-support"></a>Adicionar outra seção ItemGroup para compatibilidade com a ferramenta de CLI do .NET Core
 
 Adicione as seguintes linhas depois da seção `ItemGroup` que inspecionamos:
 
 ```xml
 <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```
 
### <a name="add-a-class-in-the-application"></a>Adicionar uma classe no aplicativo

Abra o *Program.cs* em seu editor de texto. Adicionar a classe denominada *MyClass* no *Program.cs*.

```csharp
public class MyClass
{
   public int Value;
}
```

### <a name="create-an-xmlserializer-for-myclass"></a>Criar um `XmlSerializer` para MyClass

Adicione a seguinte linha dentro de *Main* para criar um `XmlSerializer` para MyClass:

```csharp
var serializer = new System.Xml.Serialization.XmlSerializer(typeof(MyClass));
```

### <a name="build-and-run-the-application"></a>Compilar e executar o aplicativo

Ainda dentro da pasta *MyApp*, execute o aplicativo por meio do comando [`dotnet run`](../tools/dotnet-run.md) e ele carregará e usará automaticamente os serializadores pré-gerados em tempo de execução.

Digite o seguinte comando na janela do console:

 ```console
 $ dotnet run
 ```
> [!NOTE]
> [`dotnet run`](../tools/dotnet-run.md) chama [`dotnet build`](../tools/dotnet-build.md) para garantir que os destinos de build foram criados e então chama `dotnet <assembly.dll>` para executar o aplicativo de destino.

> [!IMPORTANT]
> Os comandos e as etapas mostradas neste tutorial para executar o aplicativo são usadas somente durante o tempo de desenvolvimento. Quando estiver pronto para implantar o aplicativo, dê uma olhada nas diferentes [estratégias de implantação](../deploying/index.md) para aplicativos do .NET Core e no comando [`dotnet publish`](../tools/dotnet-publish.md).

Se tudo for bem-sucedido, um assembly chamado *MyApp.XmlSerializers.dll* será gerado na pasta de saída. 



Parabéns! Você acabou de:
> [!div class="checklist"]
> * Criar um aplicativo do .NET Core.
> * Adicionar uma referência ao pacote Microsoft.XmlSerializer.Generator.
> * Editar o MyApp.csproj para adicionar dependências.
> * Adicionar uma classe e um XmlSerializer.
> * Compilar e executar o aplicativo. 

## <a name="related-resources"></a>Recursos relacionados

* [Apresentando a serialização XML](../../standard/serialization/introducing-xml-serialization.md)
* [Como serializar usando XmlSerializer (C#)](../../csharp/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)
* [Como serializar usando XmlSerializer (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)