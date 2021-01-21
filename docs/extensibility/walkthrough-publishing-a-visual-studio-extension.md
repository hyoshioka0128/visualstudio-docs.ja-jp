---
title: 'チュートリアル: Visual Studio 拡張機能の発行 |Microsoft Docs'
description: Visual Studio 拡張機能を Visual Studio Marketplace に発行する方法について説明します。これにより、開発者は、新しい拡張機能と更新された拡張機能を参照できます。
ms.custom: SEO-VS-2020
ms.date: 01/15/2021
ms.topic: how-to
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 01a46f54bfbce6126c16fa418d5c4bef53afd09b
ms.sourcegitcommit: 7a5c4f60667b5792f876953d55192b49a73f5fe9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98533918"
---
# <a name="walkthrough-publish-a-visual-studio-extension"></a>チュートリアル: Visual Studio 拡張機能の発行

このチュートリアルでは、Visual Studio 拡張機能を Visual Studio Marketplace に発行する方法について説明します。 拡張機能を Visual Studio Marketplace に追加すると、開発者は **拡張機能と更新プログラム** を使用して、新しい拡張機能や更新された拡張機能を参照できます。

## <a name="prerequisites"></a>前提条件

 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-visual-studio-extension"></a>Visual Studio 拡張機能を作成する

この記事では既定の VSPackage 拡張機能を使用しますが、各種類の拡張機能に対して手順は有効です。

- メニューコマンドを持つという名前の VSPackage を C# で作成し `TestPublish` ます。 詳細については、「 [初めての拡張機能の作成: Hello World](../extensibility/extensibility-hello-world.md)」を参照してください。

## <a name="package-your-extension"></a>拡張機能をパッケージ化する

1. 製品名、作成者、およびバージョンに関する正しい情報を使用して *source.extension.vsixmanifest* を更新します。

   ![拡張機能 source.extension.vsixmanifest の更新](media/update-extension-vsixmanifest.png)

2. **リリース** モードで拡張機能をビルドします。 これで、拡張機能は \bin\Release フォルダーに VSIX としてパッケージ化されます。

3. VSIX をダブルクリックして、インストールを確認できます。

## <a name="test-the-extension"></a>拡張機能をテストする

 拡張機能を配布する前に、Visual Studio の実験用インスタンスに正しくインストールされていることを確認するために、拡張機能をビルドしてテストします。

1. Visual Studio で、デバッグを開始して、Visual Studio の実験用インスタンスを開きます。

2. 実験用インスタンスで、[ **ツール** ] メニューの [ **拡張機能と更新プログラム**] をクリックします。 TestPublish 拡張機能が中央のウィンドウに表示され、有効になります。

3. [ **ツール** ] メニューで、[テスト] コマンドが表示されていることを確認します。

## <a name="publish-the-extension-to-visual-studio-marketplace"></a>拡張機能を Visual Studio Marketplace に発行します

1. 拡張機能のリリースバージョンがビルドされていることと、最新の状態であることを確認してください。

