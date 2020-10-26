---
title: 'IDebugField:: GetSize |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugField::GetSize
helpviewer_keywords:
- IDebugField::GetSize method
ms.assetid: 73329924-3751-4f44-af54-5986b7943374
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9fded9abc006ff6a28e122f0a4b8d7fae5da997b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148934"
---
# <a name="idebugfieldgetsize"></a>IDebugField::GetSize
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、フィールドのサイズ (バイト単位) を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetSize(   
   DWORD* pdwSize  
);  
```  
  
```csharp  
int GetSize(  
   out uint pdwSize  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwSize`  
 入出力サイズを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 すべてのフィールドには型があり、すべての型にサイズが設定されています。 たとえば、byte 型のフィールドのサイズは1バイトです。  
  
## <a name="see-also"></a>参照  
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
