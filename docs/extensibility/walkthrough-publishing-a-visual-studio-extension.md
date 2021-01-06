---
title: 'チュートリアル: Visual Studio 拡張機能の発行 |Microsoft Docs'
description: Visual Studio 拡張機能を Visual Studio Marketplace に発行する方法について説明します。これにより、開発者は新しい拡張機能と更新された拡張機能を参照できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
ms.openlocfilehash: cbdd283c5d147c53e7d82843207b48d0dbf6e6e9
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877885"
---
# <a name="walkthrough-publish-a-visual-studio-extension"></a>チュートリアル: Visual Studio 拡張機能の発行

このチュートリアルでは、Visual Studio 拡張機能を Visual Studio Marketplace に発行する方法について説明します。 拡張機能を Marketplace に追加すると、開発者は **拡張機能と更新プログラム** を使用して、新しい拡張機能や更新された拡張機能を参照できます。

## <a name="prerequisites"></a>前提条件

 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-visual-studio-extension"></a>Visual Studio 拡張機能を作成する

この記事では既定の VSPackage 拡張機能を使用しますが、各種類の拡張機能に対して手順は有効です。

1. メニューコマンドを持つという名前の VSPackage を C# で作成し `TestPublish` ます。 詳細については、「 [初めての拡張機能の作成: Hello World](../extensibility/extensibility-hello-world.md)」を参照してください。

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

## <a name="publish-the-extension-to-the-visual-studio-marketplace"></a>拡張機能を Visual Studio Marketplace に発行する

1. 拡張機能のリリースバージョンがビルドされていることと、最新の状態であることを確認してください。

2. Web ブラウザーで、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) web サイトを開きます。

3. 右上隅にある [ **サインイン**] をクリックします。

4. Microsoft アカウントを使用してサインインします。 Microsoft アカウントがない場合は、この時点で作成できます。

5. [ **拡張機能の発行**] をクリックします。  このオプションを選択すると、すべての拡張機能の [管理] ページに移動します。 発行元アカウントを持っていない場合は、この時点で1つのアカウントを作成するように求められます。

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

    * * * サポートされている Visual Studio エディションでは、拡張機能が動作する Visual Studio のエディションを選択できます。 拡張機能は、これらのエディションにのみインストールされます。

    * **[種類]** 。 最も一般的な種類の拡張機能は **ツール** です。

    * **カテゴリ**。 拡張機能に最適な最大3つを選択します。

    * **タグ** は、ユーザーが拡張機能を検索するのに役立つキーワードです。 タグを使用すると、Marketplace の拡張機能の検索に関する関連性を高めることができます。

    * **価格カテゴリ** は、拡張機能のコストです。

    * **ソースコードリポジトリ** を使用すると、ソースコードへのリンクをコミュニティと共有できます。

    * **拡張機能に対して Q&A を許可すると** 、ユーザーは拡張機能のエントリページに質問を残すことができます。

9. [ **保存 & アップロード**] をクリックします。 このオプションを選択すると、パブリッシャーの [管理] ページに戻ります。 拡張機能はまだ発行されていません。 拡張機能を発行するには、拡張機能を右クリックし、[ **公開の作成**] を選択します。 [表示] [ **拡張機能**] の順に選択すると、Marketplace で拡張機能がどのように表示されるかを確認できます。 取得番号については、[ **レポート**] をクリックします。 拡張機能に変更を加えるには、[ **編集**] をクリックします。

   ![拡張機能エントリメニュー](media/extension-entry-menu.png)

10. [ **パブリック** にする] をクリックすると、拡張機能がパブリックになります。 Visual Studio Marketplace で拡張機能を検索します。

## <a name="add-additional-users-to-manage-your-publisher-account"></a>発行者アカウントを管理するユーザーを追加する

Marketplace では、発行元アカウントにアクセスして管理するための追加のユーザーのアクセス許可の付与をサポートしています。

1. 追加のユーザーを追加するパブリッシャーアカウントに移動します。

2. [ **メンバー** ] を選択し、[ **追加**] をクリックします。

   ![追加のユーザーの追加](media/add-users.png)

3. 追加するユーザーの電子メールアドレスを指定し、[ **ロールの選択**] で適切なレベルのアクセス権を付与することができます。  次のオプションから選択できます。

   * **Creator**: ユーザーは拡張機能を公開できますが、他のユーザーによって発行された拡張機能を表示または管理することはできません。

   * **閲覧** 者: ユーザーは拡張機能を表示できますが、拡張機能を公開または管理することはできません。

   * **共同作成者**: ユーザーは拡張機能を発行および管理できますが、パブリッシャーの設定を編集したり、アクセスを管理したりすることはできません。

   * **所有者**: ユーザーは、拡張機能の発行と管理、発行者設定の編集、およびアクセスの管理を行うことができます。

## <a name="install-the-extension-from-the-visual-studio-marketplace"></a>Visual Studio Marketplace から拡張機能をインストールします。

拡張機能が公開されたので、それを Visual Studio にインストールしてテストします。

1. Visual Studio の [ **ツール** ] メニューで、[ **拡張機能と更新プログラム**] をクリックします。

2. [ **オンライン** ] をクリックし、 **testpublish** を検索します。

3. **[Download]** をクリックします。 その後、拡張機能のインストールがスケジュールされます。

4. インストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

## <a name="remove-the-extension"></a>拡張機能を削除する

Visual Studio Marketplace およびコンピューターから拡張機能を削除できます。

### <a name="to-remove-the-extension-from-the-visual-studio-marketplace"></a>Visual Studio Marketplace から拡張機能を削除するには

1. [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)の web サイトを開きます。

2. 右上隅の [拡張機能の **公開** ] をクリックします。 **Testpublish** の発行に使用したパブリッシャーを選択します。 **Testpublish** の一覧が表示されます。

3. 拡張機能のエントリを右クリックし、[ **削除**] をクリックします。 拡張機能を削除するかどうかを確認するメッセージが表示されます。 **[OK]** をクリックします。

### <a name="to-remove-the-extension-from-your-computer"></a>コンピューターから拡張機能を削除するには

1. Visual Studio の [ **ツール** ] メニューで、[ **拡張機能と更新プログラム**] をクリックします。

2. [ **Testpublish** ] を選択し、[ **アンインストール**] をクリックします。 次に、拡張機能をアンインストールするようにスケジュールを設定します。

3. アンインストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。
