---
title: IDebugClassField::D oesInterfaceExist |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField::DoesInterfaceExist
helpviewer_keywords:
- IDebugClassField::DoesInterfaceExist method
ms.assetid: cc0c8642-1a76-4fda-a309-7018a34883c9
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9f71346c1b69729ae54ef0d33be4149e7000316c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191132"
---
# <a name="idebugclassfielddoesinterfaceexist"></a>IDebugClassField::DoesInterfaceExist
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

クラスで特定のインターフェイスが定義されているかどうかを判断します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT DoesInterfaceExist(   
   LPCOLESTR pszInterfaceName  
);  
```  
  
```csharp  
int DoesInterfaceExist(  
   [In] string pszInterfaceName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszInterfaceName`  
 から検索するインターフェイス名を格納している文字列。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返し、インターフェイスが存在しない場合は S_FALSE を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、すべてのインターフェイスの列挙体を取得し、一致するインターフェイスのリストを検索します。  
  
## <a name="see-also"></a>参照  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
