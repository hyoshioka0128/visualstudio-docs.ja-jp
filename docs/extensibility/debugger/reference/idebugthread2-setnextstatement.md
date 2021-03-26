---
description: 現在の命令ポインターを指定されたコードコンテキストに設定します。
title: 'IDebugThread2:: SetNextStatement |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::SetNextStatement
helpviewer_keywords:
- IDebugThread2::SetNextStatement
ms.assetid: 9e2834dd-4ecf-45af-8e6c-f9318ebdac06
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5dd6bd027a9938b7dce855742cc351180498bb8b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081166"
---
# <a name="idebugthread2setnextstatement"></a>IDebugThread2::SetNextStatement
現在の命令ポインターを指定されたコードコンテキストに設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetNextStatement ( 
   IDebugStackFrame2*  pStackFrame,
   IDebugCodeContext2* pCodeContext
);
```

```csharp
int SetNextStatement ( 
   IDebugStackFrame2  pStackFrame,
   IDebugCodeContext2 pCodeContext
);
```

## <a name="parameters"></a>パラメーター
`pStackFrame`\
将来使用するために予約されています。を null 値に設定します。

`pCodeContext`\
から実行されるコードの場所とそのコンテキストを記述する [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 次の表に、その他の使用可能な値を示します。

|値|説明|
|-----------|-----------------|
|E_CANNOT_SET_NEXT_STATEMENT_ON_NONLEAF_FRAME|次のステートメントは、フレームスタックを深く掘り下げたスタックフレーム内に存在することはできません。|
|E_CANNOT_SETIP_TO_DIFFERENT_FUNCTION|次のステートメントは、スタック内のどのフレームにも関連付けられていません。|
|E_CANNOT_SET_NEXT_STATEMENT_ON_EXCEPTION|一部のデバッグエンジンでは、例外の後に次のステートメントを設定することはできません。|

## <a name="remarks"></a>注釈
 命令ポインターは、次に実行する命令またはステートメントを示します。 このメソッドは、ソースコードの行を再試行したり、別の関数で実行を強制するために使用されます。たとえば、のようになります。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
