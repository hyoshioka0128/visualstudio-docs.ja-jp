---
description: このメソッドは、デバッグプロセスの指定されたプロパティ値を照会します。
title: 'IDebugProcessQueryProperties:: QueryProperties |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties::QueryProperties
ms.assetid: 976a9962-b689-45bb-afb6-16b2c5dbc3b8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2e2f4d36c911e3b41d86e9cc0480c97979d63897
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081387"
---
# <a name="idebugprocessquerypropertiesqueryproperties"></a>IDebugProcessQueryProperties::QueryProperties
このメソッドは、デバッグプロセスの指定されたプロパティ値を照会します。

## <a name="syntax"></a>構文

```cpp
HRESULT QueryProperties(
   ULONG                  celt,
   PROCESS_PROPERTY_TYPE *rgdwPropTypes,
   VARIANT               *rgtPropValues);
```

```csharp
int QueryProperties(
   uint                       celt,
   enum_PROCESS_PROPERTY_TYPE rgdwPropTypes,
   out object[ ]              rgtPropValues);
```

## <a name="parameters"></a>パラメーター
`celt`\
からプロパティ定義とプロパティ値を含む配列のサイズ。

`dwPropType`\
からクエリ対象のプロパティの定義を格納している配列。 次の値を指定できます。

- PROCESS_PROPERTY_COMMAND_LINE = 1

- PROCESS_PROPERTY_CURRENT_DIRECTORY = 2

- PROCESS_PROPERTY_ENVIRONMENT_VARIABLES = 3

`pvarPropValue`\
入出力プロパティ値を格納している配列。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドはほとんど使用されません。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcessQueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties.md)
