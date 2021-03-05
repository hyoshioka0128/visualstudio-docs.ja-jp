---
description: 名前を指定して、式エバリュエーターのメトリックの値の文字列を取得します。
title: 'IDebugSettingsCallback2:: GetEEMetricString |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetEEMetricString
ms.assetid: 85e3c093-6a91-4101-ab32-d8ac6eed4918
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4e5fa78173eeb74ae5f0137805c09298304abd65
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168752"
---
# <a name="idebugsettingscallback2geteemetricstring"></a>IDebugSettingsCallback2::GetEEMetricString
名前を指定して、式エバリュエーターのメトリックの値の文字列を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEEMetricString(
   REFGUID guidLang,
   REFGUID guidVendor,
   LPCWSTR pszMetric,
   BSTR*   pbstrValue
);
```

```csharp
private int GetEEMetricString(
   ref Guid   guidLang,
   ref Guid   guidVendor,
   string     pszMetric,
   out string pbstrValue
);
```

## <a name="parameters"></a>パラメーター
`guidLang`\
からプログラミング言語の一意の識別子。

`guidVendor`\
からベンダーの一意識別子。

`pszMetric`\
からメトリックの名前。

`pbstrValue`\
入出力メトリック値の文字列を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
