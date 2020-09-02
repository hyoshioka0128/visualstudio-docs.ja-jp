---
title: PROGRAM_DESTROY_FLAGS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- PROGRAM_DESTROY_FLAGS enumeration
ms.assetid: be00d4a3-d5b8-4159-b632-64577f534883
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 16933eb409f55be209d54c26d0c077ed96f53cb1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205009"
---
# <a name="program_destroy_flags"></a>PROGRAM_DESTROY_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プログラム破棄フラグの有効な値を列挙します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
enum enum_PPROGRAM_DESTROY_FLAGS  
{  
   PROGRAM_DESTROY_CONTINUE_DEBUGGING = 0x1  
};  
typedef DWORD PROGRAM_DESTROY_FLAGS;  
```  
  
```csharp  
public enum enum_PPROGRAM_DESTROY_FLAGS  
{  
   PROGRAM_DESTROY_CONTINUE_DEBUGGING = 0x1  
};  
```  
  
## <a name="terms"></a>用語  
 PROGRAM_DESTROY_CONTINUE_DEBUGGING  
 プログラムを破棄しますが、デバッグを続行します。  
  
## <a name="remarks"></a>注釈  
 列挙体は、 [Getflags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md) メソッドによって返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)
