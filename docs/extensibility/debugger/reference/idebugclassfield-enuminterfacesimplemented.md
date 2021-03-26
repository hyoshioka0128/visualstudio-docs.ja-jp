---
description: このクラスによって実装されるインターフェイスの列挙子を作成します。
title: 'IDebugClassField:: Enumの実装 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumInterfacesImplemented
helpviewer_keywords:
- IDebugClassField::EnumInterfacesImplemented method
ms.assetid: e5523e45-d350-491e-a92c-fe0ca97d2052
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1763cbcd0a1c61150a054752c94a42f10127251a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088615"
---
# <a name="idebugclassfieldenuminterfacesimplemented"></a>IDebugClassField::EnumInterfacesImplemented
このクラスによって実装されるインターフェイスの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumInterfacesImplemented( 
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumInterfacesImplemented(
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力実装されているインターフェイスの一覧を表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 インターフェイスが存在しない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合、は S_OK を返します。または、このクラスに実装されているインターフェイスがない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>注釈
 列挙体の各要素は、インターフェイスを記述する [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトです。 アンマネージ [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] コードでは、インターフェイスを不連続エンティティとして使用しないので、このメソッドは常にアンマネージコードに対して null 値を返し [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
