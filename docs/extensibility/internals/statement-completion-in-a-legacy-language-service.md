---
title: 従来の言語サービスでのステートメント入力候補 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80704943"
---
# <a name="statement-completion-in-a-legacy-language-service"></a>従来の言語サービスでのステートメント入力補完
ステートメント入力候補は、ユーザーがコアエディターで入力を開始した言語キーワードまたは要素をユーザーが終了するのを言語サービスが支援するプロセスです。 このトピックでは、ステートメントの入力候補の動作と、言語サービスでのその実装方法について説明します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 ステートメント入力候補を実装する新しい方法の詳細については、「 [チュートリアル: ステートメント入力候補の表示](../../extensibility/walkthrough-displaying-statement-completion.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="implementing-statement-completion"></a>ステートメント入力候補の実装
 コアエディターでは、ステートメント入力候補によって特殊な UI がアクティブ化され、コードを簡単に記述できるようになります。 ステートメント入力候補は、必要に応じて適切なオブジェクトまたはクラスを表示することによって役立ちます。これにより、特定の要素を記憶したり、ヘルプリファレンストピックで検索したりする必要がなくなります。

 ステートメント入力候補を実装するには、解析可能なステートメント完了トリガーを使用する必要があります。 たとえば、は [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ドット (.) 演算子を使用し、は [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 矢印 (->) 演算子を使用します。 言語サービスでは、複数のトリガーを使用して、ステートメント入力候補を開始できます。 これらのトリガーは、コマンドフィルターでプログラミングされています。

## <a name="command-filters-and-triggers"></a>コマンドフィルターとトリガー
 コマンドフィルターは、トリガーまたはトリガーの発生をインターセプトします。 コマンドフィルターをビューに追加するには、インターフェイスを実装 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> し、メソッドを呼び出してビューにアタッチし <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> ます。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>ステートメント入力候補、エラーマーカー、メソッドヒントなど、言語サービスのすべての側面に対して同じコマンドフィルター () を使用できます。 詳細については、「 [従来の言語サービスコマンドのインターセプト](../../extensibility/internals/intercepting-legacy-language-service-commands.md)」を参照してください。

 エディターでトリガーを入力すると (具体的にはテキストバッファー)、言語サービスはメソッドを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> ます。 これにより、エディターによって UI が表示され、ユーザーはステートメント入力候補の候補から選択できるようになります。 このメソッド <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> では、パラメーターとしておよびフラグを実装する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.UpdateCompletionFlags> ます。 完了項目の一覧がスクロールリストボックスに表示されます。 ユーザーが入力を続けると、リストボックス内の選択内容が更新され、最後に入力された文字に最も近い一致が反映されます。 コアエディターは、ステートメント入力候補用の UI を実装しますが、言語サービスは、その <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> ステートメントの候補となる候補項目のセットを定義するインターフェイスを実装する必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [従来の言語サービスのコマンドの受信](../../extensibility/internals/intercepting-legacy-language-service-commands.md)
