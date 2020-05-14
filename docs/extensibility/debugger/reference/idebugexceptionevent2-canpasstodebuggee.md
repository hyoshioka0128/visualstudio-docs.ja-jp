---
title: イベント 2::スキャンパスデバッグジー |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729872"
---
# <a name="idebugexceptionevent2canpasstodebuggee"></a>IDebugExceptionEvent2::CanPassToDebuggee
デバッグ エンジン (DE) が、実行が再開されたときにデバッグ中のプログラムにこの例外を渡すオプションをサポートするかどうかを決定します。

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
 `S_OK` (例外はプログラムに渡すことができます)、または`S_FALSE`(例外を渡すことはできません) を返します。

## <a name="remarks"></a>Remarks
 デは、デバッグ対象に渡すための既定のアクションを持っている必要があります。 IDE は[、IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)イベントを受け[Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)取り、メソッドを`CanPassToDebuggee`呼び出さずに Continue メソッドを呼び出す可能性があります。 したがって、DE には例外を渡すかどうかのデフォルトのケースが必要です。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [続行](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
