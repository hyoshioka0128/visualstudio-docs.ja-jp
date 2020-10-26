---
title: 'IDebugActivateDocumentEvent2:: GetDocument |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugActivateDocumentEvent2::GetDocument
helpviewer_keywords:
- GetDocument method
- IDebugActivateDocumentEvent2::GetDocument method
ms.assetid: b3c32f1b-f3de-409d-920d-ba7b3fa84fcd
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2b159fe71c75acbeb6a0220af76ab13cf7b40e20
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186732"
---
# <a name="idebugactivatedocumentevent2getdocument"></a>IDebugActivateDocumentEvent2::GetDocument
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

アクティブにするドキュメントを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetDocument (   
   IDebugDocument2** ppDoc  
);  
```  
  
```csharp  
int GetDocument (   
   out IDebugDocument2 ppDoc  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppDoc`  
 入出力アクティブにするドキュメントを表す [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)   
 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
