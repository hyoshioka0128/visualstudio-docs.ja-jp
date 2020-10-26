---
title: 'IDebugClassField:: GetDefaultIndexer |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField::GetDefaultIndexer
helpviewer_keywords:
- IDebugClassField::GetDefaultIndexer method
ms.assetid: 47ce4f45-3816-4b40-909c-5032d0692d75
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6be0a1925a1e5d48941c1c0e13ac1b4789687229
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191023"
---
# <a name="idebugclassfieldgetdefaultindexer"></a>IDebugClassField::GetDefaultIndexer
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

既定のインデクサーの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetDefaultIndexer(   
   BSTR* pbstrIndexer  
);  
```  
  
```csharp  
int GetDefaultIndexer(  
   out string pbstrIndexer  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pbstrIndexer`  
 入出力既定のインデクサーの名前を含む文字列を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。既定のインデクサーがない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 クラスの既定のインデクサーは、 `Default` 配列アクセスのプロパティとしてマークされているプロパティです。 これは、に固有のものです [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 。 で宣言された既定のインデクサーの例 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] と、その使用方法を次に示します。  
  
```vb  
Imports System.Collections;  
  
Public Class Class1  
    Private myList as Hashtable  
  
    Default Public Property Item(ByVal Index As Integer) As Integer  
        Get  
            Return CType(List(Index), Integer)  
        End Get  
        Set(ByVal Value As Integer)  
            List(Index) = Value  
        End Set  
    End Property  
End Class  
  
Function GetItem(Index as Integer) as Integer  
    Dim classList as Class1 = new Class1  
    Dim value as Integer  
  
    ' Access array through default indexer  
    value = classList(2)  
  
    ' Access array through explicit property  
    value = classList.Item(2)  
  
    Return value  
End Function  
```  
  
## <a name="see-also"></a>参照  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