2. Web ブラウザーで、[ [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)にアクセスします。

3. 右上隅にある [ **サインイン**] をクリックします。

4. Microsoft アカウントを使用してサインインします。 Microsoft アカウントがない場合は、この時点で作成できます。

5. [ **拡張機能の発行**] をクリックします。 このオプションを選択すると、すべての拡張機能の [管理] ページに移動します。 発行元アカウントを持っていない場合は、この時点で1つのアカウントを作成するように求められます。

   ![Marketplace にアップロード](media/upload-to-marketplace.png)

6. 拡張機能のアップロードに使用する発行元を選択します。 左側に一覧表示されている発行元の名前をクリックして、パブリッシャーを変更できます。 [ **新しい拡張機能** ] をクリックし、[ **Visual Studio**] を選択します。

7. **1: 拡張子をアップロード** すると、VSIX ファイルを Visual Studio Marketplace に直接アップロードしたり、自分の web サイトへのリンクを追加したりすることができます。 この例では、拡張機能の *Testpublish* がアップロードされます。 拡張機能をドラッグアンドドロップするか、 **クリック** リンクを使用してファイルを参照します。 プロジェクトの \bin\Release フォルダーで拡張機能を見つけます。  **[続行]** をクリックします。

8. **2: 拡張機能の詳細を指定** すると、一部のフィールドが *source.extension.vsixmanifest* ファイルから自動的に設定されます。 詳細については、以下を参照してください。

    * **内部名** は、拡張機能の詳細ページの URL で使用されます。 たとえば、発行者名 "myname" の下にある拡張機能を発行し、"my extension" という内部名を指定すると、 \. 拡張機能の詳細ページの URL が "marketplace. visualstudio com/items? itemName = myname" になります。

    * 拡張機能の **表示名**。 この名前は、 *source.extension.vsixmanifest* ファイルから自動的に設定されます。

    * アップロードする拡張機能の **バージョン** 番号。 このバージョンは、 *source.extension.vsixmanifest* ファイルから自動的に設定されます。

    * **VSIX ID** は、Visual Studio が拡張機能に使用する一意の識別子です。 拡張機能が自動更新されるようにする場合は、この識別子が必要です。 この識別子は、 *source.extension.vsixmanifest* ファイルから自動的に設定されます。

    * 拡張機能に使用される **ロゴ**。 このロゴは、 *source.extension.vsixmanifest* ファイルから自動的に設定されます (指定されている場合)。

    * 拡張機能についての **簡単な説明**。 この説明は、 *source.extension.vsixmanifest* ファイルから自動的に設定されます。

    * **概要** は、スクリーンショット、および拡張機能の動作に関する詳細情報を含めるのに適した場所です。

    * **サポートされている Visual studio のバージョン** では、拡張機能で使用する visual studio のバージョンを選択できます。 拡張機能は、これらのバージョンにのみインストールされます。

    * **サポートされている Visual studio エディション** では、拡張機能が動作する visual studio のエディションを選択できます。 拡張機能は、これらのエディションにのみインストールされます。

    * **[種類]** 。 最も一般的な種類の拡張機能は **ツール** です。

    * **カテゴリ**。 拡張機能に最適な最大3つを選択します。

    * **タグ** は、ユーザーが拡張機能を検索するのに役立つキーワードです。 タグを使用すると、Visual Studio Marketplace の拡張機能の検索に関する関連性を高めることができます。

    * **価格カテゴリ** は、拡張機能のコストです。

    * **ソースコードリポジトリ** を使用すると、ソースコードへのリンクをコミュニティと共有できます。

    * **拡張機能に対して Q&A を許可すると** 、ユーザーは拡張機能のエントリページに質問を残すことができます。

9. [ **保存 & アップロード**] をクリックします。 このオプションを選択すると、パブリッシャーの [管理] ページに戻ります。 拡張機能はまだ発行されていません。

10. 拡張機能を発行するには、拡張機能を右クリックし、[ **公開の作成**] を選択します。 拡張機能が Visual Studio Marketplace にどのように表示されるかを確認するには、[ **拡張機能の表示**] を選択します。 取得番号については、[ **レポート**] をクリックします。 拡張機能に変更を加えるには、[ **編集**] をクリックします。

    ![拡張機能エントリメニュー](media/extension-entry-menu.png)

11. [ **公開**] をクリックすると、拡張機能がパブリックになります。 拡張機能の Visual Studio Marketplace を検索します。

## <a name="update-a-published-extension-in-visual-studio-marketplace"></a>Visual Studio Marketplace で公開されている拡張機能を更新する

開始する前に、拡張機能の新しいリリースバージョンがビルドされていることと、最新の状態であることを確認してください。

1.  Web ブラウザーで、[ [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)にアクセスします。

1.  右上隅にある [ **サインイン**] をクリックし、Microsoft アカウントでサインインします。

    :::image type="content" source="media/marketplace-upload-extension.png" alt-text="ファイルエクスプローラーでアップロードされた拡張ファイルの選択を示すスクリーンショット。":::

1.  [ **拡張機能の発行**] をクリックし、更新した拡張機能のアップロードに使用するパブリッシャーを選択します。

    :::image type="content" source="media/marketplace-select-extension-version.png" alt-text="[発行の拡張機能リンクが強調表示されている Visual Studio Marketplace のスクリーンショット。":::

1.  更新する拡張機能の横にある3つの水平方向のドットの上にマウスポインターを移動し、[ **編集**] を選択します。

    :::image type="content" source="media/marketplace-select-extension.png" alt-text="編集する拡張機能の選択を示すスクリーンショット。":::

1.  **1: [拡張機能のアップロード**] で、VSIX ファイル名の後にある鉛筆アイコンをクリックして、公開されている拡張機能を編集します。

     :::image type="content" source="media/marketplace-edit-extension-details.png" alt-text="鉛筆アイコンをクリックして拡張機能を編集していることを示すスクリーンショット。":::

1.  更新された拡張機能の VSIX ファイルを参照します。 ファイルをクリックし、[ **開く**] をクリックします。

    更新された拡張機能のアップロード。

    :::image type="content" source="media/marketplace-upload-extension-notification.png" alt-text="編集した拡張機能をアップロードした後のファイルのアップロード通知のスクリーンショット。":::

1. **2: 拡張機能の詳細を指定** すると、拡張機能の更新プログラムの一部の詳細が読み取り専用になります。または、拡張機能の *source.extension.vsixmanifest* ファイルから自動的に設定されます。 拡張機能の詳細については、以下を参照してください。

    - **内部名** \*は、拡張機能の詳細ページの URL で使用されます。 たとえば、発行者名 "myname" の下に拡張機能を発行し、"my extension" という内部名を指定すると、拡張機能の詳細ページの URL が "marketplace.visualstudio.com/items?itemName=myname.myextension" になります。

    - **表示名** \*を使用します。 この名前は、 *source.extension.vsixmanifest* ファイルから自動的に設定されます。

    - **バージョン** \*アップロードしている拡張機能の番号。 このバージョンは、 *source.extension.vsixmanifest* ファイルから自動的に設定されます。

    - **VSIX ID** \*は、Visual Studio が拡張機能に使用する一意の識別子です。 拡張機能が自動更新されるようにする場合は、この識別子が必要です。 この識別子は、 *source.extension.vsixmanifest* ファイルから自動的に設定されます。

    - **ロゴ** \*これは、拡張機能で使用されます。 このロゴは、 *source.extension.vsixmanifest* ファイルから自動的に設定されます (指定されている場合)。

    - **簡単な説明** \*拡張機能を使用します。 この説明は、 *source.extension.vsixmanifest* ファイルから自動的に設定されます。

    - **概要** は、スクリーンショット、および拡張機能の動作に関する詳細情報を含めるのに適した場所です。

    - **サポートされている Visual Studio のバージョン** \*拡張機能を使用する Visual Studio のバージョンを選択できます。 拡張機能は、これらのバージョンにのみインストールされます。

    - **サポートされている Visual Studio のエディション** \*拡張機能を使用する Visual Studio のエディションを選択できます。 拡張機能は、これらのエディションにのみインストールされます。

    - **[種類]** 。 最も一般的な種類の拡張機能は **ツール** です。

    - **カテゴリ**。 拡張機能に最適な最大3つを選択します。

    - **タグ** は、ユーザーが拡張機能を検索するのに役立つキーワードです。 タグを使用すると、Visual Studio Marketplace の拡張機能の検索に関する関連性を高めることができます。

    - **価格カテゴリ** は、拡張機能のコストです。

    - **ソースコードリポジトリ** を使用すると、ソースコードへのリンクをコミュニティと共有できます。

    - **拡張機能に対して Q&A を許可すると** 、ユーザーは拡張機能のエントリページに質問を残すことができます。

       \* この詳細は、拡張機能の更新では変更できません。

1. [ **保存 & アップロード**] をクリックします。 このオプションを選択すると、パブリッシャーの [管理] ページに戻ります。 拡張機能はまだ発行されていません。

1. 拡張機能を発行するには、拡張機能を右クリックし、[ **公開の作成**] を選択します。 拡張機能が Visual Studio Marketplace にどのように表示されるかを確認するには、[ **拡張機能の表示**] を選択します。 [取得番号] で、[ **レポート**] をクリックします。 拡張機能に変更を加えるには、[ **編集**] をクリックします。

## <a name="add-additional-users-to-manage-your-publisher-account"></a>発行者アカウントを管理するユーザーを追加する

Visual Studio Marketplace では、パブリッシャーアカウントにアクセスして管理するための追加のユーザーのアクセス許可の付与がサポートされています。

1. 追加のユーザーを追加するパブリッシャーアカウントに移動します。

2. [ **メンバー** ] を選択し、[ **追加**] をクリックします。

   ![追加のユーザーの追加](media/add-users.png)

3. 追加するユーザーの電子メールアドレスを指定し、[ **ロールの選択**] で適切なレベルのアクセス権を付与することができます。  次のオプションから選択できます。

   * **Creator**: ユーザーは拡張機能を公開できますが、他のユーザーによって発行された拡張機能を表示または管理することはできません。

   * **閲覧** 者: ユーザーは拡張機能を表示できますが、拡張機能を公開または管理することはできません。

   * **共同作成者**: ユーザーは拡張機能を発行および管理できますが、パブリッシャーの設定を編集したり、アクセスを管理したりすることはできません。

   * **所有者**: ユーザーは、拡張機能の発行と管理、発行者設定の編集、およびアクセスの管理を行うことができます。

## <a name="install-the-extension-from-visual-studio-marketplace"></a>Visual Studio Marketplace から拡張機能をインストールする

拡張機能が公開されたので、それを Visual Studio にインストールしてテストします。

1. Visual Studio の [ **ツール** ] メニューで、[ **拡張機能と更新プログラム**] をクリックします。

2. [ **オンライン** ] をクリックし、 **testpublish** を検索します。

3. **[Download]** をクリックします。 その後、拡張機能のインストールがスケジュールされます。

4. インストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

## <a name="remove-the-extension"></a>拡張機能を削除する

この拡張機能は、Visual Studio Marketplace とコンピューターから削除できます。

### <a name="to-remove-the-extension-from-visual-studio-marketplace"></a>拡張機能を Visual Studio Marketplace から削除するには

1. [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)にアクセスします。

2. 右上隅の [拡張機能の **公開** ] をクリックします。 **Testpublish** の発行に使用したパブリッシャーを選択します。 **Testpublish** の一覧が表示されます。

3. 拡張機能のエントリを右クリックし、[ **削除**] をクリックします。 拡張機能を削除するかどうかを確認するメッセージが表示されます。 **[OK]** をクリックします。

### <a name="to-remove-the-extension-from-your-computer"></a>コンピューターから拡張機能を削除するには

1. Visual Studio の [ **ツール** ] メニューで、[ **拡張機能と更新プログラム**] をクリックします。

2. [ **Testpublish** ] を選択し、[ **アンインストール**] をクリックします。 次に、拡張機能をアンインストールするようにスケジュールを設定します。

3. アンインストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。
