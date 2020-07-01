---
title: 実行中の ASP.NET プロセスを見つける | Microsoft Docs
ms.date: 11/04/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- ASP.NET debugging, ASP.NET process
- ASP.NET process
ms.assetid: 931a7597-b0f0-4a28-931d-46e63344435f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: c14067d58289dd0b41fa526937a0553c10934ea7
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349608"
---
# <a name="find-the-name-of-the-aspnet-process"></a>ASP.NET プロセスの名前を見つける

実行中の [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] アプリをデバッグするには、Visual Studio デバッガーを [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] プロセスに名前を指定してアタッチする必要があります。

**ASP.NET アプリを実行しているプロセスを見つけるには:**

1. アプリが実行されている状態で、Visual Studio で **[デバッグ]**  >  **[プロセスにアタッチ]** を選択します。

1. **[プロセスにアタッチ]** ダイアログで、次の一覧からプロセス名の最初の文字を入力するか、検索ボックスに入力します。 実行されているのは、ASP.NET アプリを実行しているものです。 そのプロセスにアタッチしてアプリをデバッグします。

    - *w3wp.exe* は IIS 6.0 以降です。
    - *aspnet_wp.exe* は IIS の以前のバージョンです。
    - *iisexpress.exe* は IISExpress です。
    - *dotnet.exe* は ASP.NET Core です。
    - *inetinfo.exe* は、インプロセスで実行されている以前の ASP アプリケーションです。

>[!NOTE]
>Visual Studio 2012 以前の [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] コードはファイル システム上にあり、テスト サーバー *WebDev.WebServer.exe* または *WebDev.WebServer40.exe* 上で実行できます。 この例のようにローカル デバッグの場合は、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] プロセスではなく *WebDev.WebServer.exe* または *WebDev.WebServer40.exe* にアタッチします。

**関連項目:**

- [実行中のプロセスにアタッチする](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [Web アプリケーションをリモート デバッグするための前提条件](remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)
- [システム要件](../debugger/aspnet-debugging-system-requirements.md)
- [ASP.NET アプリケーションをデバッグする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)