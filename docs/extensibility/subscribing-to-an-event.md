---
title: イベントの購読 |マイクロソフトドキュメント
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
ms.openlocfilehash: 6aefe2efce897aefc26f63835844b0cc705fb5b1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699682"
---
# <a name="subscribing-to-an-event"></a>イベントのサブスクライブ
このチュートリアルでは、実行中のドキュメント テーブル (RDT) 内のイベントに応答するツール ウィンドウを作成する方法について説明します。 ツール ウィンドウは、 を実装するユーザー<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>コントロールをホストします。 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>メソッドは、インターフェイスをイベントに接続します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="subscribing-to-rdt-events"></a>RDT イベントのサブスクライブ

#### <a name="to-create-an-extension-with-a-tool-window"></a>ツール ウィンドウを使用して拡張機能を作成するには

1. VSIX テンプレートを使用して**RDTExplorer**という名前のプロジェクトを作成し **、RDTExplorerWindow**という名前のカスタム ツール ウィンドウ項目テンプレートを追加します。

     ツール ウィンドウを使用した拡張機能の作成の詳細については、「ツール[ウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

#### <a name="to-subscribe-to-rdt-events"></a>RDT イベントをサブスクライブするには

1. ファイルを開き、 という名前`button1`のボタンを削除します。 コントロールを<xref:System.Windows.Forms.ListBox>追加し、既定の名前をそのまま使用します。 Grid 要素は次のようになります。

    ```xml
    <Grid>
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>
            <ListBox x:Name="listBox" Height="100" />
        </StackPanel>
    </Grid>
    ```

2. RDTExplorerWindow.cs ファイルをコード ビューで開きます。 ファイルの先頭に次の using ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. クラスから`RDTExplorerWindow`派生するだけでなく、インターフェイスを実装するように<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>クラスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>変更します。

    ```csharp
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents
    {. . .}
    ```

4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>を実装します。

    - インターフェイスを実装します。 名前にカーソルを置きます。 左余白に電球が表示されます。 電球の右にある下矢印をクリックし、[**インターフェイスを実装**] を選択します。

5. インターフェイスの各メソッドで、次の行`throw new NotImplementedException();`を次のように置き換えます。

    ```csharp
    return VSConstants.S_OK;
    ```

6. クラスにクッキー フィールドを追加します。

    ```csharp
    private uint rdtCookie;
    ```

     メソッドによって返される Cookie が<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>保持されます。

7. RDT イベントに登録するには、RDTExplorerWindow の初期化() メソッドをオーバーライドします。 コンストラクタではなく、常に ToolWindowPane の Initialize() メソッドでサービスを取得する必要があります。

    ```csharp
    protected override void Initialize()
    {
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
        this.GetService(typeof(SVsRunningDocumentTable));
        rdt.AdviseRunningDocTableEvents(this, out rdtCookie);
    }
    ```

     インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>を取得するために、サービスが<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>呼び出されます。 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>メソッドは、RDTExplorer オブジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>を実装するオブジェクトに RDT イベントを接続します。

8. メソッドを更新します。

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

     この<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A>メソッドは、RDT`RDTExplorer`イベント通知との間の接続を削除します。

9. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A>ステートメントの直前のハンドラー本体に次の行を`return`追加します。

    ```csharp
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");
        return VSConstants.S_OK;
    }
    ```

10. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A>ハンドラーの本体と、リスト ボックスに表示する他のイベントに、同様の行を追加します。

    ```csharp
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");
        return VSConstants.S_OK;
    }
    ```

11. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

12. を開きます **(** **表示 / その他のウィンドウ / RDTエクスプローラウィンドウ**).

     **[RDTExplorerWindow] ウィンドウ**が開き、空のイベント リストが表示されます。

13. ソリューションを開くか、または作成します。

     イベント`OnBeforeLastDocument`と`OnAfterFirstDocument`イベントが発生すると、各イベントの通知がイベントリストに表示されます。
