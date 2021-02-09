---
title: ステータスバーの拡張 |Microsoft Docs
description: IDE の下部にある Visual Studio のステータスバーを拡張して、情報を表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- status bars, about status bars
- status bars, overview
ms.assetid: f955115c-4c5f-45ec-b41b-365868c5ec0c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7776c7fa35cd7ac06dec60ced3604cb67c96da4a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903194"
---
# <a name="extend-the-status-bar"></a>ステータスバーを拡張する
IDE の下部にある Visual Studio のステータスバーを使用して、情報を表示できます。

 ステータスバーを拡張すると、フィードバック領域、進行状況バー、アニメーション領域、およびデザイナー領域の4つの領域に情報と UI を表示できます。 フィードバック領域では、テキストを表示したり、表示されているテキストを強調表示したりすることができます。 進行状況バーには、ファイルの保存など、実行時間の短い操作の進行状況が表示されます。 アニメーション領域には、ソリューション内での複数のプロジェクトのビルドなど、長時間実行される操作や不定な長さの操作に対して、連続ループアニメーションが表示されます。 デザイナー領域には、カーソル位置の行番号と列番号が表示されます。

 ステータスバーは、(サービスの) インターフェイスを使用して取得でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> ます。 また、ウィンドウフレームに配置されているオブジェクトは、インターフェイスを実装することによって、ステータスバークライアントオブジェクトとして登録でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> ます。 ウィンドウがアクティブになるたびに、Visual Studio はそのウィンドウに配置されているオブジェクトにインターフェイスを照会し `IVsStatusbarUser` ます。 見つかった場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> 返されたインターフェイスでメソッドを呼び出します。オブジェクトは、そのメソッド内からステータスバーを更新できます。 たとえば、ドキュメントウィンドウでは、メソッドを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> デザイナー領域がアクティブになったときに情報を更新できます。

 次の手順では、VSIX プロジェクトを作成し、カスタムメニューコマンドを追加する方法について理解していることを前提としています。 詳細については、「 [メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

## <a name="modify-the-status-bar"></a>ステータスバーを変更する
 この手順では、ステータスバーのフィードバック領域にテキストを設定して取得し、静的なテキストを表示し、表示されているテキストを強調表示する方法について説明します。

### <a name="read-and-write-to-the-status-bar"></a>ステータスバーの読み取りと書き込み

1. **TestStatusBarExtension** という名前の VSIX プロジェクトを作成し、 **TestStatusBarCommand** という名前のメニューコマンドを追加します。

2. *TestStatusBarCommand.cs* で、コマンドハンドラーのメソッドコード () を次のコードに置き換え `MenuItemCallback` ます。

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

4. Visual Studio の実験用インスタンスで [ **ツール** ] メニューを開きます。 [ **Invoke TestStatusBarCommand** ] ボタンをクリックします。

     ステータスバーのテキストが、**ステータスバーに書き込んだばかり** のものであることがわかります。 表示されるメッセージボックスには同じテキストが表示されます。

### <a name="update-the-progress-bar"></a>進行状況バーを更新する

1. この手順では、進行状況バーを初期化して更新する方法について説明します。

2. *TestStatusBarCommand.cs* ファイルを開き、メソッドを `MenuItemCallback` 次のコードに置き換えます。

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

4. Visual Studio の実験用インスタンスで [ **ツール** ] メニューを開きます。 [ **TestStatusBarCommand の呼び出し** ] ボタンをクリックします。

     ステータスバーのテキストが **進行状況バーへの書き込み** を読み取ることがわかります。 また、進行状況バーが20秒間、1秒ごとに更新されていることがわかります。 その後、ステータスバーと進行状況バーがクリアされます。

### <a name="display-an-animation"></a>アニメーションを表示する

1. ステータスバーには、実行時間の長い操作 (ソリューションでの複数のプロジェクトのビルドなど) を示すループアニメーションが表示されます。 このアニメーションが表示されない場合は、適切な **ツール**  >  **オプション** の設定があることを確認してください。

     [**ツール**  >  **]**  >  **[オプション] [全般**] タブにアクセスし、 **[クライアントのパフォーマンスに基づいて視覚的効果を自動的に調整** する] をオフにします。 次に、[ **リッチクライアントの視覚エクスペリエンスを有効にする**] サブオプションをオンにします。 これで、Visual Studio の実験用インスタンスでプロジェクトをビルドするときにアニメーションが表示されるようになります。

     この手順では、プロジェクトまたはソリューションのビルドを表す標準の Visual Studio アニメーションを表示します。

2. *TestStatusBarCommand.cs* ファイルを開き、メソッドを `MenuItemCallback` 次のコードに置き換えます。

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

4. 実験用インスタンスの Visual Studio で [ **ツール** ] メニューを開き、[ **TestStatusBarCommand の呼び出し**] をクリックします。

     メッセージボックスが表示されたら、右端にあるステータスバーにもアニメーションが表示されます。 メッセージボックスを閉じると、アニメーションは表示されなくなります。
