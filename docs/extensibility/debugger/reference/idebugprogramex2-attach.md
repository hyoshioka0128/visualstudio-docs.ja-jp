---
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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fcb52a96074b783043af1e908cf454466df74c30
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722379"
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
