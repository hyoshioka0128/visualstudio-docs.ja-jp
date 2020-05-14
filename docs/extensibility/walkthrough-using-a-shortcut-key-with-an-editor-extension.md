---
title: 'チュートリアル: エディター拡張機能でショートカット キーを使用する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 651598c0dbe746a9a26a6d60ce72b02853f98d47
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697150"
---
# <a name="walkthrough-use-a-shortcut-key-with-an-editor-extension"></a>チュートリアル: エディター拡張機能でショートカット キーを使用する
エディター拡張機能のショートカット キーに応答できます。 次のチュートリアルでは、ショートカット キーを使用して、テキスト ビューにビューの表示要素を追加する方法を示します。 このチュートリアルは、ビューポート表示エディタ テンプレートに基づいており、+ 文字を使用して表示要素を追加できます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>マネージ機能拡張フレームワーク (MEF) プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[**ビジュアル C# / 拡張性**] を選択し、次に**VSIX プロジェクト**を選択します)。ソリューションに名前`KeyBindingTest`を付ける:

2. エディタ テキスト表示項目テンプレートをプロジェクトに追加し、 という名前を`KeyBindingTest`付けます。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 次の参照を追加し **、CopyLocal**を に設定します`false`。

    エディター

    Microsoft.VisualStudio.OLE.Interop

    シェル.14.0

    相互運用機能

   クラス ファイルで、クラス名をパープルコーナー ボックスに変更します。 左余白に表示される電球を使用して、他の適切な変更を行います。 コンストラクター内で、表示要素レイヤーの名前を**KeyBindingTest**から**パープルコーナーボックス**に変更します。

```csharp
this.layer = view.GetAdornmentLayer("PurpleCornerBox");
```

KeyBindingTestTextViewCreationListener.csクラス ファイルで、表示要素レイヤーの名前を**キーバインドテスト**から**パープルコーナー ボックス**に変更します。

```csharp
[Export(typeof(AdornmentLayerDefinition))]
[Name("PurpleCornerBox")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
public AdornmentLayerDefinition editorAdornmentLayer;
```

## <a name="handle-typechar-command"></a>タイプ文字コマンドを処理する
Visual Studio 2017 バージョン 15.6 より前のバージョンでは、エディター拡張機能でコマンド<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>を処理する唯一の方法は、ベースのコマンド フィルターを実装していました。 Visual Studio 2017 バージョン 15.6 では、エディターのコマンド ハンドラーに基づく最新の簡略化されたアプローチが導入されました。 次の 2 つのセクションでは、従来のアプローチとモダンなアプローチの両方を使用してコマンドを処理する方法を示します。

## <a name="define-the-command-filter-prior-to-visual-studio-2017-version-156"></a>コマンド フィルターを定義する (Visual Studio 2017 バージョン 15.6 より前)

 コマンド フィルタは<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>、 の実装で、表示要素をインスタンス化してコマンドを処理します。

1. クラス ファイルを追加し、その名前を `KeyBindingCommandFilter`にします。

2. 次の using ディレクティブを追加します。

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Text.Editor;

    ```

3. という名前のクラスを継承<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>する必要があります。

    ```csharp
    internal class KeyBindingCommandFilter : IOleCommandTarget
    ```

4. テキスト ビューのプライベート フィールド、コマンド チェーンの次のコマンド、およびコマンド フィルタが既に追加されているかどうかを示すフラグを追加します。

    ```csharp
    private IWpfTextView m_textView;
    internal IOleCommandTarget m_nextTarget;
    internal bool m_added;
    internal bool m_adorned;
    ```

5. テキスト ビューを設定するコンストラクターを追加します。

    ```csharp
    public KeyBindingCommandFilter(IWpfTextView textView)
    {
        m_textView = textView;
        m_adorned = false;
    }
    ```

6. メソッドを`QueryStatus()`次のように実装します。

    ```csharp
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)
    {
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);
    }
    ```

7. プラス記号`Exec()`( )**+** 文字が入力されている場合に、ビューに紫色のボックスが追加されるようにメソッドを実装します。

    ```csharp
    int IOleCommandTarget.Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)
    {
        if (m_adorned == false)
        {
            char typedChar = char.MinValue;

            if (pguidCmdGroup == VSConstants.VSStd2K && nCmdID == (uint)VSConstants.VSStd2KCmdID.TYPECHAR)
            {
                typedChar = (char)(ushort)Marshal.GetObjectForNativeVariant(pvaIn);
                if (typedChar.Equals('+'))
                {
                    new PurpleCornerBox(m_textView);
                    m_adorned = true;
                }
            }
        }
        return m_nextTarget.Exec(ref pguidCmdGroup, nCmdID, nCmdexecopt, pvaIn, pvaOut);
    }

    ```

## <a name="add-the-command-filter-prior-to-visual-studio-2017-version-156"></a>コマンド フィルターを追加する (Visual Studio 2017 バージョン 15.6 より前)
 表示要素プロバイダーは、テキスト ビューにコマンド フィルターを追加する必要があります。 この例では、プロバイダーは<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>、テキスト ビューの作成イベントをリッスンするを実装します。 この表示要素プロバイダーは、表示要素の Z オーダーを定義する表示要素レイヤーもエクスポートします。

1. ファイルに次の using ディレクティブを追加します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio.Utilities;
    using Microsoft.VisualStudio.Editor;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.TextManager.Interop;

    ```

