---
title: プログラムノード2::Attach_V7 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::Attach
helpviewer_keywords:
- IDebugProgramNode2::Attach_V7
- IDebugProgramNode2::Attach
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bdee5b224ae38c3474009aeaf26e783ebc5dd139
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722139"
---
# <a name="idebugprogramnode2attach_v7"></a>IDebugProgramNode2::Attach_V7

> [!Note]
> 廃止。 使用しないでください。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach_V7 (
   IDebugProgram2*       pMDMProgram,
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason
);
```

```csharp
int Attach_V7 (
   IDebugProgram2       pMDMProgram,
   IDebugEventCallback2 pCallback,
   uint                 dwReason
);
```

## <a name="parameters"></a>パラメーター

`pMDMProgram`\
[in]アタッチするプログラムを表す[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイス。

`pCallback`\
[in]SDM にデバッグ[イベント](../../../extensibility/debugger/reference/idebugeventcallback2.md)を送信するために使用されるインターフェイス。

`dwReason`\
[in]添付の理由を指定する[ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)列挙体の値。

## <a name="return-value"></a>戻り値

実装は常に`E_NOTIMPL`を返す必要があります。

## <a name="remarks"></a>Remarks

> [!WARNING]
> Visual Studio 2005 以降では、このメソッドは使用されなくなり、`E_NOTIMPL`常に を返す必要があります。 プログラム ノードがアタッチできないことを示す必要がある場合、またはプログラム ノードが単にプログラム`GUID`を設定している場合は、別の方法については[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)インターフェイスを参照してください。 それ以外の場合は[、Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドを実装します。

## <a name="prior-to-visual-studio-2005"></a>2005 年より前

このメソッドは、DE がデバッグ対象のプログラムのアドレス空間で実行される場合にのみ実装する必要があります。 それ以外の場合、この`S_FALSE`メソッドは を返す必要があります。

このメソッドが呼び出されると、DE は[、IDebugEngine2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)インターフェイスのこのインスタンスに対してまだ送信されていない場合、および[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugengine2.md)イベント オブジェクトと[IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)イベント オブジェクトを送信する必要があります。 [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) `dwReason`パラメーター[がの](../../../extensibility/debugger/reference/idebugentrypointevent2.md)場合、イベント オブジェクトが送信されます`ATTACH_REASON_LAUNCH`。

DE は[、IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)イベント オブジェクトによって提供される[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクトの[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)メソッドを呼び出す必要があり、そのプログラムの`IDebugProgram2`GUID を DE によって実装されるオブジェクトのインスタンス データに格納する必要があります。

## <a name="see-also"></a>関連項目

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
