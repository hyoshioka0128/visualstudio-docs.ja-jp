---
title: コールバック2::ゲットメトリックGuid |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetMetricGuid
ms.assetid: 91092763-3362-4857-adf0-231bc1254206
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 08f03e0d09db17e3dbcda30588191ff3efcb1c41
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719977"
---
# <a name="idebugsettingscallback2getmetricguid"></a>IDebugSettingsCallback2::GetMetricGuid
指定された名前のメトリックの一意の識別子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMetricGuid(
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   GUID*   pguidValue
);
```

```csharp
private int GetMetricGuid(
   string   pszType,
   ref Guid guidSection,
   string   pszMetric,
   out Guid pguidValue
);
```

## <a name="parameters"></a>パラメーター
`pszType`\
[in]メトリックの種類。

`guidSection`\
[in]セクションを表す一意の識別子です。

`pszMetric`\
[in]メトリックの名前。

`pguidValue`\
[アウト]メトリックの一意の識別子を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
