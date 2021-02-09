---
title: IDebugProgram3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3 interface
ms.assetid: 4301ba23-c00c-4ce5-8b1e-3f27da312034
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d22a58021a744cc71b8df3acb8e577d853aa2829
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889994"
---
# <a name="idebugprogram3"></a>IDebugProgram3
このインターフェイスは、プロセスで実行されているプログラムを表し、スレッド情報を提供することによって [実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md) を拡張します。

## <a name="syntax"></a>構文

```
IDebugProgram3 : IDebugProgram3
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) とカスタムポート供給業者は、プロセス内のプログラムを表すために、このインターフェイスを実装します。 また、セッションデバッグマネージャー (SDM) は、このインターフェイスを実装して、 [アタッチ](../../../extensibility/debugger/reference/idebugprogram2-attach.md)する情報を提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)イベントは、新しいプログラムに対してこのインターフェイスを返します。 このインターフェイスは、複数のインターフェイスの多くのメソッドのパラメーターとしても使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugProgram3` ます。

|Method|説明|
|------------|-----------------|
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|プログラムを実行します。 スレッドは、実行時にユーザーが表示しているスレッドにデバッガー情報を提供するために返されます。|

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>解説
 プログラムは、特定の実行時アーキテクチャで実行されるスレッドコンテナーであり、プロセスは1つ以上のプログラムで構成されます。

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
