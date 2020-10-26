---
title: 'IDebugAlias:: Ge Ordebugvalue |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugAlias::GetICorDebugValue
helpviewer_keywords:
- IDebugAlias::GetICorDebugValue method
ms.assetid: b9eb39ee-84af-4ace-9cfe-236b3d48aff5
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 67ab8a7343cd320470515b757dfca905a0a4690e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156279"
---
# <a name="idebugaliasgeticordebugvalue"></a>IDebugAlias::GetICorDebugValue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このエイリアスに関連付けられている値を表すマネージコードインターフェイスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetICorDebugValue(  
   IUnknown** ppUnk  
);  
```  
  
```csharp  
int GetICorDebugValue(  
   out object ppUnk  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppUnk`  
 [出力] `IUnknown` この別名に関連付けられている値を表すインターフェイス。 このインターフェイスは、インターフェイスに対してクエリを実行でき `ICorDebugValue` ます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、マネージ値にのみ適用されます (は `ICorDebugValue` で使用可能なインターフェイスであり、 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] cordebug .idl ファイルの SDK で定義されてい [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ます)。  
  
## <a name="see-also"></a>参照  
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
