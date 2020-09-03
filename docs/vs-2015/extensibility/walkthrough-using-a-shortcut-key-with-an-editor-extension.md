---
title: 'チュートリアル: エディター拡張機能でのショートカットキーの使用 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
caps.latest.revision: 33
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5c9cb20bafa552c47a2f599d12e6b66fdb2bde59
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201940"
---
# <a name="walkthrough-using-a-shortcut-key-with-an-editor-extension"></a>チュートリアル: エディター拡張機能でショートカット キーを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディター拡張機能のショートカットキーに応答できます。 次のチュートリアルでは、ショートカットキーを使用して、ビューの表示要素をテキストビューに追加する方法について説明します。 このチュートリアルは、ビューポートの表示要素エディターテンプレートに基づいており、+ 文字を使用して表示要素を追加できます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトの作成  
  
1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `KeyBindingTest` します。  
  
2. エディターのテキスト表示項目テンプレートをプロジェクトに追加し、という名前を指定 `KeyBindingTest` します。 詳細については、「 [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。  
  
3. 次の参照を追加し、 **CopyLocal** をに設定し `false` ます。  
  
    VisualStudio  
  
    Microsoft.VisualStudio.OLE.Interop  
  
    VisualStudio. 14.0  
  
    VisualStudio。相互運用  
  
   KeyBindingTest クラスファイルで、クラス名を PurpleCornerBox に変更します。 左余白に表示される電球を使用して、その他の適切な変更を行います。 コンストラクター内で、装飾層の名前を **Keybindingtest** から **PurpleCornerBox**に変更します。  
  
```csharp  
this.layer = view.GetAdornmentLayer("PurpleCornerBox");  
```  
  
## <a name="defining-the-command-filter"></a>コマンドフィルターの定義  
 コマンドフィルターは、を実装したもので <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 、装飾をインスタンス化することによってコマンドを処理します。  
  
1. クラス ファイルを追加し、その名前を `KeyBindingCommandFilter`にします。  
  
2. 次の using ステートメントを追加します。  
  
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
  
    ```vb  
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)  
    {  
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);  
    }  
    ```  
  
7. `Exec()`+ 文字が入力されている場合に、ビューに紫色のボックスを追加するように、メソッドを実装します。  
  
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
  
## <a name="adding-the-command-filter"></a>コマンドフィルターを追加する  
 表示要素プロバイダーは、コマンドフィルターをテキストビューに追加する必要があります。 この例では、プロバイダーがを実装して、 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> テキストビュー作成イベントをリッスンします。 この装飾プロバイダーは、装飾の Z オーダーを定義する、装飾層もエクスポートします。  
  
1. Keybindingtesttextviewのファイルに、次の using ステートメントを追加します。  
  
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
  
2. 装飾層の定義で、AdornmentLayer の名前を **Keybindingtest** から **PurpleCornerBox**に変更します。  
  
    ```csharp  
    [Export(typeof(AdornmentLayerDefinition))]  
    [Name("PurpleCornerBox")]  
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]  
    public AdornmentLayerDefinition editorAdornmentLayer;  
    ```  
  
3. テキストビューアダプターを取得するには、をインポートする必要があり <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> ます。  
  
    ```csharp  
    [Import(typeof(IVsEditorAdaptersFactoryService))]  
    internal IVsEditorAdaptersFactoryService editorFactory = null;  
  
    ```  
  
4. を <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> 追加するようにメソッドを変更し `KeyBindingCommandFilter` ます。  
  
    ```csharp  
    public void TextViewCreated(IWpfTextView textView)  
    {  
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));  
    }  
    ```  
  
5. `AddCommandFilter`ハンドラーはテキストビューアダプターを取得し、コマンドフィルターを追加します。  
  
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
  
## <a name="making-the-adornment-appear-on-every-line"></a>すべての行に表示要素を表示する  
 元の表示要素は、テキストファイル内のすべての文字 "a" に表示されます。 これで、' + ' 文字に応答して装飾を追加するようにコードを変更したので、' + ' が入力された行にのみ、装飾を追加します。 表示要素のコードを変更して、すべての "a" に表示されるようになります。  
  
 KeyBindingTest.cs ファイルで、CreateVisuals () メソッドを変更して、' a ' 文字を修飾するビュー内のすべての行を反復処理します。  
  
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
  
## <a name="building-and-testing-the-code"></a>コードのビルドとテスト  
  
1. KeyBindingTest ソリューションをビルドし、実験用インスタンスで実行します。  
  
2. テキストファイルを作成するか、開きます。 文字 "a" を含む単語を入力し、テキストビューの任意の場所に「+」と入力します。  
  
     紫色の四角形は、ファイル内のすべての ' a ' 文字に表示されます。
