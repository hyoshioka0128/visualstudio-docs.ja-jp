---
title: 従来の言語サービスでの構文の色付け |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring
- language services, syntax coloring
ms.assetid: f65ff67e-8c20-497a-bebf-5e2a5b5b012f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2589ec24f230287306e0ff7e802d381fb6ab18b7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704755"
---
# <a name="syntax-coloring-in-a-legacy-language-service"></a>従来の言語サービスでの構文の色分け表示

Visual Studio は、色分けサービスを使用して、言語の要素を識別し、エディターで指定した色で表示します。

## <a name="colorizer-model"></a>着色剤モデル
 言語サービスは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>エディターによって使用されるインターフェイスを実装します。 この実装は、次の図に示すように、言語サービスとは別のオブジェクトです。

 ![SVC Colorizer グラフィック](../../extensibility/internals/media/figlgsvccolorizer.gif)

> [!NOTE]
> 構文の色分けサービスは、テキストを色分けするための一般的な Visual Studio のメカニズムとは別です。 色の指定をサポートする[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]一般的なメカニズムの詳細については、「[フォントと色の使用](/visualstudio/extensibility/using-fonts-and-colors?view=vs-2015)」を参照してください。

 カラー化器に加えて、言語サービスは、カスタムの着色可能な項目を提供することを宣伝することによって、エディターで使用されるカスタムのカラー対応アイテムを提供することができます。 これを行うには、インターフェイスを実装<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>する同じオブジェクトにインターフェイスを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>実装します。 エディターがメソッドを呼び出すときに、カスタムの色指定<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>可能な項目の数を返し、エディターがメソッドを呼び出<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>すときに、個々のカスタムの色付け可能な項目を返します。

 この<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>メソッドは、インターフェイスを実装するオブジェクト<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>を返します。 言語サービスが 24 ビットまたは高色の値を<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>サポートする場合は、インターフェイスと同じオブジェクトに<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>インターフェイスを実装する必要があります。

## <a name="how-a-vspackage-uses-a-language-service-colorizer"></a>VSPackage が言語サービスの色付け機能を使用する方法

1. VSPackage は、適切な言語サービスを取得する必要があります、言語サービスの VSPackage は、次を行う必要があります。

    1. インターフェイスを実装するオブジェクト<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>を使用して、色分けするテキストを取得します。

         テキストは、通常、インターフェイスを実装するオブジェクトを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>使用して表示されます。

    2. 言語サービスの GUID の VSPackage のサービス プロバイダーを照会して、言語サービスを取得します。 言語サービスは、ファイル拡張子によってレジストリで識別されます。

    3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A>メソッドを呼び出<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>して、言語サービスを に関連付けます。

2. VSPackage は、次のようにカラー化オブジェクトを取得して使用できるようになりました。

    > [!NOTE]
    > コア エディターを使用する VSPackage は、言語サービスのカラー化オブジェクトを明示的に取得する必要はありません。 コア エディターのインスタンスが適切な言語サービスを取得するとすぐに、ここに示すすべての色付けタスクが実行されます。

    1. 言語サービスのオブジェクトのメソッド<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>を呼び出して、 および<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2>インターフェイスを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>実装する言語サービスの<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>Colorizer オブジェクトを取得します。

    2. 特定の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>テキスト範囲のカラー表示情報を取得するには、このメソッドを呼び出します。

         <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>は、色分けされるテキスト範囲内の各文字に対して 1 つずつ、値の配列を返します。 値は、コア エディターによって維持される既定の色付け可能な項目リストまたは言語サービス自体によって維持されるカスタムの色付け可能な項目リストのいずれかの色付け可能な項目リストにインデックスです。

    3. 選択したテキストを表示するには、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>メソッドによって返される色付け情報を使用します。

> [!NOTE]
> 言語サービスの色指定者を使用するだけでなく、VSPackage は汎用の Visual Studio テキストの色分けメカニズムを使用することもできます。 このメカニズムの詳細については、「[フォントと色の使用](/visualstudio/extensibility/using-fonts-and-colors?view=vs-2015)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
- [構文の色分け表示の実装](../../extensibility/internals/implementing-syntax-coloring.md)

 エディターが言語サービスの構文色分けにアクセスする方法と、構文の色分けをサポートするために言語サービスが実装する必要があるものについて説明します。

- [方法: ビルトインの配色可能な項目の使用](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

 言語サービスから組み込みの色付け可能な項目を使用する方法を示します。

- [カスタムの配色可能な項目](../../extensibility/internals/custom-colorable-items.md)

 カスタムの色付け可能な項目を実装する方法について説明します。
