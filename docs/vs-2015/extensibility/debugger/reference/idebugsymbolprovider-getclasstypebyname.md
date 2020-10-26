---
title: 'IDebugSymbolProvider:: GetClassTypeByName |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetClassTypeByName
helpviewer_keywords:
- IDebugSymbolProvider::GetClassTypeByName method
ms.assetid: 2c748909-51dc-49b7-b193-19f96fca1138
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6aed4010789fd5fa9bd6f77bd41c7c1ad2076b81
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155144"
---
# <a name="idebugsymbolprovidergetclasstypebyname"></a>IDebugSymbolProvider::GetClassTypeByName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、完全修飾クラス名を表すクラスフィールド型を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetClassTypeByName(   
   LPCOLESTR          pszClassName,  
   NAME_MATCH         nameMatch,  
   IDebugClassField** ppField  
);  
```  
  
```csharp  
int GetClassTypeByName(  
   string               pszClassName,   
   NAME_MATCH           nameMatch,   
   out IDebugClassField ppField  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszClassName`  
 からクラス名。  
  
 `nameMatch`  
 から一致の種類 (大文字と小文字を区別するなど) を選択します。 [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)列挙体の値。  
  
 `ppField`  
 入出力 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) インターフェイスによって表されるクラス型を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)   
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
