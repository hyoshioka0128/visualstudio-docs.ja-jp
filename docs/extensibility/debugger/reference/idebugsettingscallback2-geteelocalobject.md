---
description: メトリック名を指定して、式エバリュエーターローカルオブジェクトを取得します。
title: 'IDebugSettingsCallback2:: GetEELocalObject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetEELocalObject
ms.assetid: e69a3469-a049-420c-b918-c48a1e7b9baf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f8dc96d8eaabbae8b9cea155cf72f2958b6b942b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075654"
---
# <a name="idebugsettingscallback2geteelocalobject"></a>IDebugSettingsCallback2::GetEELocalObject
メトリック名を指定して、式エバリュエーターローカルオブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEELocalObject(
   REFGUID     guidLang,
   REFGUID     guidVendor,
   LPCWSTR     pszMetric,
   IUnknown ** ppUnk
);
```

```csharp
private int GetEELocalObject(
   ref Guid          guidLang,
   ref Guid          guidVendor,
   string            pszMetric,
   out System.Object ppUnk
);
```

## <a name="parameters"></a>パラメーター
`guidLang`\
からプログラミング言語の一意の識別子。

`guidVendor`\
からベンダーの一意識別子。

`pszMetric`\
からメトリックの名前。

`ppUnk`\
入出力式エバリュエーターローカルオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
