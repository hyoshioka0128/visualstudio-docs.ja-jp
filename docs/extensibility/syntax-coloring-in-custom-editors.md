---
title: カスタムエディタでの構文の色付け |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - syntax coloring
ms.assetid: 74900b9a-baef-432a-8231-4568fb5e19ad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6296c8451684a121ac42dbde6619c0ebbb421908
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699333"
---
# <a name="syntax-coloring-in-custom-editors"></a>カスタム エディターでの構文の色分け表示
Visual Studio 環境 SDK エディター (コア エディターを含む) は、言語サービスを使用して特定の構文項目を識別し、特定のドキュメント ビューに指定した色で表示します。

## <a name="colorization-requirements"></a>色付けの要件
 言語サービスのカラー化を実装するすべてのエディターは、次の操作を行う必要があります。

1. 色分けする<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>テキストを管理するオブジェクトと、テキストのドキュメント ビュー<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>を提供するオブジェクトを使用します。

2. 言語サービスの識別 GUID を使用して VSPackage のサービス プロバイダーを照会して、特定の言語サービスへのインターフェイスを取得します。

3. を実装<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>するオブジェクトのメソッドを呼び出します。 このメソッドは、言語サービスを、色<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>分けされるテキストを管理するために VSPackage が使用する実装に関連付けます。

## <a name="core-editor-usage-of-a-language-services-colorizer"></a>言語サービスのカラーライザのコア エディターの使用法
 カラー化プログラムを使用した言語サービスがコア エディターのインスタンスによって取得されると、言語サービスのカラー化プログラムによるテキストの解析とレンダリングは、ユーザー側での操作を必要とせずに自動的に行われます。

 IDE は透過的に次の手順を実行します。

- の実装でテキストが追加または変更された場合にテキストを解析および分析するために必要に応じて<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>、カラー化器を呼び出します。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>実装によって提供されるドキュメント ビューによって提供される表示が更新され、着色者によって返される情報を使用して再描画されることを確認します。

## <a name="non-core-editor-usage-of-a-language-services-colorizer"></a>言語サービスのカラーライザの非コアエディタの使用法
 非コア エディター インスタンスは、言語サービスの構文の色化サービスを使用することもできますが、明示的に取得して、サービスのカラー化を適用し、ドキュメント ビュー自体を再描画する必要があります。

 これを行うには、非コア エディターを実行する必要があります。

1. 言語サービスのカラー化オブジェクト (実装<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>および<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2>) を取得します。 VSPackage は、言語サービスの<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>インターフェイスでメソッドを呼び出すことによってこれを行います。

2. 特定の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>テキスト範囲を色分けするように要求するには、このメソッドを呼び出します。

     この<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>メソッドは、色分けされるテキスト範囲内の各文字に対して 1 つずつ、値の配列を返します。 また、テキスト範囲は、コメント、キーワード、データ型などの特定の種類の色付け可能なアイテムとして識別されます。

3. 返される色化情報<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>を使用して、テキストを再描画および表示します。

> [!NOTE]
> 言語サービスのカラー化器を使用するだけでなく、VSPackage は汎用の Visual Studio 環境 SDK のテキスト色付けメカニズムを使用することを選択できます。 このメカニズムの詳細については、「[フォントと色の使用](/visualstudio/extensibility/using-fonts-and-colors?view=vs-2015)」を参照してください。

## <a name="see-also"></a>関連項目

- [従来の言語サービスでの構文の色分け表示](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [構文の色分け表示の実装](../extensibility/internals/implementing-syntax-coloring.md)
- [方法: ビルトインの配色可能な項目の使用](../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [カスタムの配色可能な項目](../extensibility/internals/custom-colorable-items.md)
