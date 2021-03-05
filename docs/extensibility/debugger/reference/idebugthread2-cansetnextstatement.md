---
description: 現在の命令ポインターを特定のスタックフレームに設定できるかどうかを判断します。
title: 'IDebugThread2:: CanSetNextStatement |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::CanSetNextStatement
helpviewer_keywords:
- IDebugThread2::CanSetNextStatement
ms.assetid: 7014af80-ff4f-4790-a34b-0528918d1fa3
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4b07eb23127abedc4e41af2795c3452401c3e670
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168388"
---
# <a name="idebugthread2cansetnextstatement"></a>IDebugThread2::CanSetNextStatement
現在の命令ポインターを特定のスタックフレームに設定できるかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanSetNextStatement ( 
   IDebugStackFrame2*  pStackFrame,
   IDebugCodeContext2* pCodeContext
);
```

```csharp
int CanSetNextStatement ( 
   IDebugStackFrame2  pStackFrame,
   IDebugCodeContext2 pCodeContext
);
```

## <a name="parameters"></a>パラメーター
`pStackFrame`\
将来使用するために予約されています。を null 値に設定します。 Null 値の場合は、現在のスタックフレームを使用します。

`pCodeContext`\
から実行されるコードの場所とそのコンテキストを記述する [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドがを返す場合は `S_OK` 、 [setnextstatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md) メソッドを呼び出して、次のステートメントを実際に設定します。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
