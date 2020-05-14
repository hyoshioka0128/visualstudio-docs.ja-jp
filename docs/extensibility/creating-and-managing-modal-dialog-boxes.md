---
title: モーダル ダイアログ ボックスの作成と管理 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dialog boxes, managing in Visual Studio
ms.assetid: 491bc0de-7dba-478c-a76b-923440e090f3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 786a2fbe2b75c51420668eb1ab6f596213d3da9b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739497"
---
# <a name="create-and-manage-modal-dialog-boxes"></a>モーダル ダイアログ ボックスの作成と管理
Visual Studio 内でモーダル ダイアログ ボックスを作成する場合は、ダイアログ ボックスが表示されている間、ダイアログ ボックスの親ウィンドウが無効になっていることを確認し、ダイアログ ボックスを閉じた後で親ウィンドウを再度有効にする必要があります。 これを行わない場合は、*モーダル ダイアログがアクティブであるため、Microsoft Visual Studio をシャットダウンできませんというエラーが表示されることがあります。アクティブなダイアログを閉じてから、やり直してください。*

これを行う方法は2つあります。 WPF ダイアログ ボックスがある場合は、<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>から派生し、ダイアログ ボックスを表示するために呼<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow.ShowModal%2A>び出すことをお勧めします。 これを行う場合は、親ウィンドウのモーダル状態を管理する必要はありません。

ダイアログ ボックスが WPF でない場合、または何らかの理由で<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>ダイアログ ボックス クラスを派生できない場合は、モーダル状態を呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.GetDialogOwnerHwnd%2A>して自分で管理し、ダイアログ ボックスを表示<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.EnableModeless%2A>する前にメソッドを 0 (false) で呼び出し、ダイアログ ボックスを閉じた後にメソッドを 1 (true) のパラメータで再度呼び出して、ダイアログ ボックスの親を取得する必要があります。

## <a name="create-a-dialog-box-derived-from-dialogwindow"></a>ダイアログ ウィンドウから派生したダイアログ ボックスを作成する

1. という名前の VSIX プロジェクトを作成し **、****メニュー**コマンドを追加します。 これを行う方法の詳細については、「メニュー[コマンドを使用して拡張機能を作成する」を](../extensibility/creating-an-extension-with-a-menu-command.md)参照してください。

2. クラスを<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>使用するには、次のアセンブリへの参照を追加する必要があります ([**参照の追加**] ダイアログ ボックスの [フレームワーク] タブ)。

    - *PresentationCore*

    - *PresentationFramework*

    - *WindowsBase*

    - *System.Xaml*

3. *OpenDialog.cs*で、次`using`のステートメントを追加します。

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    ```

4. から<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>派生するクラス`TestDialogWindow`を宣言します。

    ```csharp
    class TestDialogWindow : DialogWindow
    {. . .}
    ```

5. ダイアログ ボックスを最小化および最大化できるようにするには、次の値<xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMaximizeButton%2A>を<xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMinimizeButton%2A>設定し、true に設定します。

    ```csharp
    internal TestDialogWindow()
    {
        this.HasMaximizeButton = true;
        this.HasMinimizeButton = true;
    }
    ```

6. メソッドで`OpenDialog.ShowMessageBox`、既存のコードを次のコードに置き換えます。

    ```csharp
    TestDialogWindow testDialog = new TestDialogWindow();
    testDialog.ShowModal();
    ```

7. アプリケーションをビルドして実行します。 Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの **[ツール**] メニューに **、[OpenDialog を呼び出す]** というコマンドが表示されます。 このコマンドをクリックすると、ダイアログ ウィンドウが表示されます。 ウィンドウを最小化し、最大化できるはずです。

## <a name="create-and-manage-a-dialog-box-not-derived-from-dialogwindow"></a>ダイアログ ウィンドウから派生していないダイアログ ボックスを作成および管理する

1. この手順では、前の手順で作成した**OpenDialogTest**ソリューションを同じアセンブリ参照で使用できます。

2. 次`using`の宣言を追加します。

    ```csharp
    using System.Windows;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    ```

3. から<xref:System.Windows.Window>派生するクラス`TestDialogWindow2`を作成します。

    ```csharp
    class TestDialogWindow2 : Window
    {. . .}
    ```

4. プライベート参照を に<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>追加します。

    ```
    private IVsUIShell shell;
    ```

5. 参照を設定するコンストラクターを追加します<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>。

    ```csharp
    public TestDialogWindow2(IVsUIShell uiShell)
    {
        shell = uiShell;
    }
    ```

6. メソッドで`OpenDialog.ShowMessageBox`、既存のコードを次のコードに置き換えます。

    ```csharp
    IVsUIShell uiShell = (IVsUIShell)ServiceProvider.GetService(typeof(SVsUIShell));

    TestDialogWindow2 testDialog2 = new TestDialogWindow2(uiShell);
    //get the owner of this dialog
    IntPtr hwnd;
    uiShell.GetDialogOwnerHwnd(out hwnd);
    testDialog2.WindowStartupLocation = System.Windows.WindowStartupLocation.CenterOwner;
    uiShell.EnableModeless(0);
    try
    {
        WindowHelper.ShowModal(testDialog2, hwnd);
    }
    finally
    {
        // This will take place after the window is closed.
        uiShell.EnableModeless(1);
    }
    ```

7. アプリケーションをビルドして実行します。 [**ツール**] メニューに、[**開くダイアログを呼び出す]** というコマンドが表示されます。 このコマンドをクリックすると、ダイアログ ウィンドウが表示されます。
