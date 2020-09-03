---
title: 'IDebugMethodField:: EnumStaticLocals |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumStaticLocals
helpviewer_keywords:
- IDebugMethodField::EnumStaticLocals method
ms.assetid: e0c522c4-f759-4c32-ae87-7abcb573e77d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6e0a89b4c1ac4318b6dd070dc086b86b45ad24fa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727155"
---
# <a name="idebugmethodfieldenumstaticlocals"></a>IDebugMethodField::EnumStaticLocals
メソッドの静的ローカル変数の列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumStaticLocals( 
   IEnumDebugFields** ppLocals
);
```

```csharp
int EnumStaticLocals(
   out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>パラメーター
`ppLocals`\
入出力静的ローカル変数のリストを表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 静的ローカル変数がない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK を返すか、静的ローカル変数がない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 各要素は、さまざまな種類の静的ローカル変数を表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトです。 各オブジェクトの [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md) メソッドを呼び出して、オブジェクトが表す静的ローカルの種類を正確に特定します。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
