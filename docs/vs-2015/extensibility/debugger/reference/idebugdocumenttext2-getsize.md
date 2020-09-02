---
title: 'IDebugDocumentText2:: GetSize |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentText2::GetSize
helpviewer_keywords:
- IDebugDocumentText2::GetSize
ms.assetid: bf515a8f-dcee-4004-8f81-543d547ceaae
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1f6d438db999e2e0b2aa85c45c0b38333238755e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200211"
---
# <a name="idebugdocumenttext2getsize"></a>IDebugDocumentText2::GetSize
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ドキュメント内のこの位置にあるテキストのサイズを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetSize(   
   ULONG* pcNumLines,  
   ULONG* pcNumChars  
);  
```  
  
```csharp  
int GetSize(   
   ref uint pcNumLines,  
   ref uint pcNumChars  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pcNumLines`  
 入出力テキストの行数を返します。  
  
 `pcNumChars`  
 入出力テキストの文字数を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 [C++ のみ]特定の値が必要ない場合は、パラメーターに NULL を渡します。  
  
 [C# のみ]両方のパラメーターを指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
