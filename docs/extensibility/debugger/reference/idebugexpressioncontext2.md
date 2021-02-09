---
title: IDebugExpressionContext2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2
helpviewer_keywords:
- IDebugExpressionContext2 interface
ms.assetid: 577fdaae-4b2d-4112-9839-ab899535fa6f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 92e2561d28c3d4c7133208c78b9a492bc2614fd3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99901657"
---
# <a name="idebugexpressioncontext2"></a>IDebugExpressionContext2
このインターフェイスは、式の評価のコンテキストを表します。

## <a name="syntax"></a>構文

```
IDebugExpressionContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、式を評価できるコンテキストを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Get式コンテキスト](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)を呼び出すと、このインターフェイスが返されます。 このインターフェイスには、デバッグ中のプログラムが一時停止され、スタックフレームが使用可能な場合にのみアクセスできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugExpressionContext2` ます。

|Method|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugexpressioncontext2-getname.md)|評価コンテキストの名前を取得します。|
|[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)|評価のためにテキストベースの式を解析します。|

## <a name="remarks"></a>解説
 評価コンテキストは、式の評価を実行するためのスコープと考えることができます。

 プログラムが停止されると、セッションデバッグマネージャー (SDM) は、 [enumframe info](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)を呼び出すことで、DE からスタックフレームを取得します。 次に、SDM は [Get式コンテキスト](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) を呼び出して、インターフェイスを取得し `IDebugExpressionContext2` ます。 この後に [Parsetext](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) を呼び出して、評価の準備ができている解析済みの式を表す [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスを作成します。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
