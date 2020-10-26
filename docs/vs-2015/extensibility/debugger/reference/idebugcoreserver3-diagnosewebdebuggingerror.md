---
title: IDebugCoreServer3::D iagnoseWebDebuggingError |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
helpviewer_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
ms.assetid: 8c4570ca-ae55-42f2-bbaa-8d8e75d2fa19
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 24f142a631df25cfbff8ed795736c0cbf4e59eaf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205278"
---
# <a name="idebugcoreserver3diagnosewebdebuggingerror"></a>IDebugCoreServer3::DiagnoseWebDebuggingError
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

自動アタッチに失敗した原因の特定を試みます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT DiagnoseWebDebuggingError(  
   LPCWSTR pszUrl  
);  
```  
  
```csharp  
int DiagnoseWebDebuggingError(  
   string pszUrl  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszUrl`  
 から現在使用されていません。常に null 値に設定する必要があります。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 その他の一般的なリターンコードを次に示します。  
  
|コード|説明|  
|----------|-----------------|  
|`S_WEBDBG_UNABLE_TO_DIAGNOSE`|リモートサーバーがデバッグを開始できなかった理由を特定できません。|  
|`S_WEBDBG_DEBUG_VERB_BLOCKED`|リモートサーバーでデバッグできません。アクセス許可が不十分であるか、デバッグ動詞が有効になっていないことが原因である可能性があります。|  
|`E_WEBDBG_DEBUG_VERB_BLOCKED`|Web サーバーがロックダウンされ、デバッグを有効にするために必要な DEBUG 動詞をブロックしています。|  
  
## <a name="see-also"></a>参照  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
