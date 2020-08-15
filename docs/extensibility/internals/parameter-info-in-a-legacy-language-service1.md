---
title: 従来の言語でのパラメーターヒント Service1 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, method tips
- method tips
- language services, parameter info tooltip
- IVsMethodData interface
- Parameter Info (IntelliSense)
ms.assetid: f367295e-45b6-45d2-9ec8-77481743beef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8f8e5664634d189e8463376761d8fb59543740df
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238076"
---
# <a name="parameter-info-in-a-legacy-language-service-1"></a>従来の言語サービスのパラメーター情報1
IntelliSense の [パラメーターヒント] ツールヒントには、ユーザーが言語構成要素内の場所に関するヒントを提供します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 詳細については、「 [エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="how-parameter-info-tooltips-work"></a>パラメーターヒントのツールヒントのしくみ
 エディターでステートメントを入力すると、VSPackage は、入力されたステートメントの定義を含む小さいツールヒントウィンドウを表示します。 たとえば、Microsoft Foundation Classes (MFC) ステートメント (など) を入力 `pMainFrame ->UpdateWindow` し、左中かっこキーを押すと、パラメーターの一覧が表示され、メソッドの定義が表示され `UpdateWindow` ます。

 パラメーターヒントは通常、ステートメント入力候補と組み合わせて使用されます。 これらは、パラメーターまたはその他の書式設定された情報をメソッド名またはキーワードの後に持つ言語で最も役立ちます。

 パラメーターヒントのヒントは、コマンドのインターセプトを通じて言語サービスによって開始されます。 ユーザー文字をインターセプトするには、言語サービスオブジェクトが <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装し、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスのメソッドを呼び出すことによって、テキストビューにポインターを実装に渡す必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。 コマンドフィルターは、コードウィンドウに入力したコマンドを受け取ります。 コマンド情報を監視して、ユーザーにパラメーター情報を表示するタイミングを確認します。 ステートメント入力候補、エラーマーカーなどに対して同じコマンドフィルターを使用できます。

 言語サービスがヒントを提供できるキーワードを入力すると、言語サービスがオブジェクトを作成 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> し、インターフェイスのメソッドを呼び出して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 、ヒントを表示するよう IDE に通知します。 を使用してオブジェクトを作成し、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> `VSLocalCreateInstance` コクラスを指定し `CLSID_VsMethodTipWindow` ます。 `VsLocalCreateInstance` は、ヘッダーファイル vsdoc .h に定義されている関数です `QueryService` 。この関数は、ローカルレジストリを呼び出し、のこのオブジェクトに対してを呼び出し `CreateInstance` `CLSID_VsMethodTipWindow` ます。

## <a name="providing-a-method-tip"></a>メソッドヒントの提供
 メソッドヒントを提供するには、インターフェイス <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> のメソッドを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> 、インターフェイスの実装に渡し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> ます。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>クラスが呼び出されると、そのメソッドは次の順序で呼び出されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetContextStream%2A>

     現在のテキストバッファー内の関連データの位置と長さを返します。 これにより、IDE は、ツールヒントウィンドウでそのデータを不明瞭にしないように指示します。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetCurMethod%2A>

     最初に表示するメソッド番号 (0 から始まるインデックス) を返します。 たとえば、ゼロを返すと、最初にオーバーロードされたメソッドが最初に表示されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetOverloadCount%2A>

     現在のコンテキストで適用可能なオーバーロードされたメソッドの数を返します。 このメソッドで1を超える値を返した場合、テキストビューには、上矢印と下矢印が表示されます。 下矢印をクリックすると、IDE によってメソッドが呼び出され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.NextMethod%2A> ます。 上矢印をクリックすると、IDE によってメソッドが呼び出され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.PrevMethod%2A> ます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>

     パラメーターヒントヒントのテキストは、メソッドとメソッドの複数の呼び出し中に構築され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A> ます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterCount%2A>

     メソッドに表示するパラメーターの数を返します。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>

     表示するオーバーロードに対応するメソッド番号を返す場合は、このメソッドが呼び出され、その後にメソッドを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> ます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>

     メソッドヒントが表示されたときに、エディターを更新するように言語サービスに通知します。 メソッドで、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> 次のように呼び出します。

    ```
    <pTxWin> ->UpdateTipWindow(<pTip>, UTW_CONTENTCHANGED | UTW_CONTEXTCHANGED).
    ```

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>

     メソッドのヒントウィンドウを閉じると、メソッドの呼び出しが表示さ <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> れます。
