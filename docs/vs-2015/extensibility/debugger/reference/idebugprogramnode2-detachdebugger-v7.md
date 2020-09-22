---
title: IDebugProgramNode2::D etachDebugger_V7 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::DetachDebugger
helpviewer_keywords:
- IDebugProgramNode2::DetachDebugger
- IDebugProgramNode2::DetachDebugger_V7
ms.assetid: d2d4b78e-a2dd-4217-97a6-ab648fd2ee2f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 25c60bc42895a0527f1638dada5a28a1631314e0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841785"
---
# <a name="idebugprogramnode2detachdebugger_v7"></a>IDebugProgramNode2::DetachDebugger_V7
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

れ. 使用しないでください。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT DetachDebugger_V7 (   
   void   
);  
```  
  
```csharp  
int DetachDebugger_V7 ();  
```  
  
## <a name="return-value"></a>戻り値  
 実装は常にを返す必要があり `E_NOTIMPL` ます。  
  
## <a name="remarks"></a>注釈  
  
> [!WARNING]
> 以降 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 、このメソッドは使用されなくなり、常にを返す必要があり `E_NOTIMPL` ます。  
  
 このメソッドは、デバッガーが予期せず終了したときに呼び出されます。 このメソッドが呼び出されると、DE は、ユーザーがそのプログラムからデタッチした場合と同様にプログラムを再開します。 これ以上デバッグイベントを送信することはできません。 プログラムは、デバッガーの別のインスタンスからアタッチできる状態である必要があります。  
  
## <a name="see-also"></a>参照  
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
