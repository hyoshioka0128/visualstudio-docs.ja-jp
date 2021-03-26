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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 69286a7bf50c32aa3aa720deff78ee957f53fc65
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065659"
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

## <a name="remarks"></a>注釈
 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)構造体には、[**モジュール**] ウィンドウに表示されるモジュールの名前が含まれています。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
