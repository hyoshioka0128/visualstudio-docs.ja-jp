---
title: 'IDebugArrayField:: Ge/k |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetRank
helpviewer_keywords:
- IDebugArrayField::GetRank method
ms.assetid: 2364b876-5be1-4bab-9b8f-3b6121da35c6
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5d0396718482c9ce90527155a3612160612f66d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198732"
---
# <a name="idebugarrayfieldgetrank"></a>IDebugArrayField::GetRank
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

配列の次元のランクまたは数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetRank(   
   DWORD* pdwRank  
);  
```  
  
```csharp  
int GetRank(  
   out uint pdwRank  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwRank`  
 入出力ランクを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 配列のランクは、次元の数に対応します。 C++ および C# では、多次元配列は配列の配列であるため、1次元配列と見なされることがあり `GetRank` ます (メソッドは常に1を返します)。 一方、では、 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 多次元配列は異なる方法で処理され、そのような配列のランクは次元の数を反映し `GetRank` ます (メソッドは常に次元数を返します)。  
  
## <a name="see-also"></a>参照  
 [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
