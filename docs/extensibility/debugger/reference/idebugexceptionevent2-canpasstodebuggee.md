---
title: 'IDebugExceptionEvent2:: Can Stoデバッグ |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
ms.assetid: ae4bbe0a-fbe1-49be-a310-ea64279a434b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ab57f599214cfbd7a1f5fcca15fa104b072d1d48
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729872"
---
# <a name="idebugexceptionevent2canpasstodebuggee"></a>IDebugExceptionEvent2::CanPassToDebuggee
デバッグエンジン (DE) が、実行の再開時にデバッグ対象のプログラムにこの例外を渡すオプションをサポートするかどうかを決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanPassToDebuggee(
   void
);
```

```csharp
int CanPassToDebuggee();
```

## <a name="return-value"></a>戻り値
 `S_OK`(例外はプログラムに渡すことができます) または (例外を渡すことはできません) のいずれかを返し `S_FALSE` ます。

## <a name="remarks"></a>解説
 DE には、デバッグ対象に渡すための既定のアクションが必要です。 IDE は、 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) イベントを受け取り、メソッドを呼び出さずに [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md) メソッドを呼び出すことができ `CanPassToDebuggee` ます。 そのため、DE には、例外をに渡す既定のケースが含まれている必要があります。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [続行](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
