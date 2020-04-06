---
title: フィールド::列挙型パラメーター |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumParameters
helpviewer_keywords:
- IDebugMethodField::EnumParameters method
ms.assetid: d77b1197-deb6-4144-8d1b-8b09949ccfac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13df02cf5870e630c4aecb34e9295d218ba7a0eb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727198"
---
# <a name="idebugmethodfieldenumparameters"></a>IDebugMethodField::EnumParameters
メソッドのパラメーターの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumParameters( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumParameters(
   out IEnumDebugFields ppParams
);
```

## <a name="parameters"></a>パラメーター
`ppParams`\
[アウト]メソッドに[対](../../../extensibility/debugger/reference/ienumdebugfields.md)するパラメーターの一覧を表すオブジェクトを返します。それ以外の場合は、パラメーターがない場合は null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OKを返すか、パラメーターがない場合はS_FALSEを返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 各要素は、さまざまな型のパラメーターを表す[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクトです。 各オブジェクトに対して[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)メソッドを呼び出して、オブジェクトが表すパラメーターの種類を正確に判断します。

 パラメーターには、変数名と型の両方が含まれます。 クラス メソッドの最初のパラメーターは、通常、"this" ポインターです。

 パラメーターの型のみが必要な場合は[、EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)
