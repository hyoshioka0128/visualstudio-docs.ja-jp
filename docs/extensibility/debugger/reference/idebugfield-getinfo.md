---
title: Iデバッグフィールド::ゲットインフォ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetInfo
helpviewer_keywords:
- IDebugField::GetInfo method
ms.assetid: 7d508200-89ce-400f-a8ea-f28e7610cb2b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1b3251db3426f87901ca0768800feaa36fef5373
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728843"
---
# <a name="idebugfieldgetinfo"></a>IDebugField::GetInfo
このメソッドは、フィールドに関する表示可能な情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetInfo( 
   FIELD_INFO_FIELDS dwFields,
   FIELD_INFO* pFieldInfo
);
```

```csharp
int GetInfo(
   enum_FIELD_INFO_FIELDS dwFields,
   FIELD_INFO[] pFieldInfo
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
[in]表示する情報を選択する[FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md)定数の組み合わせ。 フィールドがシンボルを表す場合、通常はシンボル名と型になります。

`pFieldInfo`\
[アウト]指定された[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)構造体の情報を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
