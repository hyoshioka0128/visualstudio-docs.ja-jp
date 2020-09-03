---
title: 'IDebugProcessEx2:: AddImplicitProgramNodes |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: faca728144bde572d8a1d3424fbfcf908403d679
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202819"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、指定された各デバッグエンジン (DE) のプログラムノードを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT AddImplicitProgramNodes(  
   REFGUID guidLaunchingEngine,  
   GUID*   rgguidSpecificEngines,  
   DWORD   celtSpecificEngines  
);  
```  
  
```csharp  
int AddImplicitProgramNodes(  
   ref Guid guidLaunchingEngine,  
   Guid[]   rgguidSpecificEngines,  
   uint     celtSpecificEngines  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `guidLaunchingEngine`  
 からプログラムを起動するために使用される `GUID` (および、独自のプログラムノードを追加すると想定される) の。  
  
 `rgguidSpecificEngines`  
 から `GUID`プログラムノードが追加される DEs のの配列。  
  
 `celtSpecificEngines`  
 から配列内のの数 `GUID` `rgguidSpecificEngines` 。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 に示されている各 DE に対して[プログラムノード](../../../extensibility/debugger/program-nodes.md)が追加されます。これは、 `rgguidSpecificEngines` `guidLaunchingEngine` プログラムを起動したときに、独自のプログラムノードを追加することを前提としています (で指定されているように)。  
  
## <a name="see-also"></a>参照  
 [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)   
 [プログラム ノード](../../../extensibility/debugger/program-nodes.md)
