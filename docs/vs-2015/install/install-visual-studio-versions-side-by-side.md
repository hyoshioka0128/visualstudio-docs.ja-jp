---
title: Visual Studio バージョン サイド バイ サイドのインストール |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
ms.assetid: 4d00f240-4910-4699-aaf3-cda6461f0c29
caps.latest.revision: 48
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: b01219fa0d9f3ab95fb2d64e2d3dd003557bfe51
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51761249"
---
# <a name="install-visual-studio-versions-side-by-side"></a>Visual Studio バージョン サイド バイ サイドのインストールします。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のこのバージョンは、旧バージョンの Visual Studio が既にインストールされたコンピューターにもインストールできます。 インストールに失敗した場合は、 [ログ収集ツール](http://go.microsoft.com/fwlink/?LinkId=262077) を使用して失敗に関する情報を収集し、自分で問題をデバッグできます。  
  
> [!NOTE]
>  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のバージョンをリリースされた順にインストールすることをお勧めします。 たとえば、Visual Studio 2015 をインストールする前に Visual Studio 2013 をインストールします。  
  
 複数のバージョンを並行してインストールする前に、次の条件を確認してください。  
  
-   Visual Studio 2015 を使用して [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)]で作成されたソリューションを開くと、Visual Studio 2015 に固有の機能を実装しない限り、後で以前のバージョンのソリューションを開き、再度変更できます。  
  
-   Visual Studio 2015 を使用して [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] 以前のバージョンで作成されたソリューションを開こうとすると、Visual Studio 2015 と互換性のあるプロジェクトとファイルの変更が必要になる場合があります。 詳細については、次を参照してください。、[ポート、移行、および Visual Studio プロジェクトのアップグレード](../misc/port-migrate-and-upgrade-visual-studio-projects-in-visual-studio-15-rc.md)ページ。  
  
-   複数のバージョンの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がコンピューターにインストールされている場合、そのうちの 1 つのバージョンをアンインストールすると、すべてのバージョンの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のファイルの関連付けが削除されます。 ファイルの関連付けを再度割り当てるには、 **[オプション]** ダイアログ ボックスの **[環境]**、 **[全般]** ページにある [[ファイルの関連付けを復元]](../ide/reference/general-environment-options-dialog-box.md) を使用します。  
  
-   すべての拡張機能に互換性があるわけではないので、Visual Studio は拡張機能を自動的にアップグレードしません。 [Visual Studio ギャラリー](http://go.microsoft.com/fwlink/?LinkId=178891) またはソフトウェア発行者から入手した拡張機能を再インストールする必要があります。  
  
## <a name="net-framework-versions-and-side-by-side-installations"></a>.NET Framework のバージョンと複数バージョンのインストール  
  
-   Visual Basic、Visual C#、および Visual F# のプロジェクトでは、 **プロジェクト デザイナー** の **[ターゲット フレームワーク]** オプションを使用して、プロジェクトで使用する .NET Framework のバージョンを指定します。 C++ プロジェクトでは、.vcxproj ファイルを変更すると、ターゲット フレームワークを手動で変更できます。 詳細については、次を参照してください。[バージョンの互換性](http://msdn.microsoft.com/library/2f25e522-456a-48c3-8a53-e5f39275649f)します。  
  
     プロジェクトを作成するときは、プロジェクトが対象とする .NET Framework のバージョンを **[新しいプロジェクト]** ダイアログ ボックスの **[.NET Framework]** の一覧で指定できます。  
  
     言語固有の情報については、次の表の適切なトピックを参照してください。  
  
    |言語|トピック|  
    |--------------|-----------|  
    |[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]|[[アプリケーション] ページ (プロジェクト デザイナー)](../ide/reference/application-page-project-designer-visual-basic.md)|  
    |Visual C#|[[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)|  
    |Visual F#|[プロジェクトの構成](http://msdn.microsoft.com/library/a1489abb-6294-4f8f-b71f-2cb126393526)|  
    |C++|[方法: ターゲット フレームワークおよびプラットフォームのツールセットを変更する](http://msdn.microsoft.com/library/031b1d54-e6e1-4da7-9868-3e75a87d9ffe)|  
    |[!INCLUDE[jsprjscript](../includes/jsprjscript-md.md)]|[共通言語ランタイムの以前のバージョンでの JScript アプリケーションの実行](http://msdn.microsoft.com/en-us/bbea51b5-ac03-4e6c-b9a6-f487ef63eda5)|  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio のインストール](../install/install-visual-studio-2015.md)[移植、移行、および Visual Studio プロジェクトをアップグレードします。](../misc/port-migrate-and-upgrade-visual-studio-projects-in-visual-studio-15-rc.md)   
 [分離アプリケーションおよびサイド バイ サイド アセンブリ C と C++ のビルド](http://msdn.microsoft.com/library/9465904e-76f7-48bd-bb3f-c55d8f1699b6)   
 [Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)