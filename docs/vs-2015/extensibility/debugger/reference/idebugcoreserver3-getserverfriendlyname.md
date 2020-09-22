---
title: 'IDebugCoreServer3:: GetServerFriendlyName |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::GetServerFriendlyName
helpviewer_keywords:
- IDebugCoreServer3::GetServerFriendlyName
ms.assetid: 7035b904-b3d7-4d9b-98d9-65714b8a8b9f
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fa81daf7ab1d592e6a2cd460268e5d66925f61e1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841505"
---
# <a name="idebugcoreserver3getserverfriendlyname"></a>IDebugCoreServer3::GetServerFriendlyName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

サーバーのフレンドリ名を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetServerFriendlyName(  
   BSTR* pbstrName  
);  
```  
  
```csharp  
int GetServerFriendlyName(  
   out string pbstrName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pbstrName`  
 入出力サーバーのフレンドリ名を返します。  
  
> [!NOTE]
> 呼び出し元は、文字列を解放する必要があります。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 ユーザーが起動したサーバーの場合、このメソッドによって返される名前はサーバーの完全な名前になります。 自動起動サーバーの場合は、サーバーが実行されているコンピューターの名前です。  
  
 コンピューター指向の名前の場合は、 [Getservername](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md) メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)   
 [GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)
