---
title: 'IDebugGenericFieldDefinition:: 構築 Tインスタンス化 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ConstructInstantiation
- IDebugGenericFieldDefinition::ConstructInstantiation
ms.assetid: ef8ae261-a98b-4dc2-93b3-7c5191818ba2
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 60ab91340c0f9baf9a75e6e283d3c1158bdbea3b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99911113"
---
# <a name="idebuggenericfielddefinitionconstructinstantiation"></a>IDebugGenericFieldDefinition::ConstructInstantiation
型引数の配列を指定して、フィールドインスタンスを構築します。

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
から配列内の引数の数 `ppArgs` 。

`ppArgs`\
から型引数を格納している配列。 型引数は、閉じられた型 (非ジェネリックまたは完全にインスタンス化されたジェネリック) である必要があります。

`ppConstructedField`\
入出力新しいフィールドを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 制約はチェックされません。

## <a name="see-also"></a>関連項目
- [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)
