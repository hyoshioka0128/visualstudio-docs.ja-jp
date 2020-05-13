---
title: Visual Studio 2015 のインストール | Microsoft Docs
titleSuffix: ''
ms.date: 04/15/2020
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
f1_keywords:
- vs.about
helpviewer_keywords:
- Visual Studio, installing
- installing Visual Studio
- server installations [Visual Studio]
- Setup [Visual Studio]
- install Visual Studio
- visual studio installer
ms.assetid: da049020-cfda-40d7-8ff4-7492772b620f
caps.latest.revision: 183
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 1bfc573c30281e5bc976ee25ea3a80a2f874ab25
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81445078"
---
# <a name="install-visual-studio-2015"></a>Visual Studio 2015 のインストール

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このページには、開発者用の生産性ツールの統合されたスイートである、**Visual Studio 2015** をインストールする際に役立つ詳細情報が含まれています。 また、[機能](https://docs.microsoft.com/visualstudio/releasenotes/vs2015-version-history)、[システム要件](https://docs.microsoft.com/visualstudio/productinfo/vs2015-sysrequirements-vs)、ダウンロード、その他の情報にすばやくアクセスするためのリンク[も](https://visualstudio.microsoft.com/vs/older-downloads/)含まれています。

## <a name="quick-links"></a>クイック リンク

詳細について説明する前に、最も頻繁に要求されたリンクを列挙します。

|||
|------------------|----------------|
|![Visual Studio をダウンロードする](../install/media/downloads.png "ダウンロード") |**ダウンロード**: Visual Studio 2015 をインストールするには、製品の実行可能ファイルを[My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015)ページからダウンロードするか (サブスクリプションが必要です)、またはボックス化された製品のインストール メディアを使用します。 [最新バージョンまたは以前のバージョンの Visual Studio をダウンロードする方法の詳細については、こちらを参照](https://www.visualstudio.com/vs/older-downloads/)してください。|
|![機能の詳細](../install/media/features.png "特徴") |**機能**: Visual Studio 2015 の機能の詳細については[、RTM](https://docs.microsoft.com/visualstudio/releasenotes/vs2015-rtm-vs)、[更新プログラム 1](https://docs.microsoft.com/visualstudio/releasenotes/vs2015-update1-vs)、[更新 2](https://docs.microsoft.com/visualstudio/releasenotes/vs2015-update2-vs)、および[更新プログラム 3](https://docs.microsoft.com/visualstudio/releasenotes/vs2015-update3-vs)のリリース ノートを参照してください。|
|![システム要件の表示](../install/media/system-requirements.png "システム要件") |**システム要件**: Visual Studio 2015 の各エディションのシステム要件を表示するには[、Visual Studio 2015 プラットフォームの対象と互換性](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs)のページを参照してください。|
|![プロダクト キーを探す](../install/media/product-keys.png "プロダクト キー") |**プロダクト キー**: プロダクト キーを検索するには、「[方法: Visual Studio プロダクト キーを検索する](../install/how-to-locate-the-visual-studio-product-key.md)」を参照してください。|
|![ライセンスについて調べる](../install/media/licensing.png "ライセンス") |**ライセンス**: 個人または企業の両方の顧客のライセンス オプションについては[、Visual Studio 2015 ライセンスに関するホワイト ペーパーを](https://www.microsoft.com/download/details.aspx?id=13350)参照してください。|

## <a name="default-vs-custom-setup"></a><a name="custom"></a>既定とカスタム セットアップ
 Visual Studio 2015 をインストールするときに、日常的に使用するコンポーネントを含めたり除外したりできます。 一般的に、既定のインストールはカスタム インストールよりサイズが小さく、インストールにかかる時間も短くなります。 また、以前のバージョンで既定でインストールされていたコンポーネントの多数が、このバージョンでは、明示的に選択する必要があるカスタム コンポーネントと見なされるようになりました。

 ![Visual Studio 2015 のセットアップ ダイアログ](../ide/media/vs2015-setup-screen.png "VS2015_Setup_screen")

 カスタム コンポーネントには、Visual C++ 、Visual F# 、SQL Server データ ツール、クロスプラットフォーム モバイル ツールと SDK、サードパーティの SDK と拡張機能などがあります。 カスタム コンポーネントはいずれも、初期セットアップ時に選択しなくても後でインストールすることができます。

> [!NOTE]
> カスタム インストールには、既定のインストールに含まれるコンポーネントが自動的に組み込まれます。

 カスタム コンポーネントの完全な一覧は、次のとおりです。

|機能セット|Components|
|------------------|----------------|
|**更新プログラム**|Visual Studio 2015 更新プログラム 3|
|**プログラミング言語**|Visual C++<br />Visual F#<br />Python Tools for Visual Studio|
|**Windows 開発および Web 開発**|ClickOnce 発行ツール<br />LightSwitch<br />Microsoft Office Developer Tools<br />Microsoft SQL Server Data Tools<br /> Microsoft Web Developer Tools<br />ビジュアル スタジオ (サード パーティ) 用の PowerShell ツール<br />Silverlight 開発キット<br />ユニバーサル Windows アプリ開発ツール<br />Windows 10 のツールおよび SDK<br />Windows 8.1 および Windows Phone 8.0/8.1 ツール<br />Windows 8.1 のツールおよび SDK|
|**クロス プラットフォームのモバイル開発**|C#/.NET (Xamarin)<br />HTML/JavaScript (Apache Cordova)<br />iOS/Android 向け Visual C++ モバイル開発<br />Clang with Microsoft CodeGen|
|**共通ツールおよびソフトウェア開発キット**|アンドロイドネイティブ開発キット(サードパーティ)<br /> アンドロイドSDK [サードパーティ]<br />アンドロイド SDK セットアップ API (サード パーティ)<br />アパッチアント(第三者)<br /> Java SE開発キット(サードパーティ)<br /> ジョイエント ノード.js (サード パーティ)|
|**一般的なツール**|ウィンドウズ用の Git (サード パーティ)<br />ビジュアル スタジオ用の GitHub 拡張機能 (サード パーティ)<br /> Visual Studio 機能拡張ツール|

## <a name="install-visual-studio"></a><a name="installing"></a>ビジュアル スタジオのインストール
 Visual Studio をインストールするには、インストール メディア (DVD) を使用して、visual Studio サブスクリプション サービスを使用して[、My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) Web サイトから[、Visual Studio ダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/)Web サイトから Web インストーラーをダウンロードするか、またはオフライン インストール レイアウトを作成します (詳細については[、「Visual Studio のオフライン インストールの作成](../install/create-an-offline-installation-of-visual-studio.md)」ページを参照してください)。

> [!IMPORTANT]
> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]をインストールするには、管理者の資格情報が必要です。 ただしインストール後、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の使用には不要です。

 Visual Studio のすべてをインストールするには、ローカル管理者アカウントの次の特権が有効になっている必要があります。

|ローカル ポリシー オブジェクト表示名|ユーザー権限|
|--------------------------------------|----------------|
|ファイルとディレクトリのバックアップ|SeBackupPrivilege|
|プログラムのデバッグ|SeDebugPrivilege|
|監査ログとセキュリティ ログの管理|SeSecurityPrivilege|

 ローカル管理者アカウントの要件の詳細については、サポート技術情報「 [セットアップ アカウントに特定のユーザー権限がない場合、SQL Server のインストールが失敗する](https://support.microsoft.com/kb/2000257)」を参照してください。

### <a name="use-installation-media"></a><a name="BKMK_Media"></a>インストール メディアを使用する
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]をインストールするには、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] インストール メディアのルート ディレクトリで、必要なエディションのインストール ファイルを実行します。

|Edition|インストール ファイル|
|-------------|-----------------------|
|Visual Studio Enterprise|vs_enterprise.exe|
|Visual Studio Professional|vs_professional.exe|
|Visual Studio コミュニティ|vs_community.exe|

### <a name="download-from-the-product-website"></a><a name="BKMK_Website"></a>製品のウェブサイトからダウンロード
 Visual [Studio](https://visualstudio.microsoft.com/vs/older-downloads/)のダウンロード ページにアクセスし、必要な Visual Studio のエディションを選択します。

### <a name="download-from-your-subscription-service"></a>サブスクリプション サービスからダウンロードする
 [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015)ページにアクセスし、必要なエディションの Visual Studio を選択します。

### <a name="create-an-offline-installation-layout"></a><a name="BKMK_Offline"></a>オフライン インストール レイアウトを作成する
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]インストール メディアがない場合、または Visual Studio サブスクリプションがない場合、または Web インストーラーを使用してインストール[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]しない場合は、オフライン インストール レイアウトと呼ばれるものを作成して"切断済み" インストールを実行できます。 詳細については[、「Visual Studio のオフライン インストールの作成](../install/create-an-offline-installation-of-visual-studio.md)」ページを参照してください。

## <a name="deploy-visual-studio-in-an-enterprise"></a><a name="enterprise"></a>エンタープライズでの Visual Studio の展開
 ネットワーク経由で配置[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]する方法については、『 Visual Studio[管理者ガイド](../install/visual-studio-administrator-guide.md)』を参照してください。

### <a name="install-visual-studio-in-a-virtualized-environment"></a><a name="BKMK_Virtualized"></a>仮想化環境での Visual Studio のインストール
 **Hyper-V に関するビデオの問題**

 Hyper-V が有効であり、アクセラレータ機能を使用するグラフィックス アダプターが搭載されている Windows Server 2008 R2 を実行すると、システムの速度が低下することがあります。

 詳細については、「 [Hyper-V の役割が有効で、高速ディスプレイ アダプタがインストールされている Windows Server 2008 または Windows Server 2008 R2 ベースのコンピュータでビデオパフォーマンスが低下する」](https://support.microsoft.com/kb/961661)を参照してください。

 **Hyper-V によるデバイスのエミュレート**

 仮想化を使わずに Visual Studio 2015 を実際のハードウェアにインストールする場合、Hyper-V を使用して Windows デバイスと Android デバイスのエミュレーションを有効にする機能を選択できます。 HYPER-V にインストールすると、Windows デバイスまたは Android デバイスをエミュレートできなくなります。 これは、エミュレーター自体が仮想マシンであり、現時点では別の VM の内部で VM をホストすることができないためです。 回避策として、アプリケーションを直接デプロイおよびデバッグできる実際の Windows デバイスまたは Android デバイスを用意することができます。

## <a name="install-optional-components"></a><a name="optionalComponents"></a>オプション コンポーネントのインストール
 元のインストール時に選択しなかった可能性のあるコンポーネントをインストールする場合は、次の手順を実行します。

#### <a name="to-install-optional-components"></a>オプション コンポーネントをインストールするには

1. **[コントロール パネル]** の **[プログラムと機能]** ページで、1 つまたは複数のコンポーネントを追加する製品のエディションを選択し、 **[変更]** を選択します。

2. セットアップ ウィザードで、 **[変更]** を選択し、インストールするコンポーネントを選択します。

3. **[次へ]** を選択し、残りの指示に従います。

## <a name="install-offline-help-content"></a><a name="helpContent"></a>オフライン ヘルプ コンテンツのインストール
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]をインストールした後、オフラインで使用できるように、追加のヘルプ コンテンツをダウンロードすることができます。

#### <a name="to-install-or-uninstall-help-content"></a>ヘルプ コンテンツをインストールまたはアンインストールするには

1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] メニュー バーで、 **[ヘルプ]**、 **[ヘルプ コンテンツの追加と削除]** の順にクリックします。

2. **[Microsoft ヘルプ ビューア―]** の **[コンテンツの管理]** タブで、ヘルプ コンテンツのインストール ソースを選択します。

3. 特定のヘルプ コレクションを検索する場合は、**[検索]** ボックスに名前やキーワードを入力し、**Enter** キーを押します。

4. 必要なヘルプ コレクションの横で、 **[追加]** または **[削除]** リンクをクリックします。

5. [**更新**] ボタンをクリックします。

   オフライン ヘルプをインストールまたは展開する方法の詳細については、[ヘルプビューア管理者ガイド](../ide/help-viewer-administrator-guide.md)を参照してください。

## <a name="check-for-service-releases-and-product-updates"></a><a name="serviceReleases"></a>サービス リリースと製品の更新を確認する
 すべての拡張機能に互換性があるわけではないので、以前のバージョンからアップグレードするときに、Visual Studio は拡張機能を自動的にアップグレードしません。 [拡張機能は、Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)またはソフトウェア発行者から再インストールする必要があります。

#### <a name="to-automatically-check-for-service-releases"></a>サービス リリースを自動的に確認するには

1. メニュー バーで、[**ツール]、[****オプション**] の順に選択します。

2. **[オプション]** ダイアログ ボックスの **[環境]** を展開し、 **[拡張機能と更新プログラム]** をクリックします。 **[更新プログラムを自動的にチェックする]** チェック ボックスが選択されていることを確認し、 **[OK]** をクリックします。

## <a name="register-visual-studio"></a>登録のビジュアル スタジオ

1. メニュー バーで、 **[ヘルプ]**、 **[バージョン情報]** の順にクリックします。

     **[バージョン情報]** ダイアログ ボックスに製品 ID 番号 (PID) が表示されます。 製品を登録するには、PID と Windows アカウントの資格情報 (Hotmail や Outlook.com などの電子メール アドレスとパスワード) が必要です。

2. メニュー バーで、 **[ヘルプ]**、 **[製品の登録]** の順に選択します。

## <a name="repair-visual-studio"></a><a name="repair"></a>ビジュアル スタジオの修復

#### <a name="to-repair-visual-studio"></a>Visual Studio を修復するには

1. **[コントロール パネル]** の **[プログラムと機能]** ページで、修復する製品のエディションを選択し、 **[変更]** を選択します。

2. セットアップ ウィザードで、 **[修復]**、 **[次へ]** の順に選択し、残りの指示に従います。

#### <a name="to-repair-visual-studio-in-silent-or-passive-modes-that-is-to-repair-from-source"></a>サイレント モードまたはパッシブ モードで Visual Studio を修復するには (ソースから修復する)

1. Visual Studio がインストールされているコンピューターで、Windows コマンド プロンプトを開きます。

2. 次のパラメーターを入力します。

     *DVDRoot* \\ <*インストール ファイル*\>\<`/quiet|/passive``norestart`> [/ ]/`Repair`

## <a name="troubleshoot-an-installation"></a><a name="troubleshooting"></a>インストールのトラブルシューティング
 セットアップとインストールの問題に対して次のリソースを使用します。

- 「[Visual Studio Setup and Installation (Visual Studio のセットアップとインストール)](https://social.msdn.microsoft.com/Forums/en-US/vssetup/threads) 」フォーラム。 Visual Studio コミュニティでは、他のユーザーからの質問と回答を閲覧できます。 必要な情報が見つからない場合は、自分で質問してください。

- [ビジュアル スタジオのヘルプを参照](https://visualstudio.microsoft.com/vs/support/vs2015/)してください。 サポート技術情報 (KB) の記事を検索し、Visual Studio のインストールに関する問題に関する情報については、マイクロソフト サポートに問い合わせる方法を確認します。

## <a name="related-topics"></a><a name="relatedTopics"></a>関連トピック

|タイトル|説明|
|-----------|-----------------|
|[Visual Studio のオフライン インストールを作成する](../install/create-an-offline-installation-of-visual-studio.md)|インターネットに接続していない場合に Visual Studio をインストールする方法について説明します。
|[Visual Studio のバージョンをサイド バイ サイドでインストールする](../install/install-visual-studio-versions-side-by-side.md)|同じコンピューターに複数バージョンの Visual Studio をインストールする方法について説明します。|
|[コマンド ライン パラメーターを使用して Visual Studio をインストールする](/visualstudio/install/use-command-line-parameters-to-install-visual-studio)|コマンド プロンプトから Visual Studio をインストールするときに使用できるコマンド ライン パラメーターの一覧を示します。|
|[Visual Studio のアンインストール](../install/uninstall-visual-studio.md)|Visual Studio をアンインストールする方法について説明します。|
|[ビジュアルスタジオ管理者ガイド](../install/visual-studio-administrator-guide.md)|Visual Studio の配置オプションについて説明します。|
|[ビジュアルスタジオイメージライブラリ](../designers/the-visual-studio-image-library.md)|Visual Studio アプリケーションで使用できるグラフィックスをインストールする方法について説明します。|
|[Visual Studio を使用した開発の開始](../ide/get-started-developing-with-visual-studio.md)|Visual Studio をより効果的に使用するのに役立つ情報とリンクが含まれています。|

## <a name="see-also"></a>参照

- [Visual Studio へのサインイン](../ide/signing-in-to-visual-studio.md)
