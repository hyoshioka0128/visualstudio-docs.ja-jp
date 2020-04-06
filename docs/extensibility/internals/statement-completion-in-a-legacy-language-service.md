---
title: レガシー言語サービスでのステートメントの完了 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- statement completion
- language services, statement completion
ms.assetid: 617439dc-3f0e-4e5f-b346-3e4e7fcf3c1b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bbeb360cf5bc0f74d6b2d9b93086382dd35da988
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704943"
---
# <a name="statement-completion-in-a-legacy-language-service"></a>従来の言語サービスでのステートメント入力補完
ステートメント入力候補とは、言語サービスが、コア エディターで入力を開始した言語キーワードまたは要素をユーザーが完成させるのに役立つプロセスです。 このトピックでは、ステートメント入力候補のしくみと、言語サービスでのステートメント入力候補の実装方法について説明します。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 ステートメント補完を実装する新しい方法の詳細については、「[チュートリアル : ステートメント入力候補の表示](../../extensibility/walkthrough-displaying-statement-completion.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="implementing-statement-completion"></a>ステートメント入力候補の実装
 コア エディターでは、ステートメント入力候補は、対話的にコードをより簡単かつ迅速に記述するのに役立つ特別な UI をアクティブにします。 ステートメント入力候補は、必要なときに関連するオブジェクトまたはクラスを表示することで、特定の要素を覚えておく必要がないようにしたり、ヘルプリファレンス トピックで参照する必要がなくなります。

 ステートメント入力候補を実装するには、言語に構文解析可能なステートメント完了トリガーが必要です。 たとえば、[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]ドット (.) 演算子を使用し[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]、矢印 (->) 演算子を使用します。 言語サービスは、複数のトリガーを使用してステートメントの完了を開始できます。 これらのトリガーは、コマンド・フィルターでプログラムされます。

## <a name="command-filters-and-triggers"></a>コマンド フィルタとトリガ
 コマンド フィルタは、トリガーのオカレンスをインターセプトします。 ビューにコマンド フィルターを追加するには、インターフェイスを<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>実装し、メソッドを呼び出すことによってビュー<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>にアタッチします。 ステートメント入力候補、エラー マーカー、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>メソッドヒントなど、言語サービスのすべての側面に対して同じコマンド フィルター ( ) を使用できます。 詳細については、「[レガシ言語サービス コマンドのインターセプト](../../extensibility/internals/intercepting-legacy-language-service-commands.md)」を参照してください。

 エディター (具体的にはテキスト バッファー) にトリガーが入力されると、言語サービスはメソッドを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>呼び出します。 これにより、エディターが UI を表示し、ユーザーがステートメント入力候補から選択できるようになります。 このメソッドでは、実装<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>し、フラグ<xref:Microsoft.VisualStudio.TextManager.Interop.UpdateCompletionFlags>をパラメーターとして実装する必要があります。 入力候補項目の一覧がスクロール リスト ボックスに表示されます。 ユーザーが入力を続けるにつれて、リスト ボックス内の選択項目が更新され、入力された最新の文字に最も近い文字が反映されます。 コア エディターは、ステートメントの完了のための UI を実装しますが、言語<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>サービスは、ステートメントの候補完了項目のセットを定義するインターフェイスを実装する必要があります。

## <a name="see-also"></a>関連項目
- [従来の言語サービスのコマンドの受信](../../extensibility/internals/intercepting-legacy-language-service-commands.md)
