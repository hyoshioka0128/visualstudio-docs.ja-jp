---
title: をクリックしてクエリエンジン2を実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2
helpviewer_keywords:
- IDebugQueryEngine2 interface
ms.assetid: 8f0e1838-a818-4459-9138-a3dceb7408de
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31b1784055c54c9243237c81edb708e13de9bc5b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720656"
---
# <a name="idebugqueryengine2"></a>IDebugQueryEngine2
このインターフェイスを使用すると、セッション デバッグ マネージャー (SDM) は、デバッグ エンジン (DE) を表すインターフェイスを取得できます。

## <a name="syntax"></a>構文

```
IDebugQueryEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、最も一般的な DE インターフェイス[(IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) [、IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)、および[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)など) を実装するオブジェクトにこのインターフェイスを実装し、DE 自体の[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)インターフェイスへのアクセスを許可します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 この[インターフェイス](/cpp/atl/queryinterface)を取得するには、一般的な DE インターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugQueryEngine2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetEngineInterface](../../../extensibility/debugger/reference/idebugqueryengine2-getengineinterface.md)|カスタム デバッグ エンジン (DE) インターフェイスを取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは通常、因果関係順序付けされた関数を通してのステップ実行をサポートするために[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスを実装するオブジェクトに実装されます。つまり、デバッガーが関数からステップ アウトする場合、次に実行する関数は、スタックの前の関数ではなく、別のスレッドの関数である可能性があります。 "因果関係" の定義については、「 [Visual Studio デバッガーの用語集](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
