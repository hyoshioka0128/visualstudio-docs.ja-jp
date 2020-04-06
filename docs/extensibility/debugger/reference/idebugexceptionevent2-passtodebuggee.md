---
title: イベント2::PassToDebugジー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::PassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::PassToDebuggee
ms.assetid: a20d0f0b-2ca0-4437-bd22-9213c81d2738
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aec6f460295b59b2b5455b83d5b0be554bca24fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729837"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
実行が再開されるときに、デバッグ中のプログラムに例外を渡すか、または例外を破棄するかを指定します。

## <a name="syntax"></a>構文

```cpp
HRESULT PassToDebuggee(
   BOOL fPass
);
```

```csharp
int PassToDebuggee(
   int fPass
);
```

## <a name="parameters"></a>パラメーター
`fPass`\
[in]実行が`TRUE`再開されるときに、デバッグ中のプログラムに例外を渡す場合は 0 以外 ( ) 、`FALSE`例外を破棄する場合は 0 ( ) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを呼び出しても、実際にはデバッグ中のプログラムでコードが実行されるわけではありません。 呼び出しは、次のコード実行の状態を設定するだけです。 たとえば[、CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)メソッドの呼び出し`S_OK`は[、EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)で返される場合があります。`dwState` フィールドを`EXCEPTION_STOP_SECOND_CHANCE`に設定します。

 IDE は[、イベント](../../../extensibility/debugger/reference/idebugexceptionevent2.md)を受け取り[、Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)メソッドを呼び出す可能性があります。 デバッグ エンジン (DE) は、メソッドが呼び出されない場合`PassToDebuggee`、ケースを処理する既定の動作を持っている必要があります。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)
- [続行](../../../extensibility/debugger/reference/idebugprogram2-continue.md)
