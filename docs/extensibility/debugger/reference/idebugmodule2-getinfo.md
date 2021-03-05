---
description: このモジュールに関する情報を取得します。
title: 'IDebugModule2:: GetInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2::GetInfo
helpviewer_keywords:
- GetInfo method
- IDebugModule2::GetInfo method
ms.assetid: de337e66-294f-4ac9-b21e-71fac7418e36
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a31c6e40f18e3b405449179e3e5a3ea1a42acc6f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150564"
---
# <a name="idebugmodule2getinfo"></a>IDebugModule2::GetInfo
このモジュールに関する情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetInfo( 
   MODULE_INFO_FIELDS dwFields,
   MODULE_INFO*       pInfo
);
```

```cpp
int GetInfo( 
   enum_MODULE_INFO_FIELDS dwFields,
   MODULE_INFO[]           pInfo
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
からどのフィールドを入力するかを指定する、 [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md) 列挙のフラグの組み合わせ `pInfo` 。

`pInfo`\
[入力、出力]モジュールの説明を入力する [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)構造体には、[**モジュール**] ウィンドウに表示されるモジュールの名前が含まれています。

## <a name="see-also"></a>関連項目
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
