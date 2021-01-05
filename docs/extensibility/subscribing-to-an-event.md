---
title: イベントへのサブスクライブ |Microsoft Docs
description: Visual Studio SDK で実行中のドキュメントテーブルのイベントに応答するツールウィンドウを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- running document table (RDT), responding to events
- running document table (RDT), subscribing to events
ms.assetid: e94a4fea-94df-488e-8560-9538413422bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c739dad7be8d2a000662eca478bc117699694c8a
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715874"
---
# <a name="subscribing-to-an-event"></a>イベントのサブスクライブ
このチュートリアルでは、実行中のドキュメントテーブル (RDT) のイベントに応答するツールウィンドウを作成する方法について説明します。 ツールウィンドウは、を実装するユーザーコントロールをホストし <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> ます。 メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> インターフェイスをイベントに接続します。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="subscribing-to-rdt-events"></a>RDT イベントのサブスクライブ

#### <a name="to-create-an-extension-with-a-tool-window"></a>ツールウィンドウで拡張機能を作成するには

1. VSIX テンプレートを使用して **Rdtexplorer** という名前のプロジェクトを作成し、 **RDTExplorerWindow** という名前のカスタムツールウィンドウ項目テンプレートを追加します。

     ツールウィンドウを使用した拡張機能の作成の詳細については、「 [ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

#### <a name="to-subscribe-to-rdt-events"></a>RDT イベントをサブスクライブするには

1. RDTExplorerWindowControl ファイルを開き、という名前のボタンを削除し `button1` ます。 コントロールを追加 <xref:System.Windows.Forms.ListBox> し、既定の名前をそのまま使用します。 Grid 要素は次のようになります。

    ```xml
    <Grid>
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>
            <ListBox x:Name="listBox" Height="100" />
        </StackPanel>
    </Grid>
    ```

2. コードビューで RDTExplorerWindow.cs ファイルを開きます。 次の using ディレクティブをファイルの先頭に追加します。

    ```csharp
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. クラスの `RDTExplorerWindow` 派生に加えて、インターフェイスを実装するようにクラスを変更し <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> ます。

    ```csharp
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents
    {. . .}
    ```

4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>を実装します。

    - インターフェイスを実装します。 IVsRunningDocTableEvents 名にカーソルを置きます。 左余白に電球が表示されます。 電球の右側にある下矢印をクリックし、[ **インターフェイスの実装**] を選択します。

5. インターフェイスの各メソッドで、行を次 `throw new NotImplementedException();` のように置き換えます。

    ```csharp
    return VSConstants.S_OK;
    ```

6. RDTExplorerWindow クラスに cookie フィールドを追加します。

    ```csharp
    private uint rdtCookie;
    ```

     これは、メソッドによって返されるクッキーを保持し <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> ます。

7. RDTExplorerWindow の Initialize () メソッドをオーバーライドして、RDT イベントに登録します。 Createtoolwindow は toolwindowpane の Initialize () メソッドでは、常に、コンストラクターではなくサービスを取得する必要があります。

    ```csharp
    protected override void Initialize()
    {
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
        this.GetService(typeof(SVsRunningDocumentTable));
        rdt.AdviseRunningDocTableEvents(this, out rdtCookie);
    }
    ```

     <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>サービスは、インターフェイスを取得するために呼び出され <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>メソッドは、RDT イベントを <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> 、この場合は RDTExplorer オブジェクトを実装するオブジェクトに接続します。

8. RDTExplorerWindow の Dispose () メソッドを更新します。

    ```csharp
    protected override void Dispose(bool disposing)
    {
        // Release the RDT cookie.
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
            Package.GetGlobalService(typeof(SVsRunningDocumentTable));
        rdt.UnadviseRunningDocTableEvents(rdtCookie);

        base.Dispose(disposing);
    }
    ```

     メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A> `RDTExplorer` と rdt イベント通知の間の接続を削除します。

9. ハンドラーの本体のステートメントの直前に、次の行を追加し <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A> `return` ます。

    ```csharp
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");
        return VSConstants.S_OK;
    }
    ```

10. ハンドラーの本文 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A> と、リストボックスに表示するその他のイベントに同様の行を追加します。

    ```csharp
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");
        return VSConstants.S_OK;
    }
    ```

11. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

12. **RDTExplorerWindow** (**ビュー/その他のウィンドウ/RDTExplorerWindow**) を開きます。

     **RDTExplorerWindow** ウィンドウが開き、空のイベント一覧が表示されます。

13. ソリューションを開くか、作成します。

     `OnBeforeLastDocument`と `OnAfterFirstDocument` イベントが発生すると、各イベントの通知がイベント一覧に表示されます。
