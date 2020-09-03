---
title: Xamarin 環境を検証する | Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: fd39882e-06d1-4b39-80d2-4d07b6e4f8f5
caps.latest.revision: 15
ms.author: crdun
manager: crdun
ms.openlocfilehash: 98925402b91bea62e10b47312e7834ed92a1a178
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75918751"
---
# <a name="verify-your-xamarin-environment"></a>Xamarin 環境を検証する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

インストーラーが完了したら (「[セットアップとインストール](../cross-platform/setup-and-install.md)」を参照)、数分をかけて、Xamarin 開発を実行するための準備ができているかどうかを確認します。  
  
 これらの確認が終わったら、次のチュートリアルの一方または両方を実行できます。  
  
- [Visual Studio での Xamarin.Forms を使用したアプリ作成の基本事項](../cross-platform/learn-app-building-basics-with-xamarin-forms-in-visual-studio.md)  
  
- [Visual Studio で Xamarin を使用してネイティブ UI を備えたアプリを作成する](../cross-platform/build-apps-with-native-ui-using-xamarin-in-visual-studio.md)  
  
## <a name="all-platforms"></a>すべてのプラットフォーム  
 最初に、**[ツール] > [オプション]** を選択し、**[Xamarin] > [その他]** を展開して、**[今すぐ確認]** リンクをクリックして更新プログラムを確認します。 以前のライセンスの問題を回避するには、Xamarin 4.0.3.214 以降を使用する必要があります。  
  
 その後、**[ファイル] > [新しいプロジェクト]** を使って Visual Studio で新しい Xamarin ソリューションを作成し、ダイアログで **[テンプレート] > [他の言語] > [Visual C#] > [クロスプラットフォーム]** の順に展開して、**[空のアプリ (ネイティブ ポータブル)]** を選び、[OK] をクリックします。 これによって、共有ポータブル クラス ライブラリ プロジェクトと Android、iOS、Windows の個々のプロジェクトを含むソリューションが作成されます。  
  
 ![空のアプリ &#40;ネイティブポータブル&#41; テンプレートから新しいプロジェクトを作成した結果](../cross-platform/media/crossplat-xamarin-verify-1.png "CrossPlat Xamarin 検証1")  
  
> [!NOTE]
> テンプレートがない場合は、このページの下部にある「 [Are the Xamarin project templates missing? Try this](#missing) 」をご覧ください。  
  
## <a name="android"></a>Android  
  
1. 最新の Android SDK ツールがインストールされていることを確認するには、**[ツール] > [Android] > [Android SDK Manager]** に移動し、最新バージョンの Android SDK ツール、Android SDK プラットフォーム ツール、Android SDK ビルド ツール コンポーネントがインストールされていることをご確認ください。 最新の Android API レベルを必ずインストールする必要はないことにご注意ください。必要な API は、対象となるプラットフォームのレベルによって異なります。 通常、Xamarin をインストールすると、必要なプラットフォームのレベルがインストールされます。  

2. Android デザイナーの検証: ソリューション エクスプローラーの Android プロジェクトで、**[リソース] > [レイアウト] > [Main.axml]** ファイルを開きます。 (このファイルが直接参照されない場合、ソリューション エクスプローラーで検索してください。Android プロジェクトにのみ存在し、iOS プロジェクトには存在しません)。  
  
    - 「インストールされている Android SDK が古すぎます」というエラーが発生した場合は、そのメッセージ内の **[Android SDK を開く]** をクリックして、上記の手順 1 に従って利用可能な最新の SDK バージョンを選んでインストールします。 
  
3. エミュレーター (またはデバイス) でのビルドとデバッグの検証:  
  
    - ソリューション エクスプローラーで Android プロジェクトを右クリックして **[スタートアップ プロジェクトに設定]** をクリックします。  
  
         ![Visual Studio はスタートアップ プロジェクト オプションとして設定されています](../cross-platform/media/crossplat-xamarin-verify-2.png "CrossPlat Xamarin Verify 2")  
  
    - 対象の Android バージョンに基づき、適切なエミュレーターを選びます。コンピューターに Android 開発デバイスが接続されている場合は、エミュレーターと共にそれもここに一覧表示されます。  
  
        - Windows 8 +: 次に示すように、Visual Studio のデバッグドロップダウンで **VS Emulator** ターゲットを選択し、 **F5**キーを押してデバッガーを開始します。 詳細については、「 [Visual studio の Android 用エミュレーターの概要](https://devblogs.microsoft.com/devops/introducing-visual-studios-emulator-for-android/) (VISUAL studio ALM ブログ)」を参照してください。 エミュレーターを機能させるときに問題が発生する場合は、「[Visual Studio Emulator for Android のトラブルシューティング](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)」をご覧ください。 **[ツール] > [Visual Studio Emulator for Android...]** を選択して、エミュレーターの新しいデバイス プロファイルを作成することもできます。  
  
             ![デバッグ ターゲットとして Visual Studio Emulator for Android を選択します](../cross-platform/media/crossplat-xamarin-verify-3.png "CrossPlat Xamarin Verify 3")  
  
             注: **[ツール] > [Visual Studio Emulator for Android...]** メニュー オプションが表示されない場合、エミュレーター自体がインストールされていない可能性があります。 **[コントロール パネル] > [プログラムと機能]** に移動し、**[Microsoft Visual Studio]** を選択して、**[変更]** をクリックすると、インストーラーを再実行できます。 インストーラーで **[変更]** をクリックし、**[Cross Platform Mobile Development] > [Microsoft Visual Studio Emulator for Android]** のボックスにチェックマークを付け、**[更新]** をクリックします。  
  
        - Windows 7 以前: ドロップダウン リストで Xamarin Player for Android を代わりに選び、F5 キーを押して実行します。 Xamarin プレーヤー、そのデバイス マネージャー、トラブルシューティングのヒントについて詳しくは、「 [Xamarin Android Player](/xamarin/android/deploy-test/debugging/debug-on-emulator?tabs=windows) 」(xamarin.com) をご覧ください。  
  
> [!NOTE]
> Visual Studio では、ツール バーに Android エミュレーター マネージャー (AVD) ボタンが表示される場合があります (以下に示します)。これは、特に Google Android エミュレーターを構成するために使用されるデバイス マネージャーを開くものです。  これは、Visual Studio Emulator for Android と Xamarin Player のどちらにも影響しません。それぞれプロファイルを構成するための独自のデバイス マネージャーを持ちます。  詳細については、「 [Visual studio の Emulator For Android の概要](https://devblogs.microsoft.com/devops/introducing-visual-studios-emulator-for-android/) (VISUAL studio ALM ブログ)」と「 [Xamarin Android Player](/xamarin/android/deploy-test/debugging/debug-on-emulator?tabs=windows) 」 (xamarin.com) を参照してください。  
> ![CrossPlat Xamarin Verify 7](../cross-platform/media/crossplat-xamarin-verify-7.png "CrossPlat Xamarin Verify 7")  
  
## <a name="windows-phone"></a>Windows Phone  
  
1. Windows Phone デザイナーの検証: ソリューション エクスプローラーの Windows Phone プロジェクトで、 **MainPage.xaml** ファイルを開きます。  
  
2. エミュレーターまたはデバイスでのビルドとデバッグの検証 (注: このステップでは、Visual Studio セットアップでインストールされた Windows Phone エミュレーターか、テザリングされたデバイスが必要です):  
  
    - ソリューション エクスプローラーで Windows Phone プロジェクトを右クリックして **[スタートアップ プロジェクトに設定]** をクリックします。  
  
    - 次に示すように、Visual Studio のデバッグドロップダウンで **エミュレーター 8.1** のターゲットまたは接続されているデバイスを選択し、F5 キーを押してデバッガーを開始します。  
  
         ![デバッグ ターゲットとして Windows Phone エミュレーターを選択します](../cross-platform/media/crossplat-xamarin-verify-4.png "CrossPlat Xamarin Verify 4")  
  
    - エミュレーターを機能させる際に問題が発生した場合は、「 [Windows Phone 8 エミュレーターのトラブルシューティング](https://msdn.microsoft.com/library/windows/apps/jj681694.aspx)」をご覧ください。  
  
## <a name="ios"></a>iOS  
  
1. 「 [Connecting to the Mac](/xamarin/ios/get-started/installation/windows/connecting-to-mac/) 」(xamarin.com) で説明されているように、ネットワーク上で Mac が利用でき、Visual Studio とペアになっていることを確認してください。  
  
2. ストーリーボード デザイナーの検証: ソリューション エクスプローラーの iOS プロジェクトで、 **Main.storyboard** ファイルを開きます。 ここでは、Visual Studio が Mac でリモート実行されているデザイナーをホストしています。  
  
3. ビルドとデバッグの検証:  
  
    1. ソリューション エクスプローラーで iOS プロジェクトを右クリックして **[スタートアップ プロジェクトに設定]** を選択します。  
  
    2. 次に示すように、Visual Studio の [ビルド] ドロップダウンから **リストで iphonesimulator** ターゲットを選択するか、テザリングさデバイスがある場合は **iPhone** ターゲットを選択します。 シミュレーターが一覧に表示されない場合は、Mac で Xcode を起動し、[ **Xcode->の基本設定**] を選択して、[ **ダウンロード**] をクリックします。 **[コンポーネント]** の下に、ダウンロード可能なシミュレーターのバージョンが表示されます。 デバッグに関するその他の手順については、Xamarin の [デバッグ](https://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/#Debugging_on_the_Simulator) ページ (xamarin.com) を参照してください。  
  
         ![iPhoneSimulator ビルド ターゲットを選択します](../cross-platform/media/crossplat-xamarin-verify-5.png "CrossPlat Xamarin 確認5")  
  
    3. 次に示すように、Visual Studio のデバッグ ドロップダウン リストで iPhone のターゲットを選び、F5 キーを押してデバッガーを開始します。 これによって、Mac 上のシミュレーターが起動し、Visual Studio でのデバッグ中にアプリを操作できるようになります。 iPhone または iPad の実機を Mac に接続した場合は、ここに表示され、代わりに選択できます。 デバイスまたはシミュレーターが一覧に表示されない場合は、上記の手順 1. でリンクされているトピックを確認するか、[**ツール**] [iOS] [  > **iOS**  > **Xamarin Mac エージェント**] に移動して、Mac への接続を確認します。  
  
         ![iPhone のデバッグ ターゲットを選択します](../cross-platform/media/crossplat-xamarin-verify-6.png "CrossPlat Xamarin 検証6")  
  
    4. Mac に接続する際に問題が発生した場合は、「 [接続のトラブルシューティング](/xamarin/ios/get-started/installation/windows/connecting-to-mac/troubleshooting) 」(xamarin.com) をご覧ください。  
  
    5. "インストールされている iOS の署名キーに一致するプロビジョニング プロファイルがインストールされていません" というエラーが表示された場合は、次の操作を行います。  
  
        - 「 [Xcode にアカウントを追加する](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/AddingYourAccounttoXcode/AddingYourAccounttoXcode.html#//apple_ref/doc/uid/TP40013839-CH40-SW1) 」(apple.com) の説明に従って、Mac 上の Xcode に Apple ID アカウントが追加されていることを確認します。  アカウントの追加後、必ず Visual Studio と Xcode の両方を再起動します。  
  
             ![CrossPlat Xamarin Verify 8](../cross-platform/media/crossplat-xamarin-verify-8.png "CrossPlat Xamarin Verify 8")  
  
        - iOS バンドル署名タブの iOS プロジェクト プロパティで、アクティブなデバッグ構成のカスタム権利フィールドが空であることを確認します。  注: 上記のエラー メッセージが表示された場合は、この設定の削除だけを試してみる必要があります。  
  
## <a name="are-the-xamarin-project-templates-missing-try-this"></a><a name="missing"></a> Xamarin プロジェクト テンプレートが見当たりませんか? これを試します  
 Xamarin の Web サイトから直接 Xamarin をインストールして、Visual Studio 2013 と Visual Studio 2015 が同時にインストールされていると、テンプレートが見つからないことがあります。 これは簡単に修正できます。ただし、Xamarin セットアッププログラムで **xamarin For Visual Studio 2015** 機能を有効にするだけです。  
  
1. コントロール パネルで **[プログラムと機能]** を開き、 **[Xamarin]** の項目を選択してから **[変更]** をクリックします。  
  
2. 表示される Xamarin のセットアップ ウィザードで、 **[次へ]** をクリックしてから、 **[変更]** をクリックします。  
  
3. インストールするオプション機能の一覧で、 **[Xamarin for Visual Studio 2015]** を展開し、 **[ローカル ドライブにインストールする]** を選択し、 **[次へ]** をクリックして機能の追加に進みます。
