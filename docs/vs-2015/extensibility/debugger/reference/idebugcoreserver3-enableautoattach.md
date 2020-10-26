---
title: 'IDebugCoreServer3:: EnableAutoAttach |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::EnableAutoAttach
helpviewer_keywords:
- IDebugCoreServer3::EnableAutoAttach
ms.assetid: 06aa633b-263b-4e08-8844-9a52d5120b94
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 45362c9456b99d6cec0af01dcb29844d02363a27
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62569795"
---
# <a name="idebugcoreserver3enableautoattach"></a>IDebugCoreServer3::EnableAutoAttach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定されたデバッグエンジンへの自動アタッチを有効にします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT EnableAutoAttach(  
   GUID*     rgguidSpecificEngines,  
   DWORD     celtSpecificEngines,  
   LPCOLESTR pszStartPageUrl,  
   BSTR*     pbstrSessionId  
);  
```  
  
```csharp  
int EnableAutoAttach(  
   Guid[]     rgguidSpecificEngines,  
   uint       celtSpecificEngines,  
   string     pszStartPageUrl,  
   out string pbstrSessionId  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `rgguidSpecificEngines`  
 から自動アタッチとしてマークする各デバッグエンジンの Guid の配列。  
  
 `celtSpecificEngines`  
 からで指定されたエンジンの数 `rgguidSpecificEngines` 。  
  
 `pszStartPageUrl`  
 から自動アタッチ時に使用する開始 URL。  
  
 `pbstrSessionID`  
 入出力自動接続されたセッションの ID。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 1つのエラーコードはです `E_AUTO_ATTACH_NOT_REGISTERED` 。これは、自動アタッチクラスファクトリが登録されていないことを示します。  
  
## <a name="remarks"></a>注釈  
 指定した URL に関連付けられているプログラムが開始されると、指定されたデバッグエンジンが自動的に起動され、アタッチされます。  
  
## <a name="see-also"></a>参照  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
