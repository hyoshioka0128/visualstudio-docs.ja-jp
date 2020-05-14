---
title: クエリ 2::列挙カスタム属性 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::EnumCustomAttributes
helpviewer_keywords:
- IDebugCustomAttributeQuery2::EnumCustomAttributes
ms.assetid: 94bfce74-aa3d-45f0-8e04-5715faf85217
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5b00ead2236a36c2fa12e1ad154b9f853aa2224d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732588"
---
# <a name="idebugcustomattributequery2enumcustomattributes"></a>IDebugCustomAttributeQuery2::EnumCustomAttributes
このフィールドにアタッチされているすべてのカスタム属性の列挙子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumCustomAttributes( 
   IEnumDebugCustomAttributes** ppEnum
);
```

```csharp
int EnumCustomAttributes(
   out IEnumDebugCustomAttributes ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
[アウト]カスタム属性[の](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)リストを表すオブジェクトを返します。それ以外の場合は、カスタム属性がない場合は null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、このフィールドにカスタム属性がない場合は、S_OKまたはS_FALSEを返します。 それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 フィールドには複数のカスタム属性を設定できます。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
