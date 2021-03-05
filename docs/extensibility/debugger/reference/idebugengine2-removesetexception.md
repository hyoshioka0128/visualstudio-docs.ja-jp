---
description: 指定された例外を削除して、デバッグエンジンによって処理されないようにします。
title: 'IDebugEngine2:: RemoveSetException |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::RemoveSetException
helpviewer_keywords:
- IDebugEngine2::RemoveSetException
ms.assetid: bdd25097-0e9d-4218-b417-0497ea48d2e8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 588037ef9dcf495f8fbbb210acc3154c31558a32
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153950"
---
# <a name="idebugengine2removesetexception"></a>IDebugEngine2::RemoveSetException
指定された例外を削除して、デバッグエンジンによって処理されないようにします。

## <a name="syntax"></a>構文

```cpp
HRESULT RemoveSetException( 
   EXCEPTION_INFO* pException
);
```

```csharp
int RemoveSetException( 
   EXCEPTION_INFO[] pException
);
```

## <a name="parameters"></a>パラメーター
`pException`\
から削除する例外を記述する [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 削除される例外は、以前に [Setexception](../../../extensibility/debugger/reference/idebugengine2-setexception.md) メソッドを呼び出して設定されている必要があります。

 すべての set 例外を一度に削除するには、 [RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
