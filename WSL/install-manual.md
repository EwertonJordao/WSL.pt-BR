---
title: Baixar manualmente as distribuições do WSL (Subsistema do Windows para Linux)
description: Instruções sobre como baixar manualmente as distribuições do Subsistema do Windows para Linux.
keywords: wsl, subsistema do Windows para Linux, instalação manual, instalar manualmente, microsoft store, windows 10s, ondulação, Add-AppxPackage, manutenção de longo prazo, LTSC
ms.date: 05/28/2020
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 621b2619d6c62e0b6c4e53f7791fc587c1c8f878
ms.sourcegitcommit: 09f5eb0f6062642e5c86deb1f34307ce3429163a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84211712"
---
# <a name="manually-download-windows-subsystem-for-linux-distro-packages"></a>Baixar manualmente os pacotes de distribuição do Subsistema do Windows para Linux

Há vários cenários nos quais você pode não conseguir (ou desejar) instalar as distribuições do WSL para Linux por meio da Microsoft Store. Especificamente, você pode estar executando um SKU do sistema operacional da área de trabalho do Windows Server ou de LTSC (Manutenção em Longo Prazo) que não é compatível com a Microsoft Store ou suas políticas de rede corporativa e/ou administradores não permitem o uso da Microsoft Store em seu ambiente.

Nesses casos, embora o WSL em si esteja disponível, como baixar e instalar as distribuições do Linux no WSL se você não puder acessar a loja?

> Observação: **ambientes de Shell de linha de comando, incluindo distribuições de Cmd, PowerShell e Linux/WSL, não têm permissão para serem executados no Windows 10 no modo S**. Essa restrição existe para garantir a integridade e as metas de segurança que o modo S fornece: Para obter mais informações, leia [esta postagem](https://blogs.msdn.microsoft.com/commandline/2017/05/18/will-linux-distros-run-on-windows-10-s/).

## <a name="downloading-distros"></a>Como baixar as distribuições

Se o aplicativo Microsoft Store não estiver disponível, você poderá baixar e instalar manualmente as distribuições do Linux clicando nestes links:
* [Ubuntu 18.04](https://aka.ms/wsl-ubuntu-1804)
* [Ubuntu 18.04 ARM](https://aka.ms/wsl-ubuntu-1804-arm)
* [Ubuntu 16.04](https://aka.ms/wsl-ubuntu-1604)
* [Debian GNU/Linux](https://aka.ms/wsl-debian-gnulinux)
* [Kali Linux](https://aka.ms/wsl-kali-linux-new)
* [OpenSUSE Leap 42](https://aka.ms/wsl-opensuse-42)
* [SUSE Linux Enterprise Server 12](https://aka.ms/wsl-sles-12)
* [Fedora Remix para WSL](https://github.com/WhitewaterFoundry/WSLFedoraRemix/releases/)

Isso fará com que os pacotes `<distro>.appx` sejam baixados em uma pasta de sua escolha. Siga as [instruções de instalação](#installing-your-distro) para instalar suas distribuições baixadas.

## <a name="downloading-distros-via-the-command-line"></a>Baixar as distribuições usando a linha de comando
Se preferir, você também poderá baixar suas distribuições preferenciais usando a linha de comando:

 ### <a name="download-using-powershell"></a>Baixar usando o PowerShell
 Para baixar as distribuições usando o PowerShell, use o cmdlet [Invoke-WebRequest](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-5.1). Aqui está um exemplo de instrução para baixar o Ubuntu 16.04.

```powershell
Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1604 -OutFile Ubuntu.appx -UseBasicParsing
```

> [!TIP]
> Se o download estiver demorando muito, desligue a barra de progresso definindo `$ProgressPreference = 'SilentlyContinue'`

### <a name="download-using-curl"></a>Baixar usando curl
A atualização do Windows 10 Spring 2018 (ou posterior) inclui o popular [utilitário de linha de comando curl](https://curl.haxx.se/) com o qual você pode invocar solicitações da Web (ou seja, comandos HTTP GET, POST, PUT etc.) na linha de comando. Você pode usar `curl.exe` para baixar as distribuições acima:

```console
curl.exe -L -o ubuntu-1604.appx https://aka.ms/wsl-ubuntu-1604
```

No exemplo acima, `curl.exe` é executado (não apenas `curl`) para verificar se, no PowerShell, o executável curl real é invocado, não o alias curl do PowerShell para [Invoke-WebRequest](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-6)

> Observação: usar `curl` poderá ser preferível se você precisar invocar/gerar script de etapas de download usando o shell Cmd e/ou scripts `.bat` / `.cmd`.

## <a name="installing-your-distro"></a>Instalar sua distribuição
Se você estiver usando o Windows 10, poderá instalar a distribuição com o PowerShell. Basta navegar até a pasta que contém a distribuição baixada acima e, nesse diretório, executar o comando a seguir, em que `app_name` é o nome do seu arquivo de distribuição .appx.  
```Powershell
Add-AppxPackage .\app_name.appx
```

Se você estiver usando um servidor do Windows, poderá encontrar as instruções de instalação na página de documentação do [Windows Server](install-on-server.md).

Após instalar sua distribuição, siga as instruções normais para [atualizar para WSL 2](./install-win10.md#update-to-wsl-2) ou [criar uma conta e senha de usuário](./user-support.md).
