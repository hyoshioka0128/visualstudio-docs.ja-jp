---
title: Iデバッグフィールド::イコール |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::Equal
helpviewer_keywords:
- IDebugField::Equal method
ms.assetid: 75369fe6-ddd3-497d-80d1-2488e6100e9f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8a45a31c02376f95c3cd6b0c4a4adf0434fabe92
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729015"
---
# <a name="idebugfieldequal"></a>IDebugField::Equal
このメソッドは、このフィールドと指定されたフィールドを比較して等しいかどうかを確認します。

## <a name="syntax"></a>構文

```cpp
HRESULT Equal( 
   IDebugField* pField
);
```

```csharp
int Equal(
   IDebugField pField
);
```

## <a name="parameters"></a>パラメーター
`pField`\
[in]このフィールドと比較するフィールド。

## <a name="return-value"></a>戻り値
 フィールドが同じ場合は、`S_OK`を返します。 フィールドが異なる場合は、`S_FALSE.`それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
