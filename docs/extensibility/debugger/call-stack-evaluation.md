---
title: コール スタック評価 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], call stack evaluation
- call stacks, evaluation
ms.assetid: 373d6b49-0459-4cce-816e-05745a44fe49
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b5557d7eae0ffe54b0f01f1f9e95935d71455229
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739178"
---
# <a name="call-stack-evaluation"></a>コール スタックの評価
中断モード中に呼び出し履歴のスタック フレームを表示するには[、EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)メソッドを実装する必要があります。

## <a name="methods-for-evaluation"></a>評価方法
 単純なデバッグ エンジン (DE) の場合、スタック フレームが 1 つだけである場合があります。 中断モード中にスタック フレームを確認するには、[次](../../extensibility/debugger/reference/idebugstackframe2.md)のメソッドを実装する必要があります。

|Method|説明|
|------------|-----------------|
|[GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|スタック フレームのコード コンテキストを取得します。 コード コンテキストは、スタック フレーム内の現在の命令ポインターを表します。|
|[GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|スタック フレームのドキュメント コンテキストを取得します。 ドキュメント コンテキストは、スタック フレームのソース コード内の現在の位置を表します。 プログラムで停止した場合にソース コードを表示するために必要です。|

 これらのメソッドでは、コンテキスト関連の複数のインターフェイスとメソッドの実装が必要です。 したがって、[メソッド](../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)と[次](../../extensibility/debugger/reference/idebugdocumentcontext2.md)のメソッドを実装する必要があります。

|Method|説明|
|------------|-----------------|
|[GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|ドキュメント コンテキストのファイル ステートメント範囲を取得します。|

 コード コンテキストを列挙するには、[すべての](../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)メソッドを実装する必要があります。

## <a name="see-also"></a>関連項目
- [実行制御と状態評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
