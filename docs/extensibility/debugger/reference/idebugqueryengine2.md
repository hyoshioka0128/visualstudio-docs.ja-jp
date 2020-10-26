---
title: IDebugQueryEngine2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80720656"
---
# <a name="idebugqueryengine2"></a>IDebugQueryEngine2
このインターフェイスを使用すると、セッションデバッグマネージャー (SDM) は、デバッグエンジン (DE) を表すインターフェイスを取得できます。

## <a name="syntax"></a>構文

```
IDebugQueryEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 De は、de 自体の[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)インターフェイスへのアクセスを許可するために、最も一般的な de インターフェイス ( [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)、 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)、 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)など) を実装するオブジェクトに対してこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、一般的な DE インターフェイスで [QueryInterface](/cpp/atl/queryinterface) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugQueryEngine2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetEngineInterface](../../../extensibility/debugger/reference/idebugqueryengine2-getengineinterface.md)|カスタムデバッグエンジン (DE) インターフェイスを取得します。|

## <a name="remarks"></a>注釈
 このインターフェイスは、通常、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスを実装するオブジェクトに実装されます。これは、関数を使用した因果関係のステップ実行をサポートするためです。つまり、デバッガーが関数からステップアウトすると、次に実行される関数がスタック上の前の関数ではなく、別のスレッドの関数が完全になることがあります。 "因果関係" の定義については、「 [Visual Studio デバッガー用語集](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
