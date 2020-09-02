---
title: 'IDebugSettingsCallback2:: GetMetricString |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetMetricString
- GetMetricString
ms.assetid: ecc875a2-8ac6-444c-a839-5191a780fd6b
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f20348cdced520b4153f02d2320fcabcd266273d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68164834"
---
# <a name="idebugsettingscallback2getmetricstring"></a>IDebugSettingsCallback2::GetMetricString
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

名前を指定して、メトリックの値の文字列を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
  
#### <a name="parameters"></a>パラメーター  
 `pszType`  
 からメトリックの種類。  
  
 `guidSection`  
 からセクションの一意識別子。  
  
 `pszMetric`  
 からメトリックの名前。  
  
 `pbstrValue`  
 入出力メトリックの値の文字列を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
