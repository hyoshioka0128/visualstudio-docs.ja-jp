---
title: 'チュートリアル: Visual Studio 拡張機能を発行する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a34260124baedeba297dbd64e8a2c1856b55ec5a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697136"
---
# <a name="walkthrough-publish-a-visual-studio-extension"></a>チュートリアル: 拡張機能を発行します。

このチュートリアルでは、Visual Studio 拡張機能を Visual Studio マーケットプレースに発行する方法を示します。 Marketplace に拡張機能を追加すると、開発者は**拡張機能と更新プログラム**を使用して、新しい拡張機能や更新された拡張機能を参照できます。

## <a name="prerequisites"></a>必須コンポーネント

 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-visual-studio-extension"></a>拡張機能を作成する

この記事では、既定の VSPackage 拡張機能を使用しますが、手順は、拡張機能のすべての種類に有効です。

1. メニュー コマンドを持つ名前の`TestPublish`C# で VSPackage を作成します。 詳細については、「[最初の拡張機能を作成する: Hello World](../extensibility/extensibility-hello-world.md)」を参照してください。

## <a name="package-your-extension"></a>拡張機能をパッケージ化する

1. 製品名、作成者、およびバージョンに関する正しい情報を使用して、拡張子 *.vsixmanifest*を更新します。

   ![拡張機能の vsixmanifest を更新します。](media/update-extension-vsixmanifest.png)

2. **リリース**モードで拡張機能をビルドします。 これで、\bin\Release フォルダーに拡張機能が VSIX としてパッケージ化されます。

3. VSIX をダブルクリックして、インストールを確認できます。

## <a name="test-the-extension"></a>拡張機能をテストする

 拡張機能を配布する前に、ビルドしてテストし、Visual Studio の実験用インスタンスに正しくインストールされていることを確認します。

1. Visual Studio でデバッグを開始し、Visual Studio の実験用インスタンスを開きます。

2. 実験用の例で、[**ツール**] メニューの [**拡張機能と更新]** をクリックします。 TestPublish 拡張機能が中央のウィンドウに表示され、有効にする必要があります。

3. [**ツール**] メニューにテスト コマンドが表示されていることを確認します。

## <a name="publish-the-extension-to-the-visual-studio-marketplace"></a>拡張機能を Visual Studio マーケットプレースに発行する

1. 拡張機能のリリース バージョンがビルドされていること、および最新のバージョンであることを確認します。

