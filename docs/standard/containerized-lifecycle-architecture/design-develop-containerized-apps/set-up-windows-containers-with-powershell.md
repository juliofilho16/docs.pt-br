---
title: Usando comandos do Windows PowerShell em um DockerFile para configurar a contêineres do Windows (Docker padrão com base)
description: Containerized Docker Application Lifecycle with Microsoft Platform and Tools (Ciclo de vida de aplicativo do Docker em contêineres com a plataforma e as ferramentas da Microsoft)
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/19/2017
ms.openlocfilehash: 48af11117ec8eb0034d9557a332b89d3418d4b31
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="using-windows-powershell-commands-in-a-dockerfile-to-set-up-windows-containers-docker-standard-based"></a>Usando comandos do Windows PowerShell em um DockerFile para configurar a contêineres do Windows (Docker padrão com base)

Com [contêineres do Windows](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/about/about_overview), você pode converter seus aplicativos existentes do Windows para imagens do Docker e implantá-los com as mesmas ferramentas que o resto do ecossistema do Docker.

Para usar contêineres do Windows, você apenas precisa gravar comandos do Windows PowerShell no DockerFile, conforme demonstrado no exemplo a seguir:

```
FROM microsoft/windowsservercore
LABEL Description="IIS" Vendor="Microsoft" Version="10"
RUN powershell -Command Add-WindowsFeature Web-Server
CMD [ "ping", "localhost", "-t" ]
```

Nesse caso, estamos usando o Windows PowerShell para instalar uma imagem base do Windows Server Core, bem como o IIS.

De maneira semelhante, você também pode usar comandos do Windows PowerShell para configurar componentes adicionais como o tradicional ASP.NET 4. x e o .NET 4.6 ou qualquer outro software do Windows, como mostrado aqui:

```
RUN powershell add-windowsfeature web-asp-net45
```

>[!div class="step-by-step"]
[Anterior] (visual-studio-ferramentas-para-docker.md) [Avançar] (... /docker-DevOps-Workflow/index.MD)
