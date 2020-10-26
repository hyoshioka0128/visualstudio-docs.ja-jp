---
title: Android Native Activity アプリの作成 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 884014b1-5208-45ec-b0da-ad0070d2c24d
caps.latest.revision: 6
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: e554c7b97c2feac031510cfdd0894d29b4ba85eb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151080"
---
# <a name="create-an-android-native-activity-app"></a>Android Native Activity アプリの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual C++ for Cross-Platform Mobile Development オプションをインストールすると、Visual Studio 2015 を使用して、フル機能を持つ Android Native Activity アプリを作成できます。 Android Native Development Kit (NDK) は、純粋な C/C++ コードを使用して Android アプリの大半を実装することを可能にするツールセットです。 いくつかの Java JNI コードはグルーとして機能し、C/C++ コードが Android とやり取りできるようにします。 Android NDK では、Android API レベル 9 を使用して Native Activity アプリを作成する機能が導入されました。 Native Activity コードは、Unreal Engine または OpenGL を使用したゲームやグラフィックス処理の多いアプリを作成できるので人気があります。 このトピックでは、OpenGL を使用した単純な Native Activity アプリの作成方法について説明します。 他のトピックでは、Native Activity コードの編集、ビルド、デバッグ、展開の開発ライフサイクルについて説明します。  
  
 [必要性](#req)   
 [新しいネイティブアクティビティプロジェクトを作成する](#Create)   
 [既定の Android Native Activity アプリをビルドして実行する](#BuildHello)  
  
## <a name="requirements"></a><a name="req"></a> 必要条件  
 Android Native Activity アプリを作成する前に、すべてのシステム要件を満たし、Visual Studio 2015 の Visual C++ for Cross-Platform Mobile Development をインストールしていることを確認します。 詳細については、「 [Install Visual C++ for Cross-Platform Mobile Development](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)」を参照してください。 インストールに必要なサード パーティのツールと SDK が含まれていること、また Microsoft Visual Studio Emulator for Android がインストールされていることを確認してください。  
  
## <a name="create-a-new-native-activity-project"></a><a name="Create"></a> 新しいネイティブアクティビティプロジェクトを作成する  
 このチュートリアルでは、まず新しい Android Native Activity プロジェクトを作成します。それから、既定のアプリを Visual Studio Emulator for Android でビルドして実行します。  
  
#### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには  
  
1. Visual Studio を開きます。 メニュー バーで、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。  
  
2. **[新しいプロジェクト]** ダイアログ ボックスの **[テンプレート]** で **[Visual C++]**、 **[Cross Platform]** の順に選択し、 **[Native-Activity Application (Android)]** テンプレートを選択します。  
  
3. アプリケーションに `MyAndroidApp` のような名前を付けてから、**[OK]** をクリックします。  
  
    ![Native Activity プロジェクトを作成する](../cross-platform/media/cppmdd-newproject.PNG "CppMDD_NewProject")  
  
    Visual Studio は新しいソリューションを作成し、ソリューション エクスプローラーを開きます。  
  
    ![ソリューション エクスプローラーでの Native Activity プロジェクト](../cross-platform/media/cppmdd-rc-na-solutionexp.PNG "CPPMDD_RC_NA_SolutionExp")  
  
   新しい Android Native Activity アプリのソリューションには、次の 2 つのプロジェクトが含まれています。  
  
- **MyAndroidApp.NativeActivity** には、アプリが Android 上でネイティブ アクティビティとして動作するための参照とグルー コードが含まれています。 グルー コードからのエントリ ポイントの実装は main.cpp にあります。 プリコンパイル済みヘッダーは pch.h にあります。 この Native Activity アプリ プロジェクトは、共有ライブラリ (.so) ファイルにコンパイルされ、Packaging プロジェクトで使用されます。  
  
- **MyAndroidApp.Packaging** は、Android デバイスまたはエミュレーターに配置する .apk ファイルを作成します。 これには、リソースと、マニフェスト プロパティを設定する AndroidManifest.xml ファイルが含まれています。 Ant のビルド プロセスを制御する build.xml も含まれています。 それは既定でスタートアップ プロジェクトとして設定されているため、Visual Studio から直接、配置して実行できます。  
  
## <a name="build-and-run-the-default-android-native-activity-app"></a><a name="BuildHello"></a> 既定の Android Native Activity アプリをビルドして実行する  
 テンプレートによって生成されたアプリをビルドして実行し、インストールとセットアップを確認します。 この初期テストでは、Visual Studio Emulator for Android によってインストールされるデバイス プロファイルのいずれかでアプリを実行します。 別の対象でアプリをテストする場合は、対象のエミュレーターを読み込むか、デバイスをコンピューターに接続することができます。  
  
#### <a name="to-build-and-run-the-default-native-activity-app"></a>既定の Native Activity アプリをビルドして実行するには  
  
1. まだ選択されていない場合は、[**ソリューションプラットフォーム**] ボックスの一覧から [ **x86** ] を選択します。  
  
     ![ソリューション プラットフォーム ドロップダウン x86 の選択](../cross-platform/media/cppmdd-rc-na-solution-x86.png "CPPMDD_RC_NA_Solution_x86")  
  
     [**ソリューションプラットフォーム**] リストが表示されていない場合は、[**ボタンの追加と削除**] ボックスの一覧から [**ソリューションプラットフォーム**] を選択し、プラットフォームを選択します。  
  
2. メニュー バーの **[ビルド]**、 **[ソリューションのビルド]** の順にクリックします。  
  
     ソリューションに含まれる 2 つのプロジェクトのビルド プロセスの出力が [出力] ウィンドウに表示されます。  
  
3. 配置ターゲットとして、いずれかの VS Emulator Android Phone (x86) プロファイルを選択します。  
  
     別のエミュレーターをインストールしてあるか、Android デバイスを接続してある場合は、配置対象のドロップダウン リストからそれらを選択できます。  
  
4. F5 キーを押してデバッグを開始するか、Shift キーを押しながら F5 キーを押してデバッグなしで開始します。  
  
     Visual Studio Emulator for Android で、既定のアプリは次のようになります。  
  
     ![アプリを実行するエミュレーター](../cross-platform/media/cppmdd-emulator-running-app.PNG "CppMDD_Emulator_Running_App")  
  
     Visual Studio によってエミュレーターが起動されます。コードを読み込んで配置するのに数秒かかります。 アプリが開始されると、ブレークポイントの設定や、デバッガーを使用したステップ実行、ローカルの確認、値のウォッチができるようになります。  
  
5. Shift キーを押しながら F5 キーを押してデバッグを停止します。  
  
     エミュレーターは実行され続ける独立したプロセスです。 同じエミュレーターに対して、コードを何度も編集、コンパイル、配置できます。
