---
title: PROCESS_INFO_FLAGS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FLAGS
helpviewer_keywords:
- PROCESS_INFO_FLAGS enumeration
ms.assetid: 696951ce-701a-40c2-ac8c-b897f3aae6e2
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 88ff2a1da1f937fd4011932979bd95057eb40dfd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205050"
---
# <a name="process_info_flags"></a>PROCESS_INFO_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プロセスのプロパティを記述または指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_PROCESS_INFO_FLAGS {   
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,  
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,  
   PIFLAG_PROCESS_STOPPED   = 0x00000004,  
   PIFLAG_PROCESS_RUNNING   = 0x00000008,  
};  
typedef DWORD PROCESS_INFO_FLAGS;  
```  
  
```csharp  
enum enum_PROCESS_INFO_FLAGS {   
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,  
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,  
   PIFLAG_PROCESS_STOPPED   = 0x00000004,  
   PIFLAG_PROCESS_RUNNING   = 0x00000008,  
};  
```  
  
## <a name="members"></a>メンバー  
 PIFLAG_SYSTEM_PROCESS  
 プロセスがシステムプロセスであることを示します。  
  
 PIFLAG_DEBUGGER_ATTACHED  
 プロセスがデバッガーによってデバッグされていることを示します。 デバッガーの場合もあれば、 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 他のデバッガー (WinDbg など) の場合もあります。  
  
 PIFLAG_PROCESS_STOPPED  
 プロセスが停止されたことを示します。 が指定されている場合にのみ有効です `PIFLAG_DEBUGGER_ATTACHED` 。 以降で使用でき [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] ます。  
  
 PIFLAG_PROCESS_RUNNING  
 プロセスが実行中であることを示します。 が指定されている場合にのみ有効です `PIFLAG_DEBUGGER_ATTACHED` 。 以降で使用でき [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] ます。  
  
## <a name="remarks"></a>注釈  
 `Flags` [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)構造体のメンバーに使用されます。  
  
 これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
