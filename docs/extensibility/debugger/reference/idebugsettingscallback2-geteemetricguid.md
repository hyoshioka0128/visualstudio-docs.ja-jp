---
description: 名前を指定して、式エバリュエーターメトリックの一意の識別子を取得します。
title: 'IDebugSettingsCallback2:: GetEEMetricGuid |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetEEMetricGuid
ms.assetid: 3d70c19a-595d-44f1-a7b3-a0cf8f15e371
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 45e858cf78e8b0acf7e50a95d73cd06523396bc1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071377"
---
# <a name="idebugsettingscallback2geteemetricguid"></a>IDebugSettingsCallback2::GetEEMetricGuid
名前を指定して、式エバリュエーターメトリックの一意の識別子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEEMetricGuid(
   REFGUID guidLang,
   REFGUID guidVendor,
   LPCWSTR pszMetric,
   GUID*   pguidValue
);
```

```csharp
HRESULT GetEEMetricGuid(
   ref Guid guidLang,
   ref Guid guidVendor,
   string   pszMetric,
   out Guid pguidValue
);
```

## <a name="parameters"></a>パラメーター
`guidLang`\
からプログラミング言語の一意の識別子。

`guidVendor`\
からベンダーの一意識別子。

`pszMetric`\
からメトリックの名前。

`pguidValue`\
入出力メトリックの一意の識別子を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
