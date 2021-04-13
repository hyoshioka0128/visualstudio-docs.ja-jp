---
title: Visual Studio 2019 for Mac をインストールする
description: Visual Studio 2019 for Mac とクロスプラット フォーム開発に必要なその他のコンポーネントをインストールする手順について説明します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 03/04/2021
ms.technology: vs-ide-install
ms.assetid: 22B1F2CD-32AE-464D-80AC-C8AB4786B015
ms.custom: video
ms.topic: how-to
ms.openlocfilehash: 653e653a0574da52c0030b06c7a8c13b436ed686
ms.sourcegitcommit: 4bf7d82eb3a837ad5d1ae5c110039cbf74258f18
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2021
ms.locfileid: "106273415"
---
# <a name="install-visual-studio-2019-for-mac"></a>Visual Studio 2019 for Mac をインストールする

macOS でネイティブのクロスプラット フォーム対応の .NET アプリの開発を開始するには、以下の手順に従って Visual Studio 2019 for Mac をインストールします。

 > [!div class="button"]
 > [Visual Studio for Mac をダウンロードする](https://visualstudio.microsoft.com/vs/mac/)

## <a name="requirements"></a>必要条件

- macOS High Sierra 10.13 以降が搭載された Mac。

iOS または macOS 向けに Xamarin アプリをビルドするには、以下も必要になります。

- 最新バージョンの Xcode と互換性がある Mac。 Apple の[最小要件に関するドキュメント](https://developer.apple.com/support/xcode/)を参照してください。
- 最新バージョンの [Xcode](https://developer.apple.com/xcode)。 お使いの Mac と最新バージョンの間に互換性がない場合、[以前のバージョンの Xcode を使用](https://docs.microsoft.com/xamarin/ios/troubleshooting/questions/old-version-xcode)できることがあります。
- Apple ID。 Apple ID をまだ持っていない場合は、 https://appleid.apple.com で新しい ID を作成できます。 Xcode をインストールしてサインインするには、Apple ID を持っている必要があります。

## <a name="installation-instructions"></a>インストール手順

1. [Visual Studio for Mac のダウンロード ページ](https://visualstudio.microsoft.com/vs/mac/)から、インストーラーをダウンロードします。
2. ダウンロードが完了したら、 **[VisualStudioforMacInstaller.dmg]** をクリックしてインストーラーをマウントし、矢印のロゴをダブルクリックして実行します。

    [![大きい矢印をクリックしてインストールを開始する](media/install-installer-sml.png)](media/install-installer.png#lightbox)

3. インターネットから、ダウンロードしているアプリケーションに関する警告が表示される場合があります。 **[開く]** をクリックします。
4. インストーラーがシステムを確認するまで待ちます。

    [![インストーラーがシステムにインストールされているコンポーネントを確認する](media/install-checking-sml.png)](media/install-checking.png#lightbox)

5. プライバシーとライセンス条項を確認するように求める警告が表示されます。 リンクに従ってそれらを読んでから、同意する場合は **[続行]** を押します。

    [![プライバシーと条項へのリンクに従って、同意する場合は続行する](media/install-privacy.png)](media/install-privacy.png#lightbox)

6. 使用可能なワークロードの一覧が表示されます。 使用するコンポーネントを選択します。

    [![Visual Studio Mac インストーラーの [何をインストールしますか?] 画面のスクリーンショット。インストール可能なコンポーネントの一覧が表示されます。](media/install-selection.png)](media/install-selection.png#lightbox)

   すべてのプラットフォームをインストールすることを希望されない場合には、以下のガイドを使用してインストールするプラットフォームを決めることがきます。

   |アプリの種類  |Target  |選択ツール  |メモ  |
   |---------|---------|---------|---------|
   |**Xamarin を使用するアプリ**| Xamarin.Forms|**Android** と **iOS** プラットフォームを選択します |次に、[**Xcode**](https://developer.apple.com/xcode/) をインストールする必要があります |
   ||iOS のみ|**iOS** プラットフォームを選択します|次に、[**Xcode**](https://developer.apple.com/xcode/) をインストールする必要があります|
   ||Android のみ|**Android** プラットフォームを選択します|関連する依存関係も選択する必要があります|
   ||Mac のみ|**macOS (Cocoa)** プラットフォームを選択します|次に、[**Xcode**](https://developer.apple.com/xcode/) をインストールする必要があります|
   |**.NET Core アプリケーション**|         |**.NET Core** プラットフォームを選択します。|         |
   |**ASP.NET Core Web アプリケーション**|         |**.NET Core** プラットフォームを選択します。|         |
   |**Azure Functions**|         |**.NET Core** プラットフォームを選択します。|         |
   |**クロスプラットフォーム Unity ゲームの開発**|         |Visual Studio for Mac 以外の追加のプラットフォームをインストールする必要はありません。| Unity 拡張機能のインストールの詳細については、[Unity セットアップ ガイド](./setup-vsmac-tools-unity.md)に関するページをご覧ください。|

7. 選択を行ったら、 **[インストール]** ボタンを押します。
8. インストーラーではダウンロードの進行状況が表示され、Visual Studio for Mac と選択したワークロードがインストールされます。 インストールに必要な権限を付与するため、パスワードの入力が求められます。

    [![Visual Studio Mac インストーラーのスクリーンショット。Mac 用 .NET 開発者ツールキットのインストール進行状況画面が表示されています。](media/installation-progress.png)](media/installation-progress.png#lightbox)

9. インストールが完了すると、サインインして使用するキー バインドを選択することで、インストールをカスタマイズするように求めるメッセージが Visual Studio for Mac に表示されます。

    [![IDE にサインインする](media/ide-tour-2019-start-signin.png)](media/ide-tour-2019-start-signin.png#lightbox)

    [![使用するキーボード ショートカットを選択する](media/ide-tour-2019-keyboard-shortcut.png)](media/ide-tour-2019-keyboard-shortcut.png#lightbox)

企業環境でのインストール中にネットワークに問題が発生した場合は、[ファイアウォールまたはプロキシの背後へのインストール](#install-visual-studio-for-mac-behind-a-firewall-or-proxy-server)の指示を確認してください。

[リリース ノート](/visualstudio/releasenotes/vs2019-mac-relnotes)における変更点について学習します。

> [!NOTE]
> 元のインストールでプラットフォームやツールをインストールしなかった場合 (手順 6 でオフにした場合)、そのコンポーネントを後で追加するには、インストーラーをもう一度実行する必要があります。

## <a name="install-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>ファイアウォールまたはプロキシ サーバーの内側に Visual Studio for Mac をインストールする

ファイアウォールの内側に Visual Studio for Mac をインストールするには、ソフトウェアに必要なツールと更新プログラムのダウンロードができるように特定のエンドポイントにアクセスできる必要があります。

以下の場所にアクセスできるようにネットワークを構成します。

- [Visual Studio エンドポイント](./install-behind-a-firewall-or-proxy-server.md)

## <a name="next-steps"></a>次の手順

Visual Studio for Mac をインストールすると、アプリのコードの記述を開始できます。 以下のガイドで、次の手順であるプロジェクトの記述と配置について説明します。

### <a name="ios"></a>iOS

1. [Hello, iOS](https://docs.microsoft.com//xamarin/ios/get-started/hello-ios/)
2. [デバイス プロビジョニング](https://docs.microsoft.com/xamarin/ios/get-started/installation/device-provisioning/) (デバイスでアプリケーションを実行する場合)。

### <a name="android"></a>Android

1. [Hello Android](https://docs.microsoft.com/xamarin/android/get-started/hello-android/)
2. [Xamarin Android SDK Manager の使用](https://docs.microsoft.com/xamarin/android/get-started/installation/android-sdk?tabs=macos)
3. [Android SDK エミュレーター](https://docs.microsoft.com/xamarin/android/get-started/installation/android-emulator/)
4. [開発用のデバイスの設定](https://docs.microsoft.com/xamarin/android/get-started/installation/set-up-device-for-development)

### <a name="xamarinforms"></a>Xamarin.Forms

Xamarin.Forms でネイティブ クロスプラットフォーム アプリケーションを構築する:

1. [Xamarin.Forms のクイックスタート](https://docs.microsoft.com/xamarin/get-started/quickstarts/)

### <a name="net-core-apps-aspnet-core-web-apps-unity-game-development"></a>.NET Core アプリ, ASP.NET Core Web アプリ, Unity ゲーム開発

他のワークロードについては、[ワークロード](workloads.md)に関するページをご覧ください。

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Acquisition/player]

## <a name="see-also"></a>関連項目

- [Visual Studio のインストール (Windows)](/visualstudio/install/install-visual-studio)
