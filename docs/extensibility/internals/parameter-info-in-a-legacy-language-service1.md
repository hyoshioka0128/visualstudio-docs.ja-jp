---
title: レガシー言語サービスのパラメータ情報1 |マイクロソフトドキュメント
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
ms.openlocfilehash: c26073252aae5434ba5a8197955948d0d9ec883d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706802"
---
# <a name="parameter-info-in-a-legacy-language-service"></a>従来の言語サービスのパラメーター ヒント
IntelliSense パラメーターヒントツールヒントは、言語構成要素のどこにあるかについてのヒントをユーザーに提供します。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 詳細については、「[エディタと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="how-parameter-info-tooltips-work"></a>パラメーターヒントツールヒントの動作
 エディターでステートメントを入力すると、VSPackage は、入力するステートメントの定義を含む小さなツールヒント ウィンドウを表示します。 たとえば、Microsoft Foundation クラス (MFC) ステートメント ( など`pMainFrame ->UpdateWindow`) を入力し、左かっこを押してパラメーターの一覧を表示すると、メソッドの定義を`UpdateWindow`表示するメソッド ヒントが表示されます。

 パラメーターヒントツールヒントは、通常、ステートメント入力候補と組み合わせて使用されます。 メソッド名またはキーワードの後にパラメーターやその他の書式付き情報がある言語で最も役立ちます。

 パラメーターヒントツールヒントは、コマンドのインターセプトによって言語サービスによって開始されます。 ユーザー文字をインターセプトするには、言語サービス オブジェクトがインターフェイス<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>を実装し、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>インターフェイスでメソッドを呼び出すことによって、実装へのポインターをテキスト ビューに渡す必要があります。 コマンド フィルターは、コード ウィンドウに入力したコマンドをインターセプトします。 ユーザーにパラメーター情報を表示するタイミングを知るために、コマンド情報をモニターします。 ステートメント入力候補やエラー・マーカーなどには、同じコマンド・フィルターを使用できます。

 言語サービスがヒントを提供できるキーワードを入力すると、言語サービスはオブジェクトを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>作成し、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>インターフェイスでメソッドを呼び出して、ヒントを表示するように IDE に通知します。 コクラス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>`CLSID_VsMethodTipWindow`を使用`VSLocalCreateInstance`してオブジェクトを作成し、 を指定します。 `VsLocalCreateInstance`は、ローカル レジストリを呼び出し、このオブジェクトを`QueryService`呼び出`CreateInstance`すヘッダー ファイル vsdoc.h で定義されている関数です`CLSID_VsMethodTipWindow`。

## <a name="providing-a-method-tip"></a>メソッドヒントの提供
 メソッドヒントを提供するには、インターフェイスで<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>メソッドを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>呼び出し、インターフェイスの実装を<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>渡します。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>クラスが呼び出されると、そのメソッドは次の順序で呼び出されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetContextStream%2A>

     現在のテキスト バッファー内の関連データの位置と長さを返します。 これにより、ツールヒント ウィンドウでそのデータが隠されないように IDE に指示されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetCurMethod%2A>

     最初に表示するメソッド番号 (0 から始まるインデックス) を返します。 たとえば、ゼロを返した場合、最初のオーバーロードされたメソッドが最初に表示されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetOverloadCount%2A>

     現在のコンテキストで適用可能なオーバーロードされたメソッドの数を返します。 このメソッドに対して 1 より大きい値を返す場合、テキスト ビューには上下の矢印が表示されます。 下矢印をクリックすると、メソッドが呼び出<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.NextMethod%2A>されます。 上向き矢印をクリックすると、メソッドが呼<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.PrevMethod%2A>び出されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>

     パラメーターヒントのテキストは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>メソッドと<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>メソッドの呼び出し中に作成されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterCount%2A>

     メソッドに表示するパラメーターの数を返します。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>

     表示するオーバーロードに対応するメソッド番号を返す場合、このメソッドが呼び出され、その後にメソッド<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>が呼び出されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>

     メソッドヒントが表示されたときにエディタを更新するように、言語サービスに通知します。 メソッドで<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>、次のメソッドを呼び出します。

    ```
    <pTxWin> ->UpdateTipWindow(<pTip>, UTW_CONTENTCHANGED | UTW_CONTEXTCHANGED).
    ```

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>

     メソッド ヒント ウィンドウを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>閉じると、メソッドの呼び出しが受け取ります。
