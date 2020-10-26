---
title: Android および iOS での OpenGL ES アプリケーションのビルド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 76a67886-df57-4a81-accb-2e3c2eaf607b
caps.latest.revision: 7
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: b9f5db4ccd70136b711f5bd221244418cf843485
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151180"
---
# <a name="build-an-opengl-es-application-on-android-and-ios"></a>Android および iOS での OpenGL ES アプリケーションのビルド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual C++ for Cross-Platform Mobile Development オプションをインストールすると、一般的なコードを共有する iOS アプリおよび Android アプリ用の Visual Studio ソリューションとプロジェクトを作成できます。 このトピックでは、簡単な iOS アプリと Android Native Activity アプリの両方を作成するソリューション テンプレートについて説明します。 これらのアプリには、OpenGL ES を使用して各プラットフォームで同じアニメーション回転キューブを表示する共通の C++ コードがあります。 OpenGL ES (OpenGL for Embedded Systems または GLES) は、多くのモバイル デバイスでサポートされている 2D および 3D グラフィックス API です。  
  
 [必要性](#req)   
 [新しい OpenGLES アプリケーションプロジェクトを作成する](#Create)   
 [Android アプリをビルドして実行する](#BuildAndroid)   
 [IOS アプリをビルドして実行する](#BuildIOS)   
 [アプリのカスタマイズ](#Customize)  
  
## <a name="requirements"></a><a name="req"></a> 必要条件  
 iOS および Android 用 OpenGL ES アプリを作成するには、その前にすべてのシステム要件を満たしていることを確認する必要があります。 Visual Studio 2015 の Visual C++ for Cross-Platform Mobile Development オプションをインストールしている必要があります。 インストールに必要なサード パーティのツールと SDK が含まれていること、また Visual Studio Emulator for Android がインストールされていることを確認してください。 詳細と詳しい手順については、「 [Install Visual C++ for Cross-Platform Mobile Development](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)」を参照してください。 iOS アプリをビルドしてテストするには、インストール手順に従って設定されている Mac コンピューターが必要になります。 IOS 開発の設定方法の詳細については、「 [ios を使用してビルドするためのツールのインストールと構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)」を参照してください。  
  
## <a name="create-a-new-opengles-application-project"></a><a name="Create"></a> 新しい OpenGLES アプリケーションプロジェクトを作成する  
 このチュートリアルでは、まず新しい OpenGL ES アプリケーション プロジェクトを作成します。それから、既定のアプリを Visual Studio Emulator for Android でビルドして実行します。 次に、iOS 用アプリをビルドし、iOS シミュレーターでアプリを実行します。  
  
#### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには  
  
1. Visual Studio を開きます。 メニュー バーで、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。  
  
2. **[新しいプロジェクト]** ダイアログ ボックスの **[テンプレート]** で **[Visual C++]**、 **[クロス プラットフォーム]** の順に選択し、 **[OpenGLES アプリケーション (Android、iOS)]** テンプレートを選択します。  
  
3. アプリケーションに `MyOpenGLESApp` のような名前を付けてから、**[OK]** をクリックします。  
  
    ![新しい OpenGLES アプリケーション プロジェクト](../cross-platform/media/cppmdd-opengles-newproj.PNG "CPPMDD_OpenGLES_NewProj")  
  
    Visual Studio は新しいソリューションを作成し、ソリューション エクスプローラーを開きます。  
  
    ![ソリューション エクスプローラーの MyOpenGLESApp](../cross-platform/media/cppmdd-opengles-solexpl.PNG "CPPMDD_OpenGLES_SolExpl")  
  
   新しい OpenGL ES アプリケーション ソリューションには、次の 3 つのライブラリ プロジェクトと 2 つのアプリケーション プロジェクトが含まれています。 ライブラリ フォルダーには、共有コード プロジェクトと共有コードを参照する 2 つのプラットフォーム固有のプロジェクトが含まれています。  
  
- **MyOpenGLESApp.Android.NativeActivity** には、Android 上の Native Activity としてアプリを実装する参照とグルー コードが含まれています。 グルー コードからのエントリ ポイントの実装は、main.cpp に配置されます。ここには MyOpenGLESApp.Shared に共通の共有コードが含まれています。 プリコンパイル済みヘッダーは pch.h にあります。 この Native Activity アプリ プロジェクトは、MyOpenGLESApp.Android.Packaging プロジェクトによって使用される共有ライブラリ (.so) ファイルにコンパイルされます。  
  
- **MyOpenGLESApp.iOS.StaticLibrary** は、MyOpenGLESApp.Shared に共有コードが含まれている iOS スタティック ライブラリ (.a) ファイルを作成します。 MyOpenGLESApp.iOS.Application プロジェクトで作成されたアプリケーションにリンクされます。  
  
- **MyOpenGLESApp.Shared** には、プラットフォーム間で機能する共有コードが含まれています。 プラットフォーム固有のコードの条件付きコンパイルにプリプロセッサ マクロを使用します。 共有コードは MyOpenGLESApp.Android.NativeActivity と MyOpenGLESApp.iOS.StaticLibrary の両方のプロジェクト参照によって使用されます。  
  
  ソリューションには、Android および iOS プラットフォーム用のアプリを構築するための 2 つのプロジェクトがあります。  
  
- **MyOpenGLESApp.Android.Packaging** は、Android デバイスまたはエミュレーターに配置する .apk ファイルを作成します。 これには、リソースと、マニフェスト プロパティを設定する AndroidManifest.xml ファイルが含まれています。 Ant のビルド プロセスを制御する build.xml も含まれています。 それは既定でスタートアップ プロジェクトとして設定されているため、Visual Studio から直接、配置して実行できます。  
  
- **MyOpenGLESApp.iOS.Application** には、MyOpenGLESApp.iOS.StaticLibrary で C++ スタティック ライブラリ コードにリンクする iOS アプリを作成するためのリソースと Objective-C グルー コードが含まれています。 このプロジェクトは、Visual Studio およびリモート エージェントによってご使用の Mac に転送されるビルド パッケージを作成します。 このプロジェクトをビルドする場合、Visual Studio はファイルとコマンドを送信して、アプリを Mac でビルドおよび配置します。  
  
## <a name="build-and-run-the-android-app"></a><a name="BuildAndroid"></a> Android アプリをビルドして実行する  
 テンプレートで作成したソリューションは、既定のプロジェクトとして、Android アプリを設定します。  インストールとセットアップを確認するために、このアプリをビルドおよび実行できます。 初期テストでは、Visual Studio Emulator for Android によってインストールされているデバイス プロファイルのいずれかでアプリを実行します。 別の対象でアプリをテストする場合は、対象のエミュレーターを読み込むか、デバイスをコンピューターに接続することができます。  
  
#### <a name="to-build-and-run-the-android-native-activity-app"></a>Android Native Activity アプリをビルドして実行するには  
  
1. 選択されていない場合は、 **[ソリューション プラットフォーム]** ドロップダウン リストから **[x86]** を選択します。  
  
    ![ソリューション プラットフォームを x86 に設定する](../cross-platform/media/cppmdd-opengles-solutionplat.png "CPPMDD_OpenGLES_SolutionPlat")  
  
    x86 を使用して Android Emulator for Windows を対象にします。 デバイスを対象とする場合は、デバイス プロセッサに基づいてソリューション プラットフォームを選択します。 [**ソリューションプラットフォーム**] リストが表示されない場合は、[**ボタンの追加と削除**] ボックスの一覧から [**ソリューションプラットフォーム**] を選択し、使用するプラットフォームを選択します。  
  
2. **ソリューション エクスプローラー**で、MyOpenGLESApp.Android.Packaging プロジェクトのショートカット メニューを開き、 **[ビルド]** を選択します。  
  
    ![Android パッケージ化プロジェクトのビルド](../cross-platform/media/cppmdd-opengles-andbuild.png "CPPMDD_OpenGLES_AndBuild")  
  
    Android 共有ライブラリと Android アプリ用のビルド プロセスの出力が [出力] ウィンドウに表示されます。  
  
    ![Android プロジェクト用の出力のビルド](../cross-platform/media/cppmdd-opengles-andoutput.png "CPPMDD_OpenGLES_AndOutput")  
  
3. 配置ターゲットとして、いずれかの VS Emulator Android Phone (x86) プロファイルを選択します。  
  
    ![配置ターゲットの選択](../cross-platform/media/cppmdd-opengles-pickemulator.png "CPPMDD_OpenGLES_PickEmulator")  
  
    別のエミュレーターをインストールしてあるか、Android デバイスを接続してある場合は、配置対象のドロップダウン リストからそれらを選択できます。 アプリを実行するには、ビルドしたソリューション プラットフォームが、ターゲット デバイスのプラットフォームと一致している必要があります。  
  
4. F5 キーを押してデバッグを開始するか、Shift キーを押しながら F5 キーを押してデバッグなしで開始します。  
  
    Visual Studio によってエミュレーターが起動されます。コードを読み込んで配置するのに数秒かかります。 以下に、Visual Studio Emulator for Android でのアプリの外観を示します。  
  
    ![Android Emulator で実行されているアプリ](../cross-platform/media/cppmdd-opengles-andemulator.png "CPPMDD_OpenGLES_AndEmulator")  
  
    アプリが開始されると、ブレークポイントの設定や、デバッガーを使用したステップ実行、ローカルの確認、値のウォッチができるようになります。  
  
5. Shift キーを押しながら F5 キーを押してデバッグを停止します。  
  
    エミュレーターは実行され続ける独立したプロセスです。 同じエミュレーターに対して、コードを何度も編集、コンパイル、配置できます。 アプリはエミュレーターのアプリ コレクションに表示され、そこから直接起動することができます。  
  
   生成された Android Native Activity アプリとライブラリ プロジェクトは、Android プラットフォームとやり取りする "グルー" コードを含むダイナミック ライブラリに C++ 共有コードを配置します。 つまり、ほとんどのアプリ コードはライブラリ内に含まれ、マニフェスト、リソース、およびビルド手順は、パッケージ化するプロジェクトに含まれます。 共有コードは、NativeActivity プロジェクトの main.cpp から呼び出されます。 Android Native Activity をプログラムする方法の詳細については、Android NDK Developer の「 [Concepts](https://developer.android.com/ndk/guides/concepts.html) 」ページを参照してください。  
  
   Visual Studio は、プラットフォーム ツールセットとして Clang を使用する Android NDK を使用して Android Native Activity プロジェクトをビルドします。 Visual Studio は、NativeActivity プロジェクトのプロパティを、ターゲット プラットフォームでコンパイル、リンク、デバッグするために使用されるコマンド ラインのスイッチとオプションにマップします。 詳細については、MyOpenGLESApp.Android.NativeActivity プロジェクトの **[プロパティ ページ]** ダイアログを参照してください。 コマンド ライン スイッチの詳細については、「 [Clang コンパイラ ユーザーズ マニュアル](http://clang.llvm.org/docs/UsersManual.html)」を参照してください。  
  
## <a name="build-and-run-the-ios-app"></a><a name="BuildIOS"></a> IOS アプリをビルドして実行する  
 iOS アプリ プロジェクトの作成および編集は Visual Studio で行いますが、ライセンスの制限があるため、プロジェクトのビルドおよび配置は、Mac から行う必要があります。 Visual Studio は、Mac で実行するリモート エージェントと通信して、プロジェクト ファイルを転送し、ビルド、配置、デバッグのコマンドを実行します。 iOS アプリをビルドするには、その前に通信できるように Mac と Visual Studio を設定および構成する必要があります。 詳細な手順については、「 [iOS を使用してビルドするためのツールのインストールと構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)」を参照してください。 リモート エージェントを実行し、Visual Studio を Mac にペアリングすると、iOS アプリをビルドおよび実行して、インストールとセットアップを確認することができます。  
  
#### <a name="to-build-and-run-the-ios-app"></a>iOS アプリをビルドして実行するには  
  
1. リモート エージェントが Mac で実行されていること、また Visual Studio がリモート エージェントにペアリングされていることを確認します。 リモート エージェントを開始するには、ターミナル アプリのウィンドウを開き、「 `vcremote`」を参照してください。 詳細については、「[Visual Studio でリモート エージェントを構成する](../cross-platform/install-and-configure-tools-to-build-using-ios.md#ConfigureVS)」を参照してください。  
  
    ![Vcremote が実行されている Mac ターミナル ウィンドウ](../cross-platform/media/cppmdd-common-vcremote.png "CPPMDD_common_vcremote")  
  
2. 選択されていない場合は、 **[ソリューション プラットフォーム]** ドロップダウン リストから **[x86]** を選択します。  
  
    ![ソリューション プラットフォームを x86 に設定する](../cross-platform/media/cppmdd-opengles-solutionplat.png "CPPMDD_OpenGLES_SolutionPlat")  
  
    x86 を使用して iOS シミュレーターを対象とします。 iOS デバイスを対象とする場合は、デバイス プロセッサ (通常、ARM プロセッサ) に基づいてソリューション プラットフォームを選択します。 [**ソリューションプラットフォーム**] リストが表示されない場合は、[**ボタンの追加と削除**] ボックスの一覧から [**ソリューションプラットフォーム**] を選択し、使用するプラットフォームを選択します。  
  
3. ソリューション エクスプローラーで、MyOpenGLESApp.iOS.Application プロジェクトのショートカット メニューを開き、 **[ビルド]** をクリックします。  
  
    ![iOS アプリケーション プロジェクトのビルド](../cross-platform/media/cppmdd-opengles-iosbuild.png "CPPMDD_OpenGLES_iOSBuild")  
  
    iOS スタティック ライブラリと iOS アプリ用のビルド プロセスの出力が [出力] ウィンドウに表示されます。 Mac でリモート エージェントを実行しているターミナル ウィンドウに、コマンドおよびファイル転送アクティビティが表示されます。  
  
    Mac コンピューターで、コード署名要求を受け入れるようにプロンプトが表示される場合があります。 [許可] を選択して続行します。  
  
4. ツールバーで **[iOS シミュレーター]** を選択し、Mac の iOS シミュレーターでアプリを実行します。 シミュレーターを開始するのにはしばらく時間がかかる場合があります。 出力を表示するために、Mac 上でシミュレーターを最前面に表示する必要がある場合があります。  
  
    ![iOS シミュレーターで実行されているアプリ](../cross-platform/media/cppmdd-opengles-iossimulator.png "CPPMDD_OpenGLES_iOSSimulator")  
  
    アプリが開始されたら、ブレークポイントを設定し、Visual Studio デバッガーを使用してローカルを確認したり、呼び出し履歴を確認したり、値を観察したりできます。  
  
    ![iOS アプリのブレークポイントにあるデバッガー](../cross-platform/media/cppmdd-opengles-iosdebug.png "CPPMDD_OpenGLES_iOSDebug")  
  
5. Shift キーを押しながら F5 キーを押してデバッグを停止します。  
  
    iOS シミュレーターは、Mac 上で実行し続ける独立したプロセスです。 同じ iOS シミュレーター インスタンスに対して、コードを何度も編集、コンパイル、配置できます。 展開した後は、シミュレーターで直接コードを実行することもできます。  
  
   生成された iOS アプリとライブラリのプロジェクトは、共有コードのみを実装するスタティック ライブラリに C++ コードを配置します。 アプリケーション コードのほとんどは、アプリケーション プロジェクトに配置されます。 このテンプレート プロジェクトの共有ライブラリ コードへの呼び出しは、GameViewController.m ファイルで実行されます。 iOS アプリをビルドするために、Visual Studio は Xcode プラットフォーム ツールセットを使用します。これは、Mac で実行されるリモート クライアントと通信する必要があります。  
  
   Visual Studio は、Xcode を使用してアプリをビルドするために、リモート クライアントに対してプロジェクト ファイルを転送し、コマンドを送信します。 リモート クライアントは、ビルドの状態情報を Visual Studio に返します。 アプリが正常にビルドされたら、Visual Studio を使用して、アプリを実行してデバッグするためのコマンドを送信できます。 Visual Studio のデバッガーは、iOS シミュレーター (Mac または接続されている iOS デバイス上で実行されます) で実行されるアプリを制御します。 Visual Studio は、StaticLibrary プロジェクトのプロパティを、ターゲット iOS プラットフォームでビルド、リンク、デバッグするために使用されるコマンド ラインのスイッチとオプションにマップします。 コンパイラ コマンド ライン オプションの詳細については、MyOpenGLESApp.iOS.StaticLibrary プロジェクトの **[プロパティ ページ]** ダイアログを開いてください。  
  
## <a name="customize-your-apps"></a><a name="Customize"></a> アプリをカスタマイズする  
 共通機能を追加または変更するために、共有 C++ コードを変更することができます。 一致するように MyOpenGLESApp.Android.NativeActivity および MyOpenGLESApp.iOS.Application プロジェクトの共有コードへの呼び出しを変更する必要があります。 プリプロセッサ マクロを使用して、共通コードにおけるプラットフォーム固有のセクションを指定することができます。 Android 用にビルドする場合は、プリプロセッサ マクロ `__ANDROID__` が事前に定義されます。 iOS 用にビルドする場合は、プリプロセッサ マクロ `__APPLE__` が事前に定義されます。  
  
 特定のプロジェクト プラットフォーム用の IntelliSense を表示するには、エディター ウィンドウの上部のナビゲーション バーにあるコンテキスト スイッチャーのドロップダウンでプロジェクトを選択します。  
  
 ![エディターのプロジェクト コンテキスト スイッチャーのドロップダウン](../cross-platform/media/cppmdd-opengles-contextswitcher.png "CPPMDD_OpenGLES_ContextSwitcher")  
  
 現在のプロジェクトにおける IntelliSense の問題については、赤色の波線でマークされます。 他のプロジェクトでの問題については、紫色の波線でマークされます。 既定では、Visual Studio はコードの色付け、Java または Objective-C ファイルの IntelliSense をサポートしません。 ただし、アプリケーション名、アイコン、およびその他の実装の詳細を設定するために、ソース ファイルを変更したり、リソースを変更したりできます。
