---
title: '方法: ASP.NET ベースのワークフローをデバッグする (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- ASP.NET, debugging workflows
- debugging workflows, ASP.NET workflows
- ASP.NET workflows, debugging
- debugging, ASP.NET workflows
ms.assetid: 79b21edc-9e7d-410d-af68-09c1598b9c30
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f3bed38f5229cb489f663878759517480b48302c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72668665"
---
# <a name="how-to-debug-aspnet-based-workflows-legacy"></a>方法: ASP.NET ベースのワークフローをデバッグする (レガシ)
このトピックでは、従来の [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]で、[!INCLUDE[wf](../includes/wf-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] ベースの [!INCLUDE[wfd1](../includes/wfd1-md.md)] アプリケーションをデバッグする方法について説明します。

 ワークフローをそのホストとなるプロセスにアタッチすることにより、ASP.NET で開始される従来のワークフロー、または Web サービスとして公開される従来のワークフローをデバッグすることができます。

### <a name="to-debug-an-aspnet-based-workflow"></a>ASP.NET ベースのワークフローをデバッグするには

1. web.config ファイルで **debug = true** を設定して、ASP.NET アプリケーションのデバッグを有効にします。

2. ワークフロー ライブラリをスタートアップ プロジェクトとして設定し、ワークフローのブレークポイントを設定します。

3. ワークフロープロジェクトのプロパティの [ **デバッグ** ] オプションの [ **外部 url でブラウザーを開始** ] ボックスに、既定の Web ページの URL を入力します。

4. [**デバッグ**] メニューの [**プロセスにアタッチ**] をクリックします。

5. [選択 **可能なプロセス** ] ボックスの一覧から、アタッチ先のプロセスを選択します。

     ワークフローのホストとなる w3wp.exe、webdev.webserver、または aspnet_wp プロセスにアタッチします。

6. [**アタッチ先**] テキストボックスの横にある [**選択**] をクリックします。

     **[コードの種類の選択**] ダイアログボックスが表示されます。

7. [ **次のコードの種類をデバッグ** する] を選択し、[ **ワークフロー**] を選択します。

8. **[OK]** をクリックします。

9. **[アタッチ]** をクリックします。

10. ブラウザで既定の Web ページを開いて、ワークフローを開始します。

## <a name="see-also"></a>参照
 [Windows Workflow Foundation のための Visual Studio デバッガーの呼び出し (レガシ)](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md) [方法: ワークフローにブレークポイントを設定する (レガシ)](../workflow-designer/how-to-set-breakpoints-in-workflows-legacy.md) [従来のワークフローのデバッグ](../workflow-designer/debugging-legacy-workflows.md)