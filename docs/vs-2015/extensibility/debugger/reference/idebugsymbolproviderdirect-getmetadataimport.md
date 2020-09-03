---
title: 'IDebugSymbolProviderDirect:: GetMetaDataImport |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- GetMetaDataImport
- IDebugSymbolProviderDirect::GetMetaDataImport
ms.assetid: b51a492c-af00-4b08-93fb-6c19ee4916aa
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 738169ece185bfc4b861b8f8220199dbf3c762b1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155128"
---
# <a name="idebugsymbolproviderdirectgetmetadataimport"></a>IDebugSymbolProviderDirect::GetMetaDataImport
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

メタデータのインポート情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetMetaDataImport (  
    GUID*      guid,  
    DWORD      appID,  
    IUnknown** ppImport  
);  
```  
  
```csharp  
int GetMetaDataImport (  
    Guid       guid,  
    uint       appID,  
    out object ppImport  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `guid`  
 からモジュールの一意の識別子。  
  
 `appID`  
 からアプリケーションドメインの識別子。  
  
 `ppImport`  
 入出力メタデータのインポート情報を格納しているオブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)
