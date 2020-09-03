---
title: IDebugExceptionEvent2::P assToDebuggee |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729837"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
例外を、実行の再開時にデバッグされるプログラムに渡すか、または例外を破棄する必要があるかを指定します。

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
から`TRUE`実行が再開されたときにデバッグ対象のプログラムに例外を渡す必要がある場合は0以外 ()、例外を破棄する必要がある場合は 0 ( `FALSE` )。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドを呼び出すと、実際には、デバッグ中のプログラムでコードが実行されることはありません。 呼び出しは、次のコード実行の状態を設定するだけです。 たとえば、 [canパスワード](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)を使用するメソッドを呼び出すと、EXCEPTION_INFO が返される場合があり `S_OK` ます。 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)`dwState` フィールドをに設定 `EXCEPTION_STOP_SECOND_CHANCE` します。

 IDE は、 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) イベントを受け取り、 [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md) メソッドを呼び出すことができます。 デバッグエンジン (DE) には、メソッドが呼び出されない場合にそのケースを処理するための既定の動作が必要です `PassToDebuggee` 。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)
- [続行](../../../extensibility/debugger/reference/idebugprogram2-continue.md)
