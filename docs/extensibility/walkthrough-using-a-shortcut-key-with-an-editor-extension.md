---
title: エディター拡張機能でショートカットキーを使用する
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6dcbf5c22af9cabeca0b89ffa98d4ddf86173a4a
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89735151"
---
# <a name="walkthrough-use-a-shortcut-key-with-an-editor-extension"></a>チュートリアル: エディター拡張機能でのショートカットキーの使用
エディター拡張機能のショートカットキーに応答できます。 次のチュートリアルでは、ショートカットキーを使用して、ビューの表示要素をテキストビューに追加する方法について説明します。 このチュートリアルは、ビューポートの表示要素エディターテンプレートに基づいており、+ 文字を使用して表示要素を追加できます。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `KeyBindingTest` します。

2. エディターのテキスト表示項目テンプレートをプロジェクトに追加し、という名前を指定 `KeyBindingTest` します。 詳細については、「 [エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 次の参照を追加し、 **CopyLocal** をに設定し `false` ます。

    VisualStudio

    Microsoft.VisualStudio.OLE.Interop

    VisualStudio. 14.0

    VisualStudio。相互運用

   KeyBindingTest クラスファイルで、クラス名を PurpleCornerBox に変更します。 左余白に表示される電球を使用して、その他の適切な変更を行います。 コンストラクター内で、装飾層の名前を **Keybindingtest** から **PurpleCornerBox**に変更します。

```csharp
this.layer = view.GetAdornmentLayer("PurpleCornerBox");
```

KeyBindingTestTextViewCreationListener.cs クラスファイルで、AdornmentLayer の名前を **Keybindingtest** から **PurpleCornerBox**に変更します。

```csharp
[Export(typeof(AdornmentLayerDefinition))]
[Name("PurpleCornerBox")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
public AdornmentLayerDefinition editorAdornmentLayer;
```

## <a name="handle-typechar-command"></a>TYPECHAR コマンドの処理
Visual Studio 2017 バージョン15.6 より前では、エディター拡張機能のコマンドを処理する唯一の方法は、ベースのコマンドフィルターを実装することでした <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。 Visual Studio 2017 バージョン15.6 では、エディターのコマンドハンドラーに基づく、最新の簡略化された方法が導入されました。 次の2つのセクションでは、従来の方法と最新の方法の両方を使用してコマンドを処理する方法を示します。

## <a name="define-the-command-filter-prior-to-visual-studio-2017-version-156"></a>コマンドフィルターを定義します (Visual Studio 2017 バージョン15.6 より前)

 コマンドフィルターは、を実装したもので <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 、装飾をインスタンス化することによってコマンドを処理します。

1. クラス ファイルを追加し、その名前を `KeyBindingCommandFilter`にします。

2. 次の using ディレクティブを追加します。

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Text.Editor;

    ```

3. KeyBindingCommandFilter という名前のクラスは、から継承する必要があり <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。

    ```csharp
    internal class KeyBindingCommandFilter : IOleCommandTarget
    ```

4. テキストビューのプライベートフィールド、コマンドチェーンの次のコマンド、およびコマンドフィルターが既に追加されているかどうかを示すフラグを追加します。

    ```csharp
    private IWpfTextView m_textView;
    internal IOleCommandTarget m_nextTarget;
    internal bool m_added;
    internal bool m_adorned;
    ```

5. テキストビューを設定するコンストラクターを追加します。

    ```csharp
    public KeyBindingCommandFilter(IWpfTextView textView)
    {
        m_textView = textView;
        m_adorned = false;
    }
    ```

6. 次のように、メソッドを実装し `QueryStatus()` ます。

    ```csharp
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)
    {
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);
    }
    ```

7. `Exec()`プラス記号 ( **+** ) 文字が入力されている場合に、ビューに紫色のボックスを追加するように、メソッドを実装します。

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

## <a name="add-the-command-filter-prior-to-visual-studio-2017-version-156"></a>コマンドフィルターを追加します (Visual Studio 2017 バージョン15.6 より前)
 表示要素プロバイダーは、コマンドフィルターをテキストビューに追加する必要があります。 この例では、プロバイダーがを実装して、 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> テキストビュー作成イベントをリッスンします。 この装飾プロバイダーは、装飾の Z オーダーを定義する、装飾層もエクスポートします。

1. Keybindingtesttextviewのファイルに、次の using ディレクティブを追加します。

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

2. テキストビューアダプターを取得するには、をインポートする必要があり <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> ます。

    ```csharp
    [Import(typeof(IVsEditorAdaptersFactoryService))]
    internal IVsEditorAdaptersFactoryService editorFactory = null;

    ```

3. を <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> 追加するようにメソッドを変更し `KeyBindingCommandFilter` ます。

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));
    }
    ```

