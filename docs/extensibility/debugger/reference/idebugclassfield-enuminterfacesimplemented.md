---
title: 'IDebugClassField:: Enumの実装 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumInterfacesImplemented
helpviewer_keywords:
- IDebugClassField::EnumInterfacesImplemented method
ms.assetid: e5523e45-d350-491e-a92c-fe0ca97d2052
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b7283d8a2996d5ab4dfc52cde446170e7632c27c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876083"
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

## <a name="remarks"></a>解説
 列挙体の各要素は、インターフェイスを記述する [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトです。 アンマネージ [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] コードでは、インターフェイスを不連続エンティティとして使用しないので、このメソッドは常にアンマネージコードに対して null 値を返し [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] ます。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
