---
title: 従来の言語サービスのクイックヒント |Microsoft Docs
description: Id に関する情報を表示するための IntelliSense クイックヒント操作のサポートについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 255022c2722104d3790d1c417eee644730ddc1e8
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97875077"
---
# <a name="quick-info-in-a-legacy-language-service"></a>従来の言語サービスのクイック ヒント
IntelliSense のクイックヒントは、ユーザーが識別子にカレットを置き、 **intellisense** メニューから [**クイックヒント**] を選択するか、識別子の上にマウスカーソルを置いたときに、ソースの識別子に関する情報を表示します。 これにより、ツールヒントが識別子に関する情報と共に表示されます。 通常、この情報は識別子の種類で構成されます。 デバッグエンジンがアクティブになっている場合は、この情報に現在の値が含まれている可能性があります。 デバッグエンジンは式の値を提供しますが、言語サービスは識別子のみを処理します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 詳細については、「 [チュートリアル: QuickInfo ツールヒントの表示](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

 Managed package framework (MPF) 言語サービスクラスは、IntelliSense クイックヒントツールヒントを表示するための完全なサポートを提供します。 必要なのは、表示するテキストを指定して、クイックヒント機能を有効にすることだけです。

 表示されるテキストを取得するには、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 解析理由の値を指定してメソッドパーサーを呼び出し <xref:Microsoft.VisualStudio.Package.ParseReason> ます。 この理由は、オブジェクトで指定された場所にある識別子について、型情報 (またはクイックヒントに表示される適切なもの) を取得するようパーサーに指示し <xref:Microsoft.VisualStudio.Package.ParseRequest> ます。 <xref:Microsoft.VisualStudio.Package.ParseRequest>オブジェクトは、メソッドに渡されたものです <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 。

 パーサーは、 <xref:Microsoft.VisualStudio.Package.ParseRequest> すべての識別子の型を確認するために、オブジェクト内のすべての位置までを解析する必要があります。 次に、パーサーは、解析要求の場所で識別子を取得する必要があります。 最後に、パーサーは、その識別子に関連付けられたツールヒントデータをオブジェクトに渡して、 <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトがメソッドからテキストを返すことができるようにする必要があり <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> ます。

## <a name="enabling-the-quick-info-feature"></a>クイックヒント機能を有効にする
 クイックヒント機能を有効にするには、 `CodeSense` のおよび名前付きパラメーターを設定する必要があり `QuickInfo` <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> ます。これらの属性は、 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> プロパティとプロパティを設定し <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A> ます。

## <a name="implementing-the-quick-info-feature"></a>クイックヒント機能の実装
 クラスは、 <xref:Microsoft.VisualStudio.Package.ViewFilter> IntelliSense のクイックヒント操作を処理します。 クラスが <xref:Microsoft.VisualStudio.Package.ViewFilter> コマンドを受け取ると <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 、クラスは、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> の解析理由 <xref:Microsoft.VisualStudio.Package.ParseReason> とコマンドが送信されたときのキャレットの位置を使用して、メソッドを呼び出し <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> ます。 次に、メソッドパーサーは、指定された場所までソースを解析し、指定した場所にある識別子を解析して、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> クイックヒントツールヒントに表示する内容を決定する必要があります。

 ほとんどのパーサーは、ソースファイル全体を最初に解析し、結果を解析ツリーに格納します。 がメソッドに渡されると、完全な解析が実行され <xref:Microsoft.VisualStudio.Package.ParseReason> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> ます。 その他の種類の解析では、解析ツリーを使用して必要な情報を取得できます。

 たとえば、の解析理由値は、 <xref:Microsoft.VisualStudio.Package.ParseReason> ソースの場所で識別子を検索し、解析ツリー内で検索して型情報を取得することができます。 この型情報はクラスに渡され、 <xref:Microsoft.VisualStudio.Package.AuthoringScope> メソッドによって返され <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> ます。
