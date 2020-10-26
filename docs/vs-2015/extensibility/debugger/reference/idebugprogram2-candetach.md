---
title: 'IDebugProgram2:: CanDetach |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::CanDetach
helpviewer_keywords:
- IDebugProgram2::CanDetach
ms.assetid: dcd9ab6c-49e5-447e-aa7c-89f571f4a052
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0a7f8bbabbba54cc7705aedc6e7f12ca1bffc924
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187934"
---
# <a name="idebugprogram2candetach"></a>IDebugProgram2::CanDetach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグエンジン (DE) をプログラムからデタッチできるかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT CanDetach(  
   void  
);  
```  
  
```csharp  
int CanDetach();  
```  
  
## <a name="return-value"></a>戻り値  
 がデタッチできる場合はを返します。 `S_OK` それ以外の場合はエラーコードを返します。 `S_FALSE`DE がプログラムからデタッチできない場合は、を返します。  
  
## <a name="see-also"></a>参照  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
