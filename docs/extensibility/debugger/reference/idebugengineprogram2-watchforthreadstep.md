---
title: 'IDebugEngineProgram2:: WatchForThreadStep |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForThreadStep
helpviewer_keywords:
- IDebugEngineProgram2::WatchForThreadStep
ms.assetid: b70922a3-1313-409a-b3b7-50c7cd13e394
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8168b0813eb99f4f70c8a5d8ffbdae4f6fce2094
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892620"
---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
指定されたスレッドで実行を監視します (または実行の監視を停止します)。

## <a name="syntax"></a>構文

```cpp
HRESULT WatchForThreadStep( 
   IDebugProgram2* pOriginatingProgram,
   DWORD           dwTid,
   BOOL            fWatch,
   DWORD           dwFrame
);
```

```csharp
int WatchForThreadStep( 
   IDebugProgram2 pOriginatingProgram,
   uint           dwTid,
   int            fWatch,
   uint           dwFrame
);
```

## <a name="parameters"></a>パラメーター
`pOriginatingProgram`\
から階段状のプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

`dwTid`\
から監視するスレッドの識別子を指定します。

`fWatch`\
から0以外 ( `TRUE` ) は、で識別されるスレッドで実行の監視を開始することを意味します。 `dwTid` それ以外の場合、ゼロ ( `FALSE` ) はでの実行の監視を停止 `dwTid` します。

`dwFrame`\
からステップの種類を制御するフレームインデックスを指定します。 この値がゼロ (0) の場合、ステップの種類は "ステップイン" であり、によって識別されるスレッドが実行されるたびにプログラムが停止し `dwTid` ます。 `dwFrame`が0以外の場合、ステップの種類は "ステップオーバー" であり、で識別されるスレッド `dwTid` が、よりも大きいインデックスを持つフレームで実行されている場合にのみ、プログラムが停止し `dwFrame` ます。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 セッションデバッグマネージャー (SDM) が、パラメーターで識別されるプログラムをステップ実行すると、 `pOriginatingProgram` このメソッドを呼び出すことによって、アタッチされている他のすべてのプログラムに通知します。

 このメソッドは、同じスレッドのステップ実行にのみ適用できます。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