4. `AddCommandFilter`ハンドラーはテキストビューアダプターを取得し、コマンドフィルターを追加します。

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

## <a name="implement-a-command-handler-starting-in-visual-studio-2017-version-156"></a>コマンドハンドラーを実装します (Visual Studio 2017 バージョン15.6 以降)

最初に、最新のエディター API を参照するようにプロジェクトの Nuget 参照を更新します。

1. プロジェクトを右クリックし、[ **Nuget パッケージの管理**] を選択します。

2. **Nuget パッケージマネージャー**で、[**更新プログラム**] タブを選択し、[**すべてのパッケージを選択**] チェックボックスをオンにして、[**更新**] を選択します。

コマンドハンドラーは、の実装であり <xref:Microsoft.VisualStudio.Commanding.ICommandHandler%601> 、装飾をインスタンス化することによってコマンドを処理します。

1. クラス ファイルを追加し、その名前を `KeyBindingCommandHandler`にします。

2. 次の using ディレクティブを追加します。

   ```csharp
   using Microsoft.VisualStudio.Commanding;
   using Microsoft.VisualStudio.Text.Editor;
   using Microsoft.VisualStudio.Text.Editor.Commanding.Commands;
   using Microsoft.VisualStudio.Utilities;
   using System.ComponentModel.Composition;
   ```

3. KeyBindingCommandHandler という名前のクラスは、から継承し、次のようにエクスポートする必要があり `ICommandHandler<TypeCharCommandArgs>` <xref:Microsoft.VisualStudio.Commanding.ICommandHandler> ます。

   ```csharp
   [Export(typeof(ICommandHandler))]
   [ContentType("text")]
   [Name("KeyBindingTest")]
   internal class KeyBindingCommandHandler : ICommandHandler<TypeCharCommandArgs>
   ```

4. コマンドハンドラーの表示名を追加します。

   ```csharp
   public string DisplayName => "KeyBindingTest";
   ```

5. 次のように、メソッドを実装し `GetCommandState()` ます。 このコマンドハンドラーはコアエディターの TYPECHAR コマンドを処理するため、コアエディターに対してコマンドの有効化を委任できます。

   ```csharp
   public CommandState GetCommandState(TypeCharCommandArgs args)
   {
       return CommandState.Unspecified;
   }
   ```

6. `ExecuteCommand()`プラス記号 ( **+** ) 文字が入力されている場合に、ビューに紫色のボックスを追加するように、メソッドを実装します。

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

   7. *KeyBindingTestTextViewCreationListener.cs*ファイルから*KeyBindingCommandHandler.cs*レイヤーの定義をコピーし、 *KeyBindingTestTextViewCreationListener.cs*ファイルを削除します。

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

## <a name="make-the-adornment-appear-on-every-line"></a>すべての行に表示されるようにします。

元の表示要素は、テキストファイル内のすべての文字 "a" に表示されます。 文字への応答として装飾を追加するようにコードを変更したので、次は **+** 文字が入力された行にのみ装飾を追加し **+** ます。 表示要素のコードを変更して、すべての "a" に表示されるようになります。

*KeyBindingTest.cs*ファイルで、メソッドを変更し `CreateVisuals()` て、' a ' 文字を修飾するビュー内のすべての行を反復処理します。

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

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする

1. KeyBindingTest ソリューションをビルドし、実験用インスタンスで実行します。

2. テキストファイルを作成するか、開きます。 文字 "a" を含む単語を入力し、 **+** テキストビューの任意の場所に入力します。

     紫色の四角形は、ファイル内のすべての ' a ' 文字に表示されます。
