---
title: 従来の言語サービスのクイック情報 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Quick Info, supporting in language services [managed package framework]
- IntelliSense, Quick Info
- language services [managed package framework], IntelliSense Quick Info
ms.assetid: 159ccb0b-f5d6-4912-b88b-e9612924ed5e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d070c607313b406f036a5b6f071eaa371070408
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705945"
---
# <a name="quick-info-in-a-legacy-language-service"></a>従来の言語サービスのクイック ヒント
IntelliSense クイック ヒントは、ユーザーが識別子にキャレットを配置し **、IntelliSense**メニューから**クイック ヒント**を選択するか、またはマウス カーソルを識別子の上に置くと、ソース内の識別子に関する情報を表示します。 これにより、識別子に関する情報がツール ヒントに表示されます。 この情報は、通常、識別子の種類で構成されます。 デバッグ エンジンがアクティブな場合、この情報には現在の値が含まれる場合があります。 デバッグ エンジンは式の値を提供し、言語サービスは識別子のみを処理します。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 詳細については、「[チュートリアル: クイック ヒントツールヒントの表示](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

 管理パッケージ フレームワーク (MPF) 言語サービス クラスは、IntelliSense クイック ヒント ツール ヒントを表示するための完全なサポートを提供します。 必要な操作は、表示するテキストを指定して、クイックヒント機能を有効にすることだけです。

 表示されるテキストは、解析理由の値を<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A><xref:Microsoft.VisualStudio.Package.ParseReason>使用してメソッド パーサーを呼び出すことによって取得されます。 この理由は、オブジェクトで指定された場所で識別子の型情報 (または [クイック ヒント] ツール ヒントに表示される適切な情報)<xref:Microsoft.VisualStudio.Package.ParseRequest>を取得するようにパーサーに指示します。 オブジェクト<xref:Microsoft.VisualStudio.Package.ParseRequest>は<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドに渡されたものです。

 パーサーは、すべての識別子の型を決定するために、<xref:Microsoft.VisualStudio.Package.ParseRequest>オブジェクト内の位置まですべてを解析する必要があります。 次に、パーサーは、解析要求の場所で識別子を取得する必要があります。 最後に、パーサーは、オブジェクトがメソッドからテキストを返すことができるように、<xref:Microsoft.VisualStudio.Package.AuthoringScope>その識別子に関連付けられているツール ヒント<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A>データをオブジェクトに渡す必要があります。

## <a name="enabling-the-quick-info-feature"></a>クイックヒント機能の有効化
 クイック ヒント機能を有効にするには、 の`CodeSense`および`QuickInfo`名前付き<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>パラメーターを設定する必要があります。これらの属性は、 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A>プロパティと プロパティを設定します。

## <a name="implementing-the-quick-info-feature"></a>クイック ヒント機能の実装
 クラス<xref:Microsoft.VisualStudio.Package.ViewFilter>は、IntelliSense クイック ヒント操作を処理します。 クラスが<xref:Microsoft.VisualStudio.Package.ViewFilter>コマンドを<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>受け取ると、クラスは、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>コマンドが送信された時点で<xref:Microsoft.VisualStudio.Package.ParseReason>のキャレットの解析理由と場所を指定して<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>メソッドを呼び出します。 メソッド<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>パーサーは、指定した場所までソースを解析し、指定した場所で識別子を解析して、クイック ヒント ツール ヒントに表示する内容を決定する必要があります。

 ほとんどのパーサーは、ソース ファイル全体の初期解析を行い、結果を解析ツリーに格納します。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドに渡されると<xref:Microsoft.VisualStudio.Package.ParseReason>、完全解析が実行されます。 その後、解析ツリーを使用して必要な情報を取得できます。

 たとえば、解析理由の<xref:Microsoft.VisualStudio.Package.ParseReason>値は、ソースの場所で識別子を検索し、型情報を取得する解析ツリーで検索できます。 この型情報は<xref:Microsoft.VisualStudio.Package.AuthoringScope>クラスに渡され、<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A>メソッドによって返されます。
