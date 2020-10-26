---
title: 拡張機能を公開する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5238274d66296a21e15b47d1a090ab01c1a1299d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201978"
---
# <a name="walkthrough-publishing-a-visual-studio-extension"></a>チュートリアル: Visual Studio の拡張機能を発行する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**注**: Visual Studio ギャラリーは Visual Studio Marketplace に置き換えられています。 詳細については、このトピックの最新バージョンを参照してください。

このチュートリアルでは、visual studio の拡張機能を Visual Studio ギャラリーに発行する方法について説明します。 拡張機能をギャラリーに追加すると、開発者は **拡張機能と更新プログラム** を使用して、新しい拡張機能や更新された拡張機能を参照できます。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="create-a-visual-studio-extension"></a>Visual Studio 拡張機能を作成する
 この場合は、既定の VSPackage 拡張機能を使用しますが、すべての種類の拡張機能に対して同じ手順が有効です。

1. メニューコマンドを持つという名前の VSPackage を C# で作成し `TestPublishing` ます。 詳細については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

## <a name="test-the-extension"></a>拡張機能をテストする
 拡張機能を配布する前に、ビルドしてテストし、Visual Studio の実験用インスタンスに正しくインストールされていることを確認します。

1. Visual Studio で、デバッグを開始します。 Visual Studio の実験用インスタンスを開くには

2. 実験用インスタンスで、[ **ツール** ] メニューの [ **拡張機能マネージャー**] をクリックします。 TestPublishing 拡張機能が中央のウィンドウに表示され、有効になります。

3. [ **ツール** ] メニューで、[テスト] コマンドが表示されていることを確認します。

## <a name="publish-the-extension-to-the-visual-studio-gallery"></a>拡張機能を Visual Studio ギャラリーに発行する
 これで、拡張機能を Visual Studio ギャラリーに発行できるようになりました。

1. 拡張機能のリリースバージョンがビルドされていることと、最新の状態であることを確認してください。

2. Web ブラウザーで、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) web サイトを開きます。

3. 右上隅にある [ **サインイン**] をクリックします。

4. Microsoft アカウントを使用してサインインします。 Microsoft アカウントがない場合は、この時点で作成できます。

5. **[アップロード]** をクリックします。

6. [ **手順 1: 拡張機能の種類**] で、[ **ツール** ] を選択し、[ **次へ**] をクリックします。

7. [ **手順 2: アップロード**] で、Visual Studio ギャラリーに直接アップロードするか、独自の web サイトへのリンクを追加するかを選択できます。 この場合は、[ **ツールをアップロード**します] を選択します。 **[コントロールの選択**] ボックスが表示されます。 [ **参照** ] をクリックし、プロジェクトの \bin\Release フォルダーにある testpublish .vsix を選択します。 **[次へ]** をクリックします。

8. **「手順 3: 基本情報**」では、source.extension.vsixmanifest ファイルのフィールドが表示されます。 適切な **カテゴリ** を選択し、ユーザーが拡張機能を検索できるように **タグ** を追加します。 より詳細な概要と説明を追加することもできます (説明は280文字以上である必要があります)。 **拡張機能**の種類**は、Microsoft の拡張機能**や**コストカテゴリ**ではなく、**試用版**のままにしておいてください。

9. ページの下部にある投稿物契約を読み、[ **同意**する] をオンにします。

10. [ **投稿の作成**] をクリックします。 これにより、拡張機能によって Visual Studio ギャラリーに表示されるページが表示され、ページがまだ発行されていないというメッセージが表示されます。

11. **[発行]** をクリックします。

12. Visual Studio ギャラリーで拡張機能を検索します。 TestPublish 拡張機能の一覧が表示されます。

## <a name="install-the-extension-from-the-visual-studio-gallery"></a>Visual Studio ギャラリーから拡張機能をインストールする
 拡張機能が公開されたので、それを Visual Studio にインストールしてテストします。

1. Visual Studio の [ **ツール** ] メニューで、[ **拡張機能と更新プログラム**] をクリックします。

2. [ **オンライン** ] をクリックし、testpublish を検索します。 TestPublish 拡張機能の一覧が表示されます。

3. **[Download]** をクリックします。 拡張機能をダウンロードした後、 **[インストール]** をクリックします。

4. インストールを完了するには、Visual Studio を再起動します。

## <a name="removing-the-extension"></a>拡張機能を削除しています
 拡張機能は、Visual Studio ギャラリーとコンピューターから削除できます。

#### <a name="to-remove-the-extension-from-the-visual-studio-gallery"></a>Visual Studio ギャラリーから拡張機能を削除するには

1. [Visual Studio Marketplace](https://marketplace.visualstudio.com/)の web サイトを開きます。

2. 右上隅にある [ **My Extenions**] をクリックします。 TestPublish の一覧が表示されます。

3. **[削除]** をクリックします。

#### <a name="to-remove-the-extension-from-your-computer"></a>コンピューターから拡張機能を削除するには

1. Visual Studio の **[ツール]** メニューで、 **[拡張機能マネージャー]** をクリックします。

2. [TestPublish] を選択し、[ **アンインストール**] をクリックします。

3. アンインストールを完了するには、Visual Studio を再起動します。
