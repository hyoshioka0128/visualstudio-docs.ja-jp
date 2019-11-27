---
title: Visual Studio 2015 のインストール | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
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
ms.openlocfilehash: a31bc328c20aada21b05edeef61886d57e914165
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298056"
---
# <a name="install-visual-studio-2015"></a>Visual Studio 2015 のインストール

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このページには、開発者用の生産性ツールの統合されたスイートである、**Visual Studio 2015** をインストールする際に役立つ詳細情報が含まれています。 [機能](https://www.visualstudio.com/news/vs2015-vs.aspx)、 [エディション](https://go.microsoft.com/fwlink/?LinkID=242142)、 [システム要件](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs)、 [ダウンロード](https://go.microsoft.com/fwlink/?LinkId=517106)などの情報にすばやくアクセスできるリンクも記載しています。

## <a name="quick-links"></a>クイック リンク

詳細について説明する前に、最も頻繁に要求されたリンクを列挙します。

|||
|------------------|----------------|
|![Visual Studio のダウンロード](../install/media/downloads.png "ダウンロード") |**ダウンロード**: Visual Studio 2015 をインストールするには、 [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015)ページ (サブスクリプションが必要) から製品の実行可能ファイルをダウンロードするか、ボックス化された製品のインストールメディアを使用します。 [Visual Studio の現在または以前のバージョンをダウンロードする方法については、こちらを参照して](https://www.visualstudio.com/vs/older-downloads/)ください。|
|![機能についての詳細情報](../install/media/features.png "機能") |**機能**: Visual Studio 2015 の機能の詳細については、 [RTM](https://www.visualstudio.com/news/vs2015-vs)、 [update 1](https://www.visualstudio.com/news/vs2015-update1-vs)、 [update 2](https://www.visualstudio.com/news/vs2015-update2-vs)、 [update 3](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs)のリリースノートを参照してください。|
|![各 SKU の内容を確認する](../install/media/sku.png "SKU") |**SKU**: Visual Studio 2015 の各エディションで提供しているものについては、「[Visual Studio 製品の比較](https://go.microsoft.com/fwlink/?LinkID=242142)」ページを参照してください。|
|![システム要件の表示](../install/media/system-requirements.png "システム要件") |**システム要件**: visual studio 2015 の各エディションのシステム要件を表示するには、 [visual Studio 2015 の互換性](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs)に関するページを参照してください。|
|![プロダクトキーを探す](../install/media/product-keys.png "プロダクト キー") |**プロダクト**キー: プロダクトキーを検索するには、「[方法: Visual Studio プロダクトキーを検索](../install/how-to-locate-the-visual-studio-product-key.md)する」を参照してください。|
|![ライセンスについて確認する](../install/media/licensing.png "ライセンス") |**ライセンス**: 個人または企業のお客様のライセンスオプションの詳細については、 [VISUAL Studio と MSDN のライセンス](https://www.microsoft.com/download/details.aspx?id=13350)に関するホワイトペーパーを参照してください。|

## <a name="custom"></a>既定値とカスタムセットアップ
 Visual Studio 2015 をインストールするときに、日常的に使用するコンポーネントを含めたり除外したりできます。 一般的に、既定のインストールはカスタム インストールよりサイズが小さく、インストールにかかる時間も短くなります。 また、以前のバージョンで既定でインストールされていたコンポーネントの多数が、このバージョンでは、明示的に選択する必要があるカスタム コンポーネントと見なされるようになりました。

 ![Visual Studio 2015 セットアップダイアログ](../ide/media/vs2015-setup-screen.png "VS2015_Setup_screen")

 カスタム コンポーネントに含まれるのは、Visual C++、Visual F#、SQL Server Data Tools、クロス プラットフォームのモバイル ツールおよび SDK、サード パーティの SDK、拡張機能などです。 カスタム コンポーネントはいずれも、初期セットアップ時に選択しなくても後でインストールすることができます。

> [!NOTE]
> カスタム インストールには、既定のインストールに含まれるコンポーネントが自動的に組み込まれます。

 カスタム コンポーネントの完全な一覧は、次のとおりです。

|機能セット|Components|
|------------------|----------------|
|**更新プログラム**|Visual Studio 2015 更新プログラム 3|
|**プログラミング言語**|Visual C++<br />Visual F#<br />Python Tools for Visual Studio|
|**Windows 開発および Web 開発**|ClickOnce Publishing Tools<br />LightSwitch<br />Microsoft Office Developer Tools<br />Microsoft SQL Server Data Tools<br /> Microsoft Web Developer Tools<br />PowerShell Tools for Visual Studio (サードパーティ)<br />Silverlight 開発キット<br />ユニバーサル Windows アプリ開発ツール<br />Windows 10 のツールおよび SDK<br />Windows 8.1 および Windows Phone 8.0/8.1 ツール<br />Windows 8.1 のツールおよび SDK|
|**クロス プラットフォームのモバイル開発**|C#/.NET (Xamarin)<br />HTML/JavaScript (Apache Cordova)<br />iOS/Android 向け Visual C++ モバイル開発<br />Clang with Microsoft CodeGen|
|**一般的なツールとソフトウェア開発キット**|Android Native Development Kit (サードパーティ)<br /> Android SDK [サードパーティ]<br />Android SDK セットアップ Api (サードパーティ)<br />Apache Ant (サードパーティ)<br /> Java SE Development Kit (サードパーティ)<br /> Joyent node.js (サードパーティ)|
|**一般的なツール**|Git for Windows (サードパーティ)<br />Visual Studio 用の GitHub 拡張機能 (サードパーティ)<br /> Visual Studio 機能拡張ツール|

## <a name="installing"></a> Visual Studio のインストール
 インストールメディア (Dvd) を使用して Visual Studio をインストールするには、 [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) web サイトから visual studio サブスクリプションサービスを使用するか、 [Visual studio のダウンロード](https://go.microsoft.com/fwlink/?LinkId=517106)web サイトから web インストーラーをダウンロードするか、オフラインインストールレイアウトを作成します (詳細については、「 [visual Studio のオフラインインストールの作成](../install/create-an-offline-installation-of-visual-studio.md)」ページを参照してください)。

> [!IMPORTANT]
> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]をインストールするには、管理者の資格情報が必要です。 ただしインストール後、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の使用には不要です。

 Visual Studio のすべてをインストールするには、ローカル管理者アカウントの次の特権が有効になっている必要があります。

|ローカル ポリシー オブジェクト表示名|ユーザー権限|
|--------------------------------------|----------------|
|ファイルとディレクトリのバックアップ|SeBackupPrivilege|
|プログラムのデバッグ|SeDebugPrivilege|
|監査とセキュリティ ログの管理|SeSecurityPrivilege|

 ローカル管理者アカウントの要件の詳細については、サポート技術情報「 [セットアップ アカウントに特定のユーザー権限がない場合、SQL Server のインストールが失敗する](https://support.microsoft.com/kb/2000257)」を参照してください。

### <a name="BKMK_Media"></a>インストールメディアの使用
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]をインストールするには、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] インストール メディアのルート ディレクトリで、必要なエディションのインストール ファイルを実行します。

|エディション|インストール ファイル|
|-------------|-----------------------|
|Visual Studio Enterprise|vs_enterprise.exe|
|Visual Studio Professional|vs_professional.exe|
|Visual Studio コミュニティ|vs_community.exe|

### <a name="BKMK_Website"></a>製品 web サイトからのダウンロード
 [Visual studio のダウンロード](https://go.microsoft.com/fwlink/?LinkId=517106)ページにアクセスし、必要な visual studio のエディションを選択します。

### <a name="downloading-from-your-subscription-service"></a>サブスクリプションサービスからダウンロードしています
 [ [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) ] ページにアクセスし、必要な Visual Studio のエディションを選択します。

### <a name="BKMK_Offline"></a>オフラインインストールレイアウトを作成する
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] インストールメディアがない場合、または Visual Studio サブスクリプションを持っていない場合、または web インストーラーを使用して [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] をインストールしたくない場合は、オフラインインストールレイアウトと呼ばれるものを作成することによって、"切断された" インストールを実行できます。 詳細については、「 [Visual Studio のオフラインインストールを作成](../install/create-an-offline-installation-of-visual-studio.md)する」ページを参照してください。

## <a name="enterprise"></a>エンタープライズでの Visual Studio のデプロイ
 ネットワーク経由で [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] をデプロイする方法の詳細については、「 [Visual Studio 管理者ガイド](../install/visual-studio-administrator-guide.md)」を参照してください。

### <a name="BKMK_Virtualized"></a>仮想化環境への Visual Studio のインストール
 **Hyper-V に関するビデオの問題**

 Hyper-V が有効であり、アクセラレータ機能を使用するグラフィックス アダプターが搭載されている Windows Server 2008 R2 を実行すると、システムの速度が低下することがあります。

 詳細については、Microsoft Web サイトの「 [Video performance may decrease when a Windows Server 2008 or Windows Server 2008 R2 based computer has the Hyper-V role enabled and an accelerated display adapter installed (Windows Server 2008 または Windows Server 2008 R2 ベースのコンピューターで Hyper-V の役割を有効にし、アクセラレータ機能を使用するディスプレイ アダプターをインストールしたときに、ビデオ パフォーマンスが低下する場合がある)](https://go.microsoft.com/fwlink/?LinkID=231084)」を参照してください。

 **Hyper-V によるデバイスのエミュレート**

 仮想化を使わずに Visual Studio 2015 を実際のハードウェアにインストールする場合、Hyper-V を使用して Windows デバイスと Android デバイスのエミュレーションを有効にする機能を選択できます。 HYPER-V にインストールすると、Windows デバイスまたは Android デバイスをエミュレートできなくなります。 これは、エミュレーター自体が仮想マシンであり、現時点では別の VM の内部で VM をホストすることができないためです。 回避策として、アプリケーションを直接デプロイおよびデバッグできる実際の Windows デバイスまたは Android デバイスを用意することができます。

## <a name="optionalComponents"></a>オプションコンポーネントのインストール
 最初のインストール時に選択していない可能性のあるコンポーネントをインストールする場合は、次の手順を実行します。

#### <a name="to-install-optional-components"></a>オプションコンポーネントをインストールするには

1. **[コントロール パネル]** の **[プログラムと機能]** ページで、1 つまたは複数のコンポーネントを追加する製品のエディションを選択し、 **[変更]** を選択します。

2. セットアップ ウィザードで、 **[変更]** を選択し、インストールするコンポーネントを選択します。

3. **[次へ]** を選択し、残りの指示に従います。

## <a name="helpContent"></a> オフラインのヘルプ コンテンツのインストール
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]をインストールした後、オフラインで使用できるように、追加のヘルプ コンテンツをダウンロードすることができます。

#### <a name="to-install-or-uninstall-help-content"></a>ヘルプ コンテンツをインストールまたはアンインストールするには

1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] メニュー バーで、 **[ヘルプ]** 、 **[ヘルプ コンテンツの追加と削除]** の順にクリックします。

2. **[Microsoft ヘルプ ビューア―]** の **[コンテンツの管理]** タブで、ヘルプ コンテンツのインストール ソースを選択します。

3. 特定のヘルプ コレクションを検索する場合は、 **[検索]** ボックスに名前やキーワードを入力し、**Enter** キーを押します。

4. 必要なヘルプ コレクションの横で、 **[追加]** または **[削除]** リンクをクリックします。

5. **[更新]** ボタンをクリックします。

   オフラインヘルプをインストールまたは展開する方法の詳細については、[ヘルプビューアーの管理者ガイド](../ide/help-viewer-administrator-guide.md)を参照してください。

## <a name="serviceReleases"></a> サービス リリースと製品の更新プログラムのチェック
 すべての拡張機能に互換性があるわけではないので、以前のバージョンからアップグレードするときに、Visual Studio は拡張機能を自動的にアップグレードしません。 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)またはソフトウェアパブリッシャーから拡張機能を再インストールする必要があります。

#### <a name="to-automatically-check-for-service-releases"></a>サービス リリースを自動的に確認するには

1. メニュー バーの **[ツール]** 、 **[オプション]** の順にクリックします。

2. **[オプション]** ダイアログ ボックスの **[環境]** を展開し、 **[拡張機能と更新プログラム]** をクリックします。 **[更新プログラムを自動的にチェックする]** チェック ボックスが選択されていることを確認し、 **[OK]** をクリックします。

## <a name="registering-visual-studio"></a>Visual Studio の登録

1. メニュー バーで、 **[ヘルプ]** 、 **[バージョン情報]** の順にクリックします。

     **[バージョン情報]** ダイアログ ボックスに製品 ID 番号 (PID) が表示されます。 製品を登録するには、PID と Windows アカウントの資格情報 (Hotmail や Outlook.com などの電子メール アドレスとパスワード) が必要です。

2. メニュー バーで、 **[ヘルプ]** 、 **[製品の登録]** の順に選択します。

## <a name="repair"></a> Visual Studio の修復

#### <a name="to-repair-visual-studio"></a>Visual Studio を修復するには

1. **[コントロール パネル]** の **[プログラムと機能]** ページで、修復する製品のエディションを選択し、 **[変更]** を選択します。

2. セットアップ ウィザードで、 **[修復]** 、 **[次へ]** の順に選択し、残りの指示に従います。

#### <a name="to-repair-visual-studio-in-silent-or-passive-modes-that-is-to-repair-from-source"></a>サイレントモードまたはパッシブモードで Visual Studio を修復する (つまり、ソースから修復する) には

1. Visual Studio がインストールされているコンピューターで、Windows コマンド プロンプトを開きます。

2. 次のパラメーターを入力します。

     *DVDRoot* \\< インストールファイル\> \</quiet&#124;/passive > [/norestart]/Repair

## <a name="troubleshooting"></a>インストールのトラブルシューティング
 セットアップとインストールの問題に対して次のリソースを使用します。

- 「[Visual Studio Setup and Installation (Visual Studio のセットアップとインストール)](https://go.microsoft.com/fwlink/?LinkID=151190) 」フォーラム。 Visual Studio コミュニティでは、他のユーザーからの質問と回答を閲覧できます。 必要な情報が見つからない場合は、自分で質問してください。

- 「[Microsoft Support for Visual Studio (Visual Studio 用の Microsoft サポート)](https://go.microsoft.com/fwlink/?LinkID=251019) 」Web サイト。 サポート技術情報 (KB) の文書を読むことや、Visual Studio のインストールに関する問題について Microsoft サポートに問い合わせる方法を知ることができます。

## <a name="relatedTopics"></a> 関連トピック

|タイトル|説明|
|-----------|-----------------|
|[Visual Studio のオフライン インストールを作成する](../install/create-an-offline-installation-of-visual-studio.md)|インターネットに接続していない場合に Visual Studio をインストールする方法について説明します。
|[複数バージョンの Visual Studio をインストールする](../install/install-visual-studio-versions-side-by-side.md)|同じコンピューターに複数バージョンの Visual Studio をインストールする方法について説明します。|
|[コマンド ライン パラメーターを使用して Visual Studio をインストールする](/visualstudio/install/use-command-line-parameters-to-install-visual-studio)|コマンドプロンプトから Visual Studio をインストールするときに使用できるコマンドラインパラメーターの一覧を示します。|
|[Visual Studio のアンインストール](../install/uninstall-visual-studio.md)|Visual Studio をアンインストールする方法について説明します。|
|[Visual Studio 管理者ガイド](../install/visual-studio-administrator-guide.md)|Visual Studio の配置オプションについて説明します。|
|[Visual Studio Image Library](../designers/the-visual-studio-image-library.md)|Visual Studio アプリケーションで使用できるグラフィックスをインストールする方法について説明します。|
|[Visual Studio を使用した開発の開始](../ide/get-started-developing-with-visual-studio.md)|Visual Studio をより効果的に使用するために役立つ情報とリンクが含まれています。|

## <a name="see-also"></a>関連項目

- [Visual Studio へのサインイン](../ide/signing-in-to-visual-studio.md)
