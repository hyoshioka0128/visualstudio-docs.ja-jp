---
title: 式評価コンテキスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, context
ms.assetid: a2fd3758-09bd-45ae-8ecc-2d276c0036ba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e939a4fa5f4673e2f701206c96599c54bc0c3b51
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738738"
---
# <a name="expression-evaluation-context"></a>式評価コンテキスト
デバッグ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]時に、**式の評価コンテキスト**:

- 式の評価のコンテキストを表します。 一般に、評価コンテキストは、変数、パラメーター、関数、およびメソッドを評価する構文のスコープに対応します。 たとえば、スタック フレームに関連付けられた式評価コンテキストは、ローカル変数、メソッド パラメーター、およびクラス メンバー (該当する場合) を評価するためのコンテキストを提供します。

- プログラムがブレークポイントで停止したときに存在します。 式自体は、指定されたコンテキスト内でのバインディングと評価の準備が整った解析済み式を表すデータ構造です。

     詳細については、[式を使用](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)して作成します。 式が評価されると、変数または引数の名前と型とその値を含む、印刷可能な文字列が生成されます。 この文字列は、IDE の [ウォッチ] ウィンドウまたは [ローカル] ウィンドウに表示されます。

     `BSTR` [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)インターフェイスを指定すると、デバッグ エンジン (DE) は式を解析することで[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスを作成できます。 インターフェイスを`IDebugExpression2`指定すると、DE は同期式または非同期式の評価を通じて値を取得できます。 この値は、変数または引数の名前と型とともに IDE に送信され、表示されます。

## <a name="see-also"></a>関連項目
- [式評価インタフェース](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [デバッガーのコンテキスト](../../extensibility/debugger/debugger-contexts.md)
