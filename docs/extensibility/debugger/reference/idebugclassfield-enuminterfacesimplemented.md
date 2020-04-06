---
title: インターフェイスの実装マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumInterfacesImplemented
helpviewer_keywords:
- IDebugClassField::EnumInterfacesImplemented method
ms.assetid: e5523e45-d350-491e-a92c-fe0ca97d2052
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 91d9cac6b695ba2a0d34da776fa79ba62ba2e015
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734489"
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
[アウト]実装されている[インターフェイス](../../../extensibility/debugger/reference/ienumdebugfields.md)の一覧を表すオブジェクトを返します。 インターフェイスがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、このクラスに実装されているインターフェイスがない場合は、S_OKを返すか、S_FALSEを返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 列挙体の各要素は、インターフェイスを記述する[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)オブジェクトです。 アンマネージ[!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)]コードでは、インターフェイスを個別のエンティティとして使用しないため、このメソッドは常にアンマネージ[!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)]コードの null 値を返します。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
