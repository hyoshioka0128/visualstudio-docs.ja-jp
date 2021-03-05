---
description: インターセプトされた例外の処理が完了したときに呼び出されます。
title: IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
helpviewer_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
ms.assetid: 07b20866-e598-4783-9ecc-6aa8625c8804
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 70fb92c20eab3700043a11f8544896bbbce3b7c6
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102172533"
---
# <a name="idebuginterceptexceptioncompleteevent2getinterceptcookie"></a>IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
インターセプトされた例外の処理が完了したときに呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetInterceptCookie(
   UINT64* pqwCookie
);
```

```csharp
int GetInterceptCookie(
   out ulong pqwCookie
);
```

## <a name="parameters"></a>パラメーター
`pqwCookie`\
入出力インターセプトされた例外に関連付けられている一意の値。

## <a name="return-value"></a>戻り値
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。

## <a name="remarks"></a>解説
 [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)メソッドによってインターセプトされた例外の処理が完了すると、 [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)イベントが送信されます。 ハンドラーは、メソッドを使用して、 `GetInterceptCookie` 例外に関連付けられている一意の値 (メソッドに渡されたものと同じ値) を取得でき `InterceptCurrentException` ます。

## <a name="see-also"></a>関連項目
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)
