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
|![Visual Studio のダウンロード](../install/media/downloads.png "ダウンロード") |**Downloads**: To install Visual Studio 2015, you can download a product executable file from the  [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) page (subscription required), or use the installation media from the boxed product. [Learn more about how to download current or previous versions of Visual Studio](https://www.visualstudio.com/vs/older-downloads/).|
|![Learn more about features](../install/media/features.png "フィーチャー") |**Features**: To learn  more about the features in Visual Studio 2015, see the release notes for [RTM](https://www.visualstudio.com/news/vs2015-vs), [Update 1](https://www.visualstudio.com/news/vs2015-update1-vs), [Update 2](https://www.visualstudio.com/news/vs2015-update2-vs), and [Update 3](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs).|
|![Find out what's in each SKU](../install/media/sku.png "SKU") |**SKU**: Visual Studio 2015 の各エディションで提供しているものについては、「[Visual Studio 製品の比較](https://go.microsoft.com/fwlink/?LinkID=242142)」ページを参照してください。|
|![View system requirements](../install/media/system-requirements.png "システム要件") |**System Requirements**: To view the system requirements for each edition of Visual Studio 2015, see the [Visual Studio 2015 Compatibility](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs) page.|
|![Locate your Product Key](../install/media/product-keys.png "プロダクト キー") |**Product Keys**: To locate your product key, see the [How to: Locate the Visual Studio Product Key](../install/how-to-locate-the-visual-studio-product-key.md) topic.|
|![Find out about licensing](../install/media/licensing.png "ライセンス") |**Licensing**: To find out about licensing options for both individuals or enterprise customers, see  the [Visual Studio and MSDN Licensing](https://www.microsoft.com/download/details.aspx?id=13350) white paper.|

## <a name="custom"></a> Default vs. Custom Setup
 Visual Studio 2015 をインストールするときに、日常的に使用するコンポーネントを含めたり除外したりできます。 一般的に、既定のインストールはカスタム インストールよりサイズが小さく、インストールにかかる時間も短くなります。 また、以前のバージョンで既定でインストールされていたコンポーネントの多数が、このバージョンでは、明示的に選択する必要があるカスタム コンポーネントと見なされるようになりました。

 ![Visual Studio 2015 Setup Dialog](../ide/media/vs2015-setup-screen.png "VS2015_Setup_screen")

 カスタム コンポーネントに含まれるのは、Visual C++、Visual F#、SQL Server Data Tools、クロス プラットフォームのモバイル ツールおよび SDK、サード パーティの SDK、拡張機能などです。 カスタム コンポーネントはいずれも、初期セットアップ時に選択しなくても後でインストールすることができます。

> [!NOTE]
> カスタム インストールには、既定のインストールに含まれるコンポーネントが自動的に組み込まれます。

 カスタム コンポーネントの完全な一覧は、次のとおりです。

|Feature Sets|コンポーネント|
|------------------|----------------|
|**更新**|Visual Studio 2015 更新プログラム 3|
|**プログラミング言語**|Visual C++<br />Visual F#<br />Python Tools for Visual Studio|
|**Windows 開発および Web 開発**|ClickOnce 発行ツール<br />LightSwitch<br />Microsoft Office Developer Tools<br />Microsoft SQL Server Data Tools<br /> Microsoft Web Developer Tools<br />PowerShell Tools for Visual Studio (3rd Party)<br />Silverlight 開発キット<br />ユニバーサル Windows アプリ開発ツール<br />Windows 10 のツールおよび SDK<br />Windows 8.1 および Windows Phone 8.0/8.1 ツール<br />Windows 8.1 のツールおよび SDK|
|**クロス プラットフォームのモバイル開発**|C#/.NET (Xamarin)<br />HTML/JavaScript (Apache Cordova)<br />iOS/Android 向け Visual C++ モバイル開発<br />Clang with Microsoft CodeGen|
|**Common Tools and Software Development Kits**|Android Native Development Kit (3rd Party)<br /> Android SDK [3rd Party]<br />Android SDK Setup APIs (3rd Party)<br />Apache Ant (3rd Party)<br /> Java SE Development Kit (3rd Party)<br /> Joyent Node.js (3rd Party)|
|**一般的なツール**|Git for Windows (3rd Party)<br />GitHub Extension for Visual Studio (3rd Party)<br /> Visual Studio 機能拡張ツール|

## <a name="installing"></a> Visual Studio のインストール
 You can install Visual Studio by using installation media (DVDs), by using your Visual Studio subscription service from the [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) website, by downloading  a web installer from the [Visual Studio Downloads](https://go.microsoft.com/fwlink/?LinkId=517106) website, or by creating an offline installation layout (see the [Create an Offline Installation of Visual Studio](../install/create-an-offline-installation-of-visual-studio.md) page for more details).

> [!IMPORTANT]
> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]をインストールするには、管理者の資格情報が必要です。 ただしインストール後、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の使用には不要です。

 Visual Studio のすべてをインストールするには、ローカル管理者アカウントの次の特権が有効になっている必要があります。

|ローカル ポリシー オブジェクト表示名|ユーザー権限|
|--------------------------------------|----------------|
|ファイルとディレクトリのバックアップ|SeBackupPrivilege|
|プログラムのデバッグ|SeDebugPrivilege|
|監査ログとセキュリティ ログの管理|SeSecurityPrivilege|

 ローカル管理者アカウントの要件の詳細については、サポート技術情報「 [セットアップ アカウントに特定のユーザー権限がない場合、SQL Server のインストールが失敗する](https://support.microsoft.com/kb/2000257)」を参照してください。

### <a name="BKMK_Media"></a> Using installation media
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]をインストールするには、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] インストール メディアのルート ディレクトリで、必要なエディションのインストール ファイルを実行します。

|エディション|インストール ファイル|
|-------------|-----------------------|
|Visual Studio Enterprise|vs_enterprise.exe|
|Visual Studio Professional|vs_professional.exe|
|Visual Studio コミュニティ|vs_community.exe|

### <a name="BKMK_Website"></a> Downloading from the product website
 Visit the [Visual Studio Downloads](https://go.microsoft.com/fwlink/?LinkId=517106) page, and select the edition of Visual Studio that you want.

### <a name="downloading-from-your-subscription-service"></a>Downloading from your subscription service
 Visit  the [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) page, and select the edition of Visual Studio that you want.

### <a name="BKMK_Offline"></a> Creating an offline installation layout
 If you do not have the [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] installation media, or you do not have a Visual Studio subscription,  or you do not want to install [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] by using the web installer, you can perform a "disconnected" installation by creating what is known as an offline installation layout. For more information, see the [Create an Offline Installation of Visual Studio](../install/create-an-offline-installation-of-visual-studio.md) page.

## <a name="enterprise"></a> Deploying Visual Studio in an Enterprise
 For information about how to deploy [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] over a network, see the [Visual Studio Administrator Guide](../install/visual-studio-administrator-guide.md).

### <a name="BKMK_Virtualized"></a> Installing Visual Studio in a virtualized environment
 **Hyper-V に関するビデオの問題**

 Hyper-V が有効であり、アクセラレータ機能を使用するグラフィックス アダプターが搭載されている Windows Server 2008 R2 を実行すると、システムの速度が低下することがあります。

 詳細については、Microsoft Web サイトの「 [Video performance may decrease when a Windows Server 2008 or Windows Server 2008 R2 based computer has the Hyper-V role enabled and an accelerated display adapter installed (Windows Server 2008 または Windows Server 2008 R2 ベースのコンピューターで Hyper-V の役割を有効にし、アクセラレータ機能を使用するディスプレイ アダプターをインストールしたときに、ビデオ パフォーマンスが低下する場合がある)](https://go.microsoft.com/fwlink/?LinkID=231084)」を参照してください。

 **Hyper-V によるデバイスのエミュレート**

 仮想化を使わずに Visual Studio 2015 を実際のハードウェアにインストールする場合、Hyper-V を使用して Windows デバイスと Android デバイスのエミュレーションを有効にする機能を選択できます。 HYPER-V にインストールすると、Windows デバイスまたは Android デバイスをエミュレートできなくなります。 これは、エミュレーター自体が仮想マシンであり、現時点では別の VM の内部で VM をホストすることができないためです。 回避策として、アプリケーションを直接デプロイおよびデバッグできる実際の Windows デバイスまたは Android デバイスを用意することができます。

## <a name="optionalComponents"></a> Installing optional components
 If you want to install components that you might not have selected during your original installation, use the following procedure.

#### <a name="to-install-optional-components"></a>To install optional components

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

5. Click the **Update** button.

   For more information about how to install or deploy offline Help, see the [Help Viewer Administrator Guide](../ide/help-viewer-administrator-guide.md).

## <a name="serviceReleases"></a> サービス リリースと製品の更新プログラムのチェック
 すべての拡張機能に互換性があるわけではないので、以前のバージョンからアップグレードするときに、Visual Studio は拡張機能を自動的にアップグレードしません。 You must reinstall the extensions from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/) or from the software publisher.

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

#### <a name="to-repair-visual-studio-in-silent-or-passive-modes-that-is-to-repair-from-source"></a>To repair Visual Studio in silent or passive modes (that is, to repair from source)

1. Visual Studio がインストールされているコンピューターで、Windows コマンド プロンプトを開きます。

2. 次のパラメーターを入力します。

     *DVDRoot* \\<Installation File\> \</quiet&#124;/passive> [/norestart]/Repair

## <a name="troubleshooting"></a> Troubleshooting an installation
 セットアップとインストールの問題に対して次のリソースを使用します。

- 「[Visual Studio Setup and Installation (Visual Studio のセットアップとインストール)](https://go.microsoft.com/fwlink/?LinkID=151190) 」フォーラム。 Visual Studio コミュニティでは、他のユーザーからの質問と回答を閲覧できます。 必要な情報が見つからない場合は、自分で質問してください。

- 「[Microsoft Support for Visual Studio (Visual Studio 用の Microsoft サポート)](https://go.microsoft.com/fwlink/?LinkID=251019) 」Web サイト。 サポート技術情報 (KB) の文書を読むことや、Visual Studio のインストールに関する問題について Microsoft サポートに問い合わせる方法を知ることができます。

## <a name="relatedTopics"></a> 関連トピック

|Title|説明|
|-----------|-----------------|
|[Visual Studio のオフライン インストールを作成する](../install/create-an-offline-installation-of-visual-studio.md)|Describes how to install Visual Studio when you are not connected to the Internet.
|[複数バージョンの Visual Studio をインストールする](../install/install-visual-studio-versions-side-by-side.md)|同じコンピューターに複数バージョンの Visual Studio をインストールする方法について説明します。|
|[コマンド ライン パラメーターを使用して Visual Studio をインストールする](/visualstudio/install/use-command-line-parameters-to-install-visual-studio)|Lists the command-line parameters that you can use when you install Visual Studio from a command prompt.|
|[Visual Studio のアンインストール](../install/uninstall-visual-studio.md)|Describes how to uninstall Visual Studio.|
|[Visual Studio 管理者ガイド](../install/visual-studio-administrator-guide.md)|Visual Studio の配置オプションについて説明します。|
|[Visual Studio Image Library](../designers/the-visual-studio-image-library.md)|Visual Studio アプリケーションで使用できるグラフィックスをインストールする方法について説明します。|
|[Get Started Developing with Visual Studio](../ide/get-started-developing-with-visual-studio.md)|Includes information and links that can help you use Visual Studio more effectively.|

## <a name="see-also"></a>参照

- [Visual Studio へのサインイン](../ide/signing-in-to-visual-studio.md)