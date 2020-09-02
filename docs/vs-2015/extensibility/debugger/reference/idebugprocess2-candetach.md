---
title: 'IDebugProcess2:: CanDetach |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess2::CanDetach
helpviewer_keywords:
- IDebugProcess2::CanDetach
ms.assetid: 2830f7c3-69fb-474a-97b8-5b869e38d546
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bd96442ad3639aa03fa894facbbc9e6dbe3bbd21
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188089"
---
# <a name="idebugprocess2candetach"></a>IDebugProcess2::CanDetach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

セッションデバッグマネージャー (SDM) がプロセスをデタッチできるかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT CanDetach(  
   void  
);  
```  
  
```csharp  
int CanDetach();  
```  
  
## <a name="return-value"></a>戻り値  
 成功した場合 `S_OK.` 、 `S_FALSE` デバッガーがプロセスからデタッチできない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
