---
title: 呼び出し履歴の評価 |Microsoft Docs
description: Enumframes Info メソッドと、このメソッドを実装して、中断モード中に呼び出し履歴のスタックフレームを表示する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: fc637ff3ce2fe596eed48684523da7114fe0a03a
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914674"
---
# <a name="call-stack-evaluation"></a>呼び出し履歴の評価
中断モード中に呼び出し履歴のスタックフレームを表示するには、 [enumframes info](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) メソッドを実装する必要があります。

## <a name="methods-for-evaluation"></a>評価の方法
 単純なデバッグエンジン (DE) の場合は、スタックフレームが1つだけ存在する可能性があります。 中断モード中にスタックフレームを確認するには、 [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)の次のメソッドを実装する必要があります。

|メソッド|説明|
|------------|-----------------|
|[GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|スタックフレームのコードコンテキストを取得します。 コードコンテキストは、スタックフレーム内の現在の命令ポインターを表します。|
|[GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|スタックフレームのドキュメントコンテキストを取得します。 ドキュメントコンテキストは、スタックフレームのソースコード内の現在の場所を表します。 プログラム内で停止したときにソースコードを表示するために必要です。|

 これらのメソッドには、いくつかのコンテキスト関連のインターフェイスおよびメソッドの実装が必要です。 したがって、 [Getdocumentcontext](../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) メソッドと [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md)の次のメソッドを実装する必要があります。

|メソッド|説明|
|------------|-----------------|
|[GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|ドキュメントコンテキストのファイルステートメントの範囲を取得します。|

 コードコンテキストを列挙するには、 [IEnumDebugCodeContexts2](../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)のすべてのメソッドを実装する必要があります。

## <a name="see-also"></a>関連項目
- [実行制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
