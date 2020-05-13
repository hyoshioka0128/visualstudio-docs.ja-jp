---
title: オブジェクトを取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetSize
helpviewer_keywords:
- IDebugObject::GetSize method
ms.assetid: 89af423b-36eb-479d-b2de-2693455eca15
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8fd42abfc056c3b9e50d073ad335f72ac9022aa7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726568"
---
# <a name="idebugobjectgetsize"></a>IDebugObject::GetSize
オブジェクトのサイズをバイト単位で取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSize( 
   UINT* pnSize
);
```

```csharp
int GetSize(
   out uint pnSize
);
```

## <a name="parameters"></a>パラメーター
`pnSize`\
[アウト]サイズをバイト単位で返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)メソッドを使用して、値をバイト シーケンスとして取得します。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
