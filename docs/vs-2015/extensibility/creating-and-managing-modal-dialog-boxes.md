---
title: モーダルダイアログボックスの作成と管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- dialog boxes, managing in Visual Studio
ms.assetid: 491bc0de-7dba-478c-a76b-923440e090f3
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 29b0066f201fbb791d471d5cfb433d9a335aa775
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62431577"
---
# <a name="creating-and-managing-modal-dialog-boxes"></a>モーダル ダイアログ ボックスの作成と管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 内でモーダルダイアログボックスを作成する場合は、ダイアログボックスが表示されている間、ダイアログボックスの親ウィンドウが無効になっていることを確認し、ダイアログボックスを閉じた後で親ウィンドウを再び有効にする必要があります。 そうしないと、"モーダルダイアログがアクティブになっているため、Microsoft Visual Studio をシャットダウンできません" というエラーが表示されることがあります。 アクティブなダイアログを閉じて、もう一度やり直してください。 "  
  
 これを行うには、2つの方法があります。 WPF ダイアログボックスがある場合は、から派生させ、を呼び出してダイアログボックスを表示することをお勧めし <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow.ShowModal%2A> ます。 これを行うと、親ウィンドウのモーダル状態を管理する必要がなくなります。  
  
 ダイアログボックスが WPF でない場合、またはその他の理由でダイアログボックスクラスをから派生できない場合は、ダイアログボックスを <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.GetDialogOwnerHwnd%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.EnableModeless%2A> 表示する前にパラメーター 0 (false) を指定してメソッドを呼び出し、ダイアログボックスを閉じた後にパラメーター 1 (true) を指定してメソッドを呼び出すことによって、ダイアログボックスの親を取得する必要が  
  
## <a name="creating-a-dialog-box-derived-from-dialogwindow"></a>ダイアログボックスを作成して表示ウィンドウから派生する  
  
1. **Open/test**という名前の VSIX プロジェクトを作成し、 **opendialog**という名前のメニューコマンドを追加します。 これを行う方法の詳細については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。  
  
2. クラスを使用するには、 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> [ **参照の追加** ] ダイアログボックスの [フレームワーク] タブで、次のアセンブリへの参照を追加する必要があります。  
  
    - PresentationCore  
  
    - PresentationFramework  
  
    - WindowsBase  
  
    - System.Xaml  
  
3. OpenDialog.cs で、次のステートメントを追加し `using` ます。  
  
    ```csharp  
    using Microsoft.VisualStudio.PlatformUI;  
    ```  
  
4. から派生した **Test表示ウィンドウ** という名前のクラスを宣言し <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> ます。  
  
    ```csharp  
    class TestDialogWindow : DialogWindow  
    {. . .}  
    ```  
  
5. ダイアログボックスを最小化して最大化できるようにするには、 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMaximizeButton%2A> とを <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMinimizeButton%2A> true に設定します。  
  
    ```csharp  
    internal TestDialogWindow()  
    {  
        this.HasMaximizeButton = true;  
        this.HasMinimizeButton = true;  
    }  
    ```  
  
6. **Opendialog ShowMessageBox**メソッドで、既存のコードを次のコードに置き換えます。  
  
    ```csharp  
    TestDialogWindow testDialog = new TestDialogWindow();  
    testDialog.ShowModal();  
    ```  
  
7. アプリケーションをビルドして実行します。 Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの [ **ツール** ] メニューに、 **Invoke opendialog**という名前のコマンドが表示されます。 このコマンドをクリックすると、ダイアログウィンドウが表示されます。 ウィンドウを最小化して最大化できるようになります。  
  
## <a name="creating-and-managing-a-dialog-box-not-derived-from-dialogwindow"></a>ダイアログボックスの作成と管理 ([プロパティ] ウィンドウから派生しない)  
  
1. この手順では、同じアセンブリ参照を使用して、前の手順で作成した **Openのテスト** ソリューションを使用できます。  
  
2. 次の宣言を追加し `using` ます。  
  
    ```csharp  
    using System.Windows;  
    using Microsoft.Internal.VisualStudio.PlatformUI;  
    ```  
  
3. から派生する **TestDialogWindow2** という名前のクラスを作成し <xref:System.Windows.Window> ます。  
  
    ```csharp  
    class TestDialogWindow2 : Window  
    {. . .}  
    ```  
  
4. にプライベート参照を追加し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ます。  
  
    ```  
    private IVsUIShell shell;  
    ```  
  
5. への参照を設定するコンストラクターを追加し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ます。  
  
    ```csharp  
    public TestDialogWindow2(IVsUIShell uiShell)  
    {  
        shell = uiShell;  
    }  
    ```  
  
6. **Opendialog ShowMessageBox**メソッドで、既存のコードを次のコードに置き換えます。  
  
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
  
7. アプリケーションをビルドして実行します。 [ **ツール** ] メニューの [ **Opendialog の呼び出し]** という名前のコマンドが表示されます。 このコマンドをクリックすると、ダイアログウィンドウが表示されます。