2. Web ブラウザーで[、Visual Studio マーケットプレース](https://marketplace.visualstudio.com/vs)Web サイトを開きます。

3. 右上隅の [**サインイン**] をクリックします。

4. Microsoft アカウントを使用してサインインします。 Microsoft アカウントをお持ちでない場合は、この時点でアカウントを作成できます。

5. [**拡張機能の発行**] をクリックします。  このオプションを選択すると、すべての拡張機能の管理ページに移動します。 発行元アカウントがない場合は、この時点で作成するように求められます。

   ![マーケットプレースへのアップロード](media/upload-to-marketplace.png)

6. 拡張機能のアップロードに使用するパブリッシャーを選択します。 左側に表示されている発行元名をクリックすると、発行元を変更できます。 [**新しい拡張機能**] をクリックし **、[Visual Studio]** を選択します。

7. **1: 拡張機能をアップロード**する VSIX ファイルを直接 Visual Studio マーケットプレースにアップロードするか、または自分の Web サイトへのリンクを追加するかを選択できます。 この例では、拡張機能*TestPublish.vsix*がアップロードされます。 拡張子をドラッグアンドドロップするか、**クリック**リンクを使用してファイルを参照します。 プロジェクトの \bin\Release フォルダーで拡張機能を探します。  **[続行]** をクリックします。

8. 2:**拡張機能の詳細を指定**する : 一部のフィールドは、拡張機能から*source.extension.vsixmanifest*ファイルから自動的に設定されます。 各詳細については、以下をご覧ください。

    * **内部名**は、拡張機能の詳細ページの URL で使用されます。 たとえば、パブリッシャー名 "myname" で拡張機能を公開し、内部名を "my extension" に指定すると、拡張機能の詳細ページの URL\.が "marketplace.visualstudio com/items?itemName=myname.myextension" になります。

    * **拡張機能の表示名**。 この名前は *、source.extension.vsixmanifest*ファイルから自動的に設定されます。

    * アップロードする拡張機能の**バージョン**番号。 このバージョンは *、source.extension.vsixmanifest*ファイルから自動的に設定されます。

    * **VSIX ID**は、拡張機能に使用する一意の識別子です。 この識別子は、拡張機能を自動更新する場合に必要です。 この識別子は *、source.extension.vsixmanifest*ファイルから自動的に設定されます。

    * **拡張機能**に使用されるロゴ。 このロゴは、指定されている場合は *、source.extension.vsixmanifest*ファイルから自動的に設定されます。

    * 拡張機能の動作の**簡単な説明**。 この説明は *、source.extension.vsixmanifest*ファイルから自動的に設定されます。

    * **概要**は、スクリーンショットや拡張機能の機能に関する詳細情報を含めるのに適した場所です。

    * **サポートされている Visual Studio バージョン**では、拡張機能が動作する Visual Studio のバージョンを選択できます。 拡張機能は、これらのバージョンにのみインストールされます。

    * ** サポートされている Visual Studio エディションを使用すると、拡張機能を使用する Visual Studio のエディションを選択できます。 拡張機能は、これらのエディションにのみインストールされます。

    * **[種類]**。 最も一般的な種類の拡張機能は **、 ツール**です。

    * **カテゴリ :** あなたの拡張子に最適な3つまでピックアップ。

    * **タグ**は、ユーザーが拡張機能を見つけやすくするためのキーワードです。 タグは、マーケットプレースでの拡張機能の検索の関連性を高めるために役立ちます。

    * **価格カテゴリ**は、拡張機能のコストです。

    * **ソース コード リポジトリ**を使用すると、ソース コードへのリンクをコミュニティと共有できます。

    * **拡張機能の Q&A を許可**すると、ユーザーは拡張機能のエントリ ページに質問を残すことができます。

9. [**アップロード&保存 ]** をクリックします。 このオプションを選択すると、パブリッシャーの管理ページに戻ります。 拡張機能はまだ公開されていません。 拡張機能を公開するには、拡張機能を右クリックし、[**公開**] を選択します。 [拡張機能の表示] を選択すると、エクステンションがどのように表示されるかを Marketplace で**確認**できます。 取得番号については、[**レポート**] をクリックします。 拡張機能を変更するには、[**編集**] をクリックします。

   ![拡張エントリメニュー](media/extension-entry-menu.png)

10. [**パブリックにする**] をクリックすると、拡張機能がパブリックになります。 拡張機能を Visual Studio マーケットプレースで検索します。

## <a name="add-additional-users-to-manage-your-publisher-account"></a>パブリッシャー アカウントを管理するユーザーを追加する

Marketplace では、パブリッシャー アカウントにアクセスして管理するためのアクセス許可を追加ユーザーに付与できます。

1. 追加ユーザーを追加するパブリッシャー アカウントに移動します。

2. [**メンバー] を**選択し、[**追加**] をクリックします。

   ![追加ユーザーの追加](media/add-users.png)

3. 追加するユーザーの電子メール アドレスを指定し、[ロールの選択] で適切なレベルのアクセス**権を**付与できます。  次のオプションから選択できます。

   * **作成者**: ユーザーは拡張機能を公開できますが、他のユーザーが公開した拡張機能を表示または管理することはできません。

   * **閲覧者**: ユーザーは拡張機能を表示できますが、拡張機能の発行や管理はできません。

   * **投稿者**: ユーザーは拡張機能を公開および管理できますが、発行者設定の編集やアクセスの管理はできません。

   * **所有者**: ユーザーは、拡張機能の公開と管理、発行者設定の編集、およびアクセスの管理を行うことができます。

## <a name="install-the-extension-from-the-visual-studio-marketplace"></a>拡張機能を Visual Studio マーケットプレースからインストールする

拡張機能が発行された後、Visual Studio にインストールして、そこでテストします。

1. Visual Studio の [**ツール**] メニューの [**拡張機能と更新プログラム**] をクリックします。

2. [**オンライン**] をクリックし、[**発行のテスト**] を検索します。

3. **[Download]** をクリックします。 その後、拡張機能はインストールのスケジュールが設定されます。

4. インストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

## <a name="remove-the-extension"></a>拡張機能を削除する

拡張機能は、Visual Studio マーケットプレースおよびコンピューターから削除できます。

### <a name="to-remove-the-extension-from-the-visual-studio-marketplace"></a>拡張機能をビジュアル スタジオ マーケットプレースから削除するには

1. ビジュアル[スタジオ マーケットプレース](https://marketplace.visualstudio.com/vs)Web サイトを開きます。

2. 右上隅にある [拡張機能の**発行**] をクリックします。 発行に使用した発行元を選択**します**。 **テスト発行**の一覧が表示されます。

3. 拡張機能のエントリを右クリックし、[**削除**] をクリックします。 拡張機能を削除するかどうかの確認を求められます。 **[OK]** をクリックします。

### <a name="to-remove-the-extension-from-your-computer"></a>コンピューターから拡張機能を削除するには

1. Visual Studio の [**ツール**] メニューの [**拡張機能と更新プログラム**] をクリックします。

2. [**発行のテスト**] を選択し、[**アンインストール**] をクリックします。 その後、拡張機能はアンインストールのスケジュールに入ります。

3. アンインストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。