2. テキスト ビュー アダプターを取得するには、 を<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>インポートする必要があります。

    ```csharp
    [Import(typeof(IVsEditorAdaptersFactoryService))]
    internal IVsEditorAdaptersFactoryService editorFactory = null;

    ```

3. メソッドを<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>変更して、 を追加`KeyBindingCommandFilter`します。

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));
    }
    ```

4. ハンドラー`AddCommandFilter`は、テキスト ビュー アダプターを取得し、コマンド フィルターを追加します。

    ```csharp
    void AddCommandFilter(IWpfTextView textView, KeyBindingCommandFilter commandFilter)
    {
        if (commandFilter.m_added == false)
        {
            //get the view adapter from the editor factory
            IOleCommandTarget next;
            IVsTextView view = editorFactory.GetViewAdapter(textView);

            int hr = view.AddCommandFilter(commandFilter, out next);

            if (hr == VSConstants.S_OK)
            {
                commandFilter.m_added = true;
                 //you'll need the next target for Exec and QueryStatus
                if (next != null)
                commandFilter.m_nextTarget = next;
            }
        }
    }
    ```

## <a name="implement-a-command-handler-starting-in-visual-studio-2017-version-156"></a>コマンド ハンドラーを実装する (Visual Studio 2017 バージョン 15.6 以降)

まず、最新のエディター API を参照するようにプロジェクトの Nuget 参照を更新します。

1. プロジェクトを右クリックし **、[Nuget パッケージの管理**] を選択します。

2. **Nuget パッケージ マネージャー**で、[**更新**] タブを選択し、[**すべてのパッケージを選択**する] チェック ボックスをオンにして、[**更新**] を選択します。

コマンド ハンドラーは、 の<xref:Microsoft.VisualStudio.Commanding.ICommandHandler%601>実装で、表示要素をインスタンス化することによってコマンドを処理します。

1. クラス ファイルを追加し、その名前を `KeyBindingCommandHandler`にします。

2. 次の using ディレクティブを追加します。

   ```csharp
   using Microsoft.VisualStudio.Commanding;
   using Microsoft.VisualStudio.Text.Editor;
   using Microsoft.VisualStudio.Text.Editor.Commanding.Commands;
   using Microsoft.VisualStudio.Utilities;
   using System.ComponentModel.Composition;
   ```

3. という名前のクラスは`ICommandHandler<TypeCharCommandArgs>`から継承し、 として<xref:Microsoft.VisualStudio.Commanding.ICommandHandler>エクスポートする必要があります。

   ```csharp
   [Export(typeof(ICommandHandler))]
   [ContentType("text")]
   [Name("KeyBindingTest")]
   internal class KeyBindingCommandHandler : ICommandHandler<TypeCharCommandArgs>
   ```

4. コマンド ハンドラーの表示名を追加します。

   ```csharp
   public string DisplayName => "KeyBindingTest";
   ```

5. メソッドを`GetCommandState()`次のように実装します。 このコマンド ハンドラーはコア エディターの TYPECHAR コマンドを処理するため、コマンドを有効にするコマンドをコア エディターにデリゲートできます。

   ```csharp
   public CommandState GetCommandState(TypeCharCommandArgs args)
   {
       return CommandState.Unspecified;
   }
   ```

6. プラス記号`ExecuteCommand()`( )**+** 文字が入力されている場合に、ビューに紫色のボックスが追加されるようにメソッドを実装します。

   ```csharp
   public bool ExecuteCommand(TypeCharCommandArgs args, CommandExecutionContext executionContext)
   {
       if (args.TypedChar == '+')
       {
           bool alreadyAdorned = args.TextView.Properties.TryGetProperty(
               "KeyBindingTextAdorned", out bool adorned) && adorned;
           if (!alreadyAdorned)
           {
               new PurpleCornerBox((IWpfTextView)args.TextView);
               args.TextView.Properties.AddProperty("KeyBindingTextAdorned", true);
           }
       }

       return false;
   }
   ```

   7. 表示レイヤー定義*KeyBindingTestTextViewCreationListener.cs*ファイルから*KeyBindingCommandHandler.cs*にコピーし、*ファイルKeyBindingTestTextViewCreationListener.cs*削除します。

   ```csharp
   /// <summary>
   /// Defines the adornment layer for the adornment. This layer is ordered
   /// after the selection layer in the Z-order.
   /// </summary>
   [Export(typeof(AdornmentLayerDefinition))]
   [Name("PurpleCornerBox")]
   [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
   private AdornmentLayerDefinition editorAdornmentLayer;
   ```

## <a name="make-the-adornment-appear-on-every-line"></a>すべての行に表示要素を表示する

元の表示要素は、テキスト ファイル内のすべての文字 'a' に表示されます。 **+** 文字に応答して表示要素を追加するようにコードを変更したので、文字が入力された行にのみ表示要素が**+** 追加されます。 装飾コードを変更して、表示要素がすべての 'a' にもう一度表示されるようにすることができます。

*KeyBindingTest.cs*ファイルで、'a' 文字を`CreateVisuals()`装飾するビュー内のすべての行を反復処理するメソッドを変更します。

```csharp
private void CreateVisuals(ITextViewLine line)
{
    IWpfTextViewLineCollection textViewLines = this.view.TextViewLines;

    foreach (ITextViewLine textViewLine in textViewLines)
    {
        if (textViewLine.ToString().Contains("a"))
        {
            // Loop through each character, and place a box around any 'a'
            for (int charIndex = textViewLine.Start; charIndex < textViewLine.End; charIndex++)
            {
                if (this.view.TextSnapshot[charIndex] == 'a')
                {
                    SnapshotSpan span = new SnapshotSpan(this.view.TextSnapshot, Span.FromBounds(charIndex, charIndex + 1));
                    Geometry geometry = textViewLines.GetMarkerGeometry(span);
                    if (geometry != null)
                    {
                        var drawing = new GeometryDrawing(this.brush, this.pen, geometry);
                        drawing.Freeze();

                        var drawingImage = new DrawingImage(drawing);
                        drawingImage.Freeze();

                        var image = new Image
                        {
                            Source = drawingImage,
                        };

                        // Align the image with the top of the bounds of the text geometry
                        Canvas.SetLeft(image, geometry.Bounds.Left);
                        Canvas.SetTop(image, geometry.Bounds.Top);

                        this.layer.AddAdornment(AdornmentPositioningBehavior.TextRelative, span, null, image, null);
                    }
                }
            }
        }
    }
}
```

## <a name="build-and-test-the-code"></a>コードのビルドとテスト

1. KeyBindingTest ソリューションをビルドし、実験用インスタンスで実行します。

2. テキスト ファイルを作成するか、開きます。 文字 'a' を含む単語を入力し**+**、テキスト ビューの任意の場所に入力します。

     ファイル内のすべての 'a' 文字に紫色の四角形が表示されます。
