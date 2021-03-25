---
description: スレッドの実行を再開します。
title: 'IDebugThread2:: Resume |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 93552bac60d16a21212bfa89816481cf7099d399
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053023"
---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
スレッドの実行を再開します。

## <a name="syntax"></a>構文

```cpp
HRESULT Resume ( 
   DWORD *pdwSuspendCount
);
```

```csharp
int Resume ( 
   out uint pdwSuspendCount
);
```

## <a name="parameters"></a>パラメーター
`pdwSuspendCount`\
入出力再開操作後の中断回数を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドを呼び出すたびに、0に達するまで中断回数が減少します。この時間が経過すると、実行は実際に再開されます。 この中断回数は、[ **スレッド** デバッグ] ウィンドウに表示されます。

 このメソッドを呼び出すたびに、前に [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md) メソッドを呼び出す必要があります。 中断カウントは、これ `IDebugThread2::Suspend` までにメソッドが呼び出された回数を決定します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [[中断]](../../../extensibility/debugger/reference/idebugthread2-suspend.md)
