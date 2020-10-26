---
title: '方法: ASP.NET Process の名前を検索する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ASP.NET debugging, ASP.NET process
- ASP.NET process
ms.assetid: 931a7597-b0f0-4a28-931d-46e63344435f
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 53072013c1665687262d30f4a0c2720641c920be
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685957"
---
# <a name="how-to-find-the-name-of-the-aspnet-process"></a>方法 : ASP.NET プロセスの名前を見つける
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

実行中の [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションにアタッチする場合、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] プロセスの名前を把握している必要があります。  
  
- IIS 6.0 または IIS 7.0 を実行している場合、プロセスの名前は w3wp.exe です。  
  
- 6.0 よりも前のバージョンの IIS を実行している場合、プロセスの名前は aspnet_wp.exe です。  
  
  以降のバージョンを使用してビルドされたアプリケーションの場合 [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)] 、 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] コードはファイルシステム上に存在し、テストサーバー WebDev.WebServer.exe で実行できます。 この場合、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] プロセスの代わりに WebDev.WebServer.exe にアタッチする必要があります。 ただし、これは、ローカル デバッグだけに当てはまります。  
  
  古いバージョンの ASP アプリケーションは、インプロセスで実行する場合、IIS プロセス inetinfo.exe 内で実行します。  
  
> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-determine-whether-project-code-resides-on-the-file-system-or-iis"></a>プロジェクト コードがファイル システムと IIS のどちらに存在するかを判断するには  
  
1. Visual Studio で **ソリューションエクスプローラー** を開きます (まだ開いていない場合)。  
  
2. アプリケーション名を含む最上位のノードを選択します。  
  
3. [ **プロパティ** ] ウィンドウのタイトルにファイルパスが含まれている場合、アプリケーションコードはファイルシステム上に存在します。  
  
     それ以外の場合は、[ **プロパティ** ] ウィンドウのタイトルに Web サイトの名前が表示されます。  
  
### <a name="to-determine-the-iis-version-under-which-the-application-is-running"></a>アプリケーションが実行されている IIS のバージョンを判断するには  
  
1. **管理ツール**を見つけて実行します。 オペレーティングシステムによっては、これは **コントロールパネル**内のアイコン、または [ **開始**] をクリックしたときに表示されるメニューエントリになることがあります。  
  
     Windows XP では、 **コントロールパネル** をカテゴリビューまたはクラシックビューにすることができます。 カテゴリビューでは、[ **クラシック表示に切り替える** ] または [ **パフォーマンスとメンテナンス** ] をクリックして、[ **管理ツール** ] アイコンを表示する必要があります。  
  
2. [ **管理ツール**] でインターネットインフォメーションサービスを実行します。 MMC ダイアログ ボックスが表示されます。  
  
3. 左側のペインに複数のコンピューターが表示される場合、アプリケーション コードが存在するコンピューターを選択します。  
  
4. IIS のバージョンは、右側のウィンドウの [ **バージョン** ] 列に表示されます。  
  
## <a name="see-also"></a>参照  
 [Web アプリケーションのリモートデバッグのための前提条件](../debugger/prerequistes-for-remote-debugging-web-applications.md)   
 [システム要件](../debugger/aspnet-debugging-system-requirements.md)   
 [ASP.NET をデバッグする準備をしています](../debugger/preparing-to-debug-aspnet.md)   
 [Web アプリケーションとスクリプトのデバッグ](../debugger/debugging-web-applications-and-script.md)
