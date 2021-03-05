---
description: プログラムにセッションをアタッチします。
title: 'IDebugProgramEx2:: Attach |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2::Attach
helpviewer_keywords:
- IDebugProgramEx2::Attach
ms.assetid: 33b22b2f-431e-4205-9441-d28a9c928c97
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa9a66bdec3da9b6d18772b4ff2c85a7874bde6c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150147"
---
# <a name="idebugprogramex2attach"></a>IDebugProgramEx2::Attach
プログラムにセッションをアタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason,
   IDebugSession2*       pSession
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   uint                 dwReason,
   IDebugSession2       pSession
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
からアタッチされたデバッグエンジンがイベントを送信するコールバック関数を表す [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`dwReason`\
からアタッチ操作の理由を説明する [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 列挙の値。

`pSession`\
からプログラムにアタッチしているセッションを一意に識別する値。

## <a name="return-value"></a>戻り値
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 `E_ATTACH_DEBUGGER_ALREADY_ATTACHED`プログラムが既にアタッチされている場合、このメソッドはを返します。

## <a name="remarks"></a>解説
 プログラムを含むポートは、の値を使用して、 `pSession` どのセッションがプログラムにアタッチしようとしているかを判断できます。 たとえば、ポートで一度に1つのデバッグセッションだけをプロセスにアタッチできる場合、ポートでは、同じセッションがプロセス内の他のプログラムに既にアタッチされているかどうかを判断できます。

> [!NOTE]
> 渡されるインターフェイスは、 `pSession` クッキーとしてのみ扱われます。これは、このプログラムにアタッチするセッションデバッグマネージャーを一意に識別する値です。指定されたインターフェイスのメソッドは機能しません。

## <a name="see-also"></a>関連項目
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
