---
title: 'デバッグの準備: ASP.NET Web Applications |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
helpviewer_keywords:
- debugging ASP.NET Web applications
- debugging [Visual Studio], Web applications
ms.assetid: bcfb1080-98d1-42f9-96af-186fb14f232a
caps.latest.revision: 38
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7a80587062442688551d07128a2cec49a712adf6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691459"
---
# <a name="debugging-preparation-aspnet-web-applications"></a>デバッグの準備 : ASP.NET Web アプリケーション
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] サイトテンプレートは、Web フォームアプリケーションを作成します。 このテンプレートを使用して Web サイトを作成する場合、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] はデバッグ用に既定の設定を作成します。 [ **プロジェクトのプロパティ** ] ダイアログボックスで、Web ページをスタートアップページにするかどうかを指定できます。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]これらの既定の設定で Web サイトのデバッグを開始すると、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は Internet Explorer を起動し、デバッガーを [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカープロセス (aspnet_wp.exe または w3wp.exe) にアタッチします。 詳細については、「 [System Requirements](../debugger/aspnet-debugging-system-requirements.md)」をご覧ください。  
  
### <a name="to-create-a-web-forms-application"></a>Web フォーム アプリケーションを作成するには  
  
1. [ **ファイル** ] メニューの [ **新しい Web サイト**] をクリックします。  
  
2. [**新しい Web サイト**] ダイアログボックスで、[ [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] **web サイト**] を選択します。  
  
3. **[OK]** をクリックします。  
  
### <a name="to-debug-your-web-form"></a>Web フォームをデバッグするには  
  
1. 関数とイベント ハンドラーに 1 つ以上のブレークポイントを設定します。  
  
     詳細については、「 [Breakpoints and Tracepoints](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583)」を参照してください。  
  
2. ブレークポイントに達したら、関数内のコードをステップ実行します。 問題が特定されるまでコードの実行を確認します。  
  
     詳細については、「 [Web アプリケーションとスクリプト](../debugger/debugging-web-applications-and-script.md)の[ステップ](https://msdn.microsoft.com/8791dac9-64d1-4bb9-b59e-8d59af1833f9)実行とデバッグ」を参照してください。  
  
## <a name="changing-default-configurations"></a>既定の構成の変更  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で作成された既定のデバッグ構成とリリース構成を変更する必要がある場合は、構成を変更できます。 詳細については、[デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)」を参照してください。  
  
#### <a name="to-change-the-default-debug-configuration"></a>既定のデバッグ構成を変更するには  
  
1. **ソリューションエクスプローラー**で、Web サイトを右クリックし、[**プロパティページ**] をクリックして [**プロパティページ**] ダイアログボックスを開きます。  
  
2. [ **開始オプション**] をクリックします。  
  
3. 最初に表示する Web ページに [ **開始アクション** ] を設定します。  
  
4. [ **デバッガー**] の下で、 **ASP.NET デバッグ** が選択されていることを確認します。  
  
     詳細については、「 [Web プロジェクトのプロパティページの設定](../debugger/property-pages-settings-for-web-projects.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)   
 [デバッガーの基本](../debugger/debugger-basics.md)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
