---
title: 'IDebugProgramNode2:: Attach_V7 |Microsoft Docs'
description: このインターフェイスメソッドは、Visual Studio 2005 より前に使用されていた、古い非推奨の attach メソッドです。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::Attach
helpviewer_keywords:
- IDebugProgramNode2::Attach_V7
- IDebugProgramNode2::Attach
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c949bba45457917e4dd00bdc05bc300f3a38eb7e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053595"
---
# <a name="idebugprogramnode2attach_v7"></a>IDebugProgramNode2::Attach_V7

> [!Note]
> れ. 使用しないでください。

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
からアタッチ先のプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイス。

`pCallback`\
からデバッグイベントを SDM に送信するために使用される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) インターフェイス。

`dwReason`\
からアタッチの理由を指定する [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 列挙の値。

## <a name="return-value"></a>戻り値

実装は常にを返す必要があり `E_NOTIMPL` ます。

## <a name="remarks"></a>注釈

> [!WARNING]
> Visual Studio 2005 の時点では、このメソッドは使用されなくなり、常にを返す必要があり `E_NOTIMPL` ます。 プログラムノードがに接続できないことを示す必要がある場合、またはプログラムノードがプログラムを単に設定している場合は、 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md) インターフェイスで別の方法を参照してください `GUID` 。 それ以外の場合は、 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドを実装します。

## <a name="prior-to-visual-studio-2005"></a>Visual Studio 2005 より前

このメソッドは、デバッグ中のプログラムのアドレス空間で DE を実行する場合にのみ実装する必要があります。 それ以外の場合、このメソッドはを返し `S_FALSE` ます。

このメソッドが呼び出されると、DE は、 [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) イベントオブジェクト ( [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) インターフェイスのこのインスタンスに対してまだ送信されていない場合)、および [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) および [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) イベントオブジェクトを送信する必要があります。 パラメーターがの場合、 [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) イベントオブジェクトが送信され `dwReason` `ATTACH_REASON_LAUNCH` ます。

DE は、 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) event オブジェクトによって提供される[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクトの[getprogramid](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)メソッドを呼び出す必要があり `IDebugProgram2` ます。また、de によって実装されたオブジェクトのインスタンスデータにそのプログラムの GUID を格納する必要があります。

## <a name="see-also"></a>こちらもご覧ください

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
