---
description: このメソッドは、デバッグプロセスの指定されたプロパティ値を照会します。
title: 'IDebugProcessQueryProperties:: QueryProperty |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties::QueryProperty
ms.assetid: 9a91707d-a590-44ef-b122-69d9816a7a79
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9814ff2dd377d1a10895f6ec5ba0818f480bfcf3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081400"
---
# <a name="idebugprocessquerypropertiesqueryproperty"></a>IDebugProcessQueryProperties::QueryProperty
このメソッドは、デバッグプロセスの指定されたプロパティ値を照会します。

## <a name="syntax"></a>構文

```cpp
HRESULT QueryProperty(
   PROCESS_PROPERTY_TYPE  dwPropType,
   VARIANT               *pvarPropValue);
```

```csharp
int QueryProperty(
   enum_PROCESS_PROPERTY_TYPE dwPropType,
   out object                 pvarPropValue);
```

## <a name="parameters"></a>パラメーター
`dwPropType`\
からクエリ対象のプロパティの定義。 値は次のとおりです。

- PROCESS_PROPERTY_COMMAND_LINE = 1

- PROCESS_PROPERTY_CURRENT_DIRECTORY = 2

- PROCESS_PROPERTY_ENVIRONMENT_VARIABLES = 3

`pvarPropValue`\
入出力プロパティの値。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドはほとんど使用されません。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcessQueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties.md)
