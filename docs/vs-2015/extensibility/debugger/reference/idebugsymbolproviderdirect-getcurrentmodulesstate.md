---
title: 'IDebugSymbolProviderDirect:: Getcurrentモジュール State |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- GetCurrentModulesState
- IDebugSymbolProviderDirect::GetCurrentModulesState
ms.assetid: a0c85318-5686-4eed-b213-21f2b9e681e6
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 49e623c22bea7cedb2918cd0467bb7540f8fb96f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155137"
---
# <a name="idebugsymbolproviderdirectgetcurrentmodulesstate"></a>IDebugSymbolProviderDirect::GetCurrentModulesState
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

シンボルプロバイダーがメンバーとなっているシンボルグループに関する情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetCurrentModulesState(  
    DWORD*          pState,  
    unsigned long * count  
);  
```  
  
```csharp  
int GetCurrentModulesState(  
    out uint pState,  
    out uint count  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pState`  
 入出力シンボルプロバイダーグループの状態。  
  
 `count`  
 入出力グループ内のモジュールの数。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 モジュールがシンボルグループに追加されるか、シンボルグループから削除されるたびに、状態が変更されます。 そのため、このメソッドを使用して、シンボルグループが変更されているかどうかを検出できます。  
  
## <a name="see-also"></a>参照  
 [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)
