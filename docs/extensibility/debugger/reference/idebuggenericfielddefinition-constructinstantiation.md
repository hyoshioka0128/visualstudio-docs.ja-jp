---
title: ジェネリックフィールド定義::構築インスタンス化 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ConstructInstantiation
- IDebugGenericFieldDefinition::ConstructInstantiation
ms.assetid: ef8ae261-a98b-4dc2-93b3-7c5191818ba2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 352018e50b955ed414af974bc21b62775fd55f53
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728265"
---
# <a name="idebuggenericfielddefinitionconstructinstantiation"></a>IDebugGenericFieldDefinition::ConstructInstantiation
引数型の配列を指定してフィールド インスタンスを構築します。

## <a name="syntax"></a>構文

```cpp
HRESULT ConstructInstantiation(
   ULONG32       cArgs,
   IDebugField** ppArgs,
   IDebugField** ppConstructedField
);
```

```csharp
int ConstructInstantiation(
   uint            cArgs,
   IDebugField[]   ppArgs,
   out IDebugField ppConstructedField
);
```

## <a name="parameters"></a>パラメーター
`cArgs`\
[in]配列内の引数の`ppArgs`数。

`ppArgs`\
[in]型引数を格納する配列。 型引数は、クローズ型 (ジェネリック型または完全にインスタンス化されたジェネリック型以外) である必要があります。

`ppConstructedField`\
[アウト]新しいフィールドを表す[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 制約はチェックされません。

## <a name="see-also"></a>関連項目
- [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)
