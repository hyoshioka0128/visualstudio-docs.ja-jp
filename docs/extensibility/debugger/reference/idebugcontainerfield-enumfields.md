---
title: フィールドを列挙します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField::EnumFields
helpviewer_keywords:
- IDebugContainerField::EnumFields method
ms.assetid: 9e5e681b-ad49-4c62-bd95-4afa11d61a57
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: afc461d52f81afc2c2e7127a90313bea7b9dacf3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733226"
---
# <a name="idebugcontainerfieldenumfields"></a>IDebugContainerField::EnumFields
コンテナーのフィールドの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumFields( 
   FIELD_KIND         dwKindFilter,
   FIELD_MODIFIERS    dwModifiersFilter,
   LPCOLESTR          pszNameFilter,
   NAME_MATCH         nameMatch,
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumFields(
   enum_ FIELD_KIND      dwKindFilter,
   enum_ FIELD_MODIFIERS dwModifiersFilter,
   string                pszNameFilter,
   NAME_MATCH            nameMatch,
   out IEnumDebugFields  ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwKindFilter`\
[in]列挙するフィールドを選択する[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)定数の組み合わせ。 フィールドの種類は、クラスやプリミティブなどのストレージの種類、またはローカル、パラメーター、または "this" ポインターなどの特定の情報を記述できます。

`dwModifiersFilter`\
[in]列挙するフィールドを選択する[FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)定数の組み合わせ。 フィールド修飾子には、パブリック、プライベートなどのアクセス許可、または仮想、静的、最終などのストレージ情報を指定できます。

`pszNameFilter`\
[in]列挙するフィールドの名前。 すべてのフィールドが返される場合は、NULL 値になります。

`nameMatch`\
[in]検索で大文字と小文字を区別するかどうかを制御する[NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)列挙体の値。

`ppEnum`\
[アウト]フィールドの[一](../../../extensibility/debugger/reference/ienumdebugfields.md)覧を表すオブジェクトを返します。 フィールドがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、フィールドがない場合はS_OKまたはS_FALSEを返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 たとえば`dwKindFilter`、"MyMethod"`dwModifiersFilter`という名前のすべてのパブリック仮想メソッドを選択するために、パラメータ、、、および`pszNameFilter`パラメータを組み合わせることができます。

## <a name="see-also"></a>関連項目
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
