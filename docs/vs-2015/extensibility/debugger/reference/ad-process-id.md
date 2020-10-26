---
title: AD_PROCESS_ID |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- AD_PROCESS_ID
helpviewer_keywords:
- AD_PROCESS_ID union
ms.assetid: 4cb40d12-2e92-4f09-83f4-689928bd65b3
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ea06d8e007e2df88cb46c2f0e6dd4a79ebe711b7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153624"
---
# <a name="ad_process_id"></a>AD_PROCESS_ID
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プロセス ID を指定します。これは、システム ID または GUID のいずれかになります。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _AD_PROCESS_ID {  
   AD_PROCESS_ID_TYPE ProcessIdType;  
   union {  
      DWORD dwProcessId;   
      GUID  guidProcessId;   
      DWORD dwUnused;   
   } ProcessId;  
} AD_PROCESS_ID;  
```  
  
```csharp  
public struct AD_PROCESS_ID {  
   AD_PROCESS_ID_TYPE ProcessIdType;  
   DWORD              dwProcessId;   
   GUID               guidProcessId;   
   DWORD              dwUnused;   
};  
```  
  
## <a name="members"></a>メンバー  
 `ProcessIdType`  
 [AD_PROCESS_ID_TYPE](../../../extensibility/debugger/reference/ad-process-id-type.md) `ProcessId` 共用体 (または、マネージコードの場合は、アクセスする構造体のメンバー) を解釈する方法を指定する AD_PROCESS_ID_TYPE 列挙の値。  
  
 dwProcessId  
 システムからの値としてのプロセス ID。  
  
 guidProcessId  
 GUID としてのプロセス ID。  
  
 dwUnused  
 余白.  
  
## <a name="remarks"></a>注釈  
 この構造体は、次のメソッドに渡されます。  
  
- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)  
  
- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)  
  
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)  
  
- [GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)  
  
  とは、次のメソッドから返されます。  
  
- [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)  
  
- [GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)   
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)   
 [AD_PROCESS_ID_TYPE](../../../extensibility/debugger/reference/ad-process-id-type.md)   
 [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)   
 [GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)   
 [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)   
 [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)   
 [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
