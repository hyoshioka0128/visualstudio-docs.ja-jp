---
title: 'IDebugSettingsCallback2:: GetMetricString |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetMetricString
- GetMetricString
ms.assetid: ecc875a2-8ac6-444c-a839-5191a780fd6b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 929783f0fa2c82babf9197f9a0a81108143d1f87
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875823"
---
# <a name="idebugsettingscallback2getmetricstring"></a>IDebugSettingsCallback2::GetMetricString
名前を指定して、メトリックの値の文字列を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMetricString(
    LPCWSTR pszType,
    REFGUID guidSection,
    LPCWSTR pszMetric,
    BSTR*   pbstrValue
);
```

```csharp
private int GetMetricString(
    string     pszType,
    ref Guid   guidSection,
    string     pszMetric,
    out string pbstrValue
);
```

## <a name="parameters"></a>パラメーター
`pszType`\
からメトリックの種類。

`guidSection`\
からセクションの一意識別子。

`pszMetric`\
からメトリックの名前。

`pbstrValue`\
入出力メトリックの値の文字列を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
