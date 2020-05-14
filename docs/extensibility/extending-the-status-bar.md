---
title: ステータス バーを拡張する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- status bars, about status bars
- status bars, overview
ms.assetid: f955115c-4c5f-45ec-b41b-365868c5ec0c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa62326d82d81f7ee4d10a838209364355cc488e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711539"
---
# <a name="extend-the-status-bar"></a>ステータス バーを拡張する
IDE の下部にある Visual Studio ステータス バーを使用して、情報を表示できます。

 ステータス バーを拡張すると、フィードバック領域、進行状況バー、アニメーション領域、デザイナー領域の 4 つの領域に情報と UI を表示できます。 フィードバック領域では、テキストを表示し、表示されたテキストを強調表示することができます。 進行状況バーには、ファイルの保存など、実行時間の短い操作の進行状況が増分で表示されます。 アニメーション領域には、長時間実行される操作や、ソリューション内に複数のプロジェクトを構築するなど、未定の長さの操作を行うための連続ループアニメーションが表示されます。 デザイナー領域には、カーソル位置の行番号と列番号が表示されます。

 ステータス バーは、(<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar><xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>サービスから) インターフェイスを使用して取得できます。 さらに、ウィンドウ フレーム上に置かれたオブジェクトは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>インターフェイスを実装することでステータス バー クライアント オブジェクトとして登録できます。 ウィンドウがアクティブ化されるたびに、Visual Studio はそのウィンドウに置き込まれるオブジェクトに`IVsStatusbarUser`インターフェイスを照会します。 見つかった場合は、返<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>されたインターフェイスのメソッドを呼び出し、オブジェクトはそのメソッド内からステータス バーを更新できます。 たとえば、ドキュメント ウィンドウは、このメソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>を使用して、デザイナー領域の情報がアクティブになったときに更新できます。

 次の手順では、VSIX プロジェクトを作成し、カスタム メニュー コマンドを追加する方法を理解していることを前提としています。 詳細については、[メニュー コマンドを使用した拡張機能の作成を](../extensibility/creating-an-extension-with-a-menu-command.md)参照してください。

## <a name="modify-the-status-bar"></a>ステータス バーを変更する
 この手順では、テキストの設定と取得、静的テキストの表示、ステータス バーのフィードバック領域での表示テキストの強調表示の方法を示します。

### <a name="read-and-write-to-the-status-bar"></a>ステータス バーの読み取りと書き込み

1. という名前の VSIX プロジェクト**を**作成し、という名前のメニュー コマンド**を追加します**。

2. *TestStatusBarCommand.cs*で、コマンド ハンドラ メソッド`MenuItemCallback`コード ( ) を次のように置き換えます。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));

        // Make sure the status bar is not frozen
        int frozen;

        statusBar.IsFrozen(out frozen);

        if (frozen != 0)
        {
            statusBar.FreezeOutput(0);
        }

        // Set the status bar text and make its display static.
        statusBar.SetText("We just wrote to the status bar.");

        // Freeze the status bar.
        statusBar.FreezeOutput(1);

        // Get the status bar text.
        string text;
        statusBar.GetText(out text);
        System.Windows.Forms.MessageBox.Show(text);

        // Clear the status bar text.
        statusBar.FreezeOutput(0);
        statusBar.Clear();
    }
    ```

3. コードをコンパイルし、デバッグを開始します。

4. Visual Studio の実験用インスタンスで **[ツール**] メニューを開きます。 [**テストステータスバー コマンドの呼び出し] ボタンを**クリックします。

     ステータス バーのテキストが[ステータス バーに**書き込んだばかり**]と表示されます。 表示されるメッセージ ボックスには同じテキストが表示されます。

### <a name="update-the-progress-bar"></a>進行状況バーを更新する

1. この手順では、進行状況バーを初期化および更新する方法を示します。

2. *TestStatusBarCommand.cs*ファイルを開き、`MenuItemCallback`メソッドを次のコードに置き換えます。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));
        uint cookie = 0;
        string label = "Writing to the progress bar";

        // Initialize the progress bar.
        statusBar.Progress(ref cookie, 1, "", 0, 0);

        for (uint i = 0, total = 20; i <= total; i++)
        {
            // Display progress every second.
            statusBar.Progress(ref cookie, 1, label, i, total);
            System.Threading.Thread.Sleep(1000);
        }

        // Clear the progress bar.
        statusBar.Progress(ref cookie, 0, "", 0, 0);
    }
    ```

3. コードをコンパイルし、デバッグを開始します。

4. Visual Studio の実験用インスタンスで **[ツール**] メニューを開きます。 [**テストステータスバーコマンドの呼び出し]** ボタンをクリックします。

     ステータス バーのテキストが**進行状況バーへの書き込みを**読み上げていることがわかります。 また、プログレスバーが毎秒20秒間更新されるのも確認できます。 その後、ステータスバーとプログレスバーがクリアされます。

### <a name="display-an-animation"></a>アニメーションを表示する

1. ステータス バーには、実行時間の長い操作 (たとえば、ソリューションで複数のプロジェクトを構築する操作) を示すループ アニメーションが表示されます。 このアニメーションが表示されない場合は、次の設定が正しい**ツール** > **オプション**を使用してください。

     [**ツール** > **オプション** > の**全般**] タブに移動し、[**クライアントのパフォーマンスに基づいて視覚的なエクスペリエンスを自動的に調整する**] チェック ボックスをオフにします。 次に、サブオプションの [**リッチ クライアントのビジュアル エクスペリエンスを有効にする**] をオンにします。 Visual Studio の実験用インスタンスでプロジェクトをビルドするときにアニメーションを表示できるようになりました。

     この手順では、プロジェクトまたはソリューションのビルドを表す標準の Visual Studio アニメーションを表示します。

2. *TestStatusBarCommand.cs*ファイルを開き、`MenuItemCallback`メソッドを次のコードに置き換えます。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar =(IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));

        // Use the standard Visual Studio icon for building.
        object icon = (short)Microsoft.VisualStudio.Shell.Interop.Constants.SBAI_Build;

        // Display the icon in the Animation region.
        statusBar.Animation(1, ref icon);

        // The message box pauses execution for you to look at the animation.
        System.Windows.Forms.MessageBox.Show("showing?");

        // Stop the animation.
        statusBar.Animation(0, ref icon);
    }
    ```

3. コードをコンパイルし、デバッグを開始します。

4. Visual Studio の実験用インスタンスで **[ツール**] メニューを開き **、[TestStatusBarCommand の呼び出し**] をクリックします。

     メッセージ ボックスが表示されたら、右端のステータス バーにもアニメーションが表示されます。 メッセージ ボックスを閉じると、アニメーションが消えます。
