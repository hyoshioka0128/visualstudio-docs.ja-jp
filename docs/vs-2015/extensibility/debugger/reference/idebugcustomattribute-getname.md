---
title: 'IDebugCustomAttribute:: GetName |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetName
helpviewer_keywords:
- IDebugCustomAttribute::GetName
ms.assetid: ba509cc5-5816-4925-a094-4c72d88c360c
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4463fc4f9d321b26487e885255843a7acd945f76
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62569271"
---
# <a name="idebugcustomattributegetname"></a>IDebugCustomAttribute::GetName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

カスタム属性の名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetName(   
   BSTR* bstrName  
);  
```  
  
```csharp  
int GetName(  
   out string bstrName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `bstrName`  
 入出力カスタム属性の名前を含む文字列を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドによって返されるという名前のは、属性の宣言に使用されるクラスの名前に対応します。 これは、カスタム属性クラス自体の名前に完全に対応しているとは限りません。 C# では、宣言で使用されている場合、"Attribute" サフィックスをカスタム属性名から削除することができます。  
  
## <a name="see-also"></a>参照  
 [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
