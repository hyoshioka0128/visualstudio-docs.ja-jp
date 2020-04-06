---
title: を使用します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::RemoveSetException
helpviewer_keywords:
- IDebugEngine2::RemoveSetException
ms.assetid: bdd25097-0e9d-4218-b417-0497ea48d2e8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e811ce2e387c299ff3655799bf35185c1d2029b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730926"
---
# <a name="idebugengine2removesetexception"></a>IDebugEngine2::RemoveSetException
デバッグ エンジンで処理されないように、指定した例外を削除します。

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
[in]削除する例外を記述する[EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)構造体。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 削除される例外は[、SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)メソッドの以前の呼び出しによって事前に設定されている必要があります。

 一度にすべての設定された例外を削除するには、メソッドを呼び出[します](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
