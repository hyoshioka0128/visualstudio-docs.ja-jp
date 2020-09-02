---
title: AD_PROCESS_ID_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- AD_PROCESS_ID_TYPE
helpviewer_keywords:
- AD_PROCESS_ID_TYPE enumeration
ms.assetid: 0aab80e9-285a-4697-94ac-c864d42a6aaa
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d471a73205383f0f23c5016872712a3ba2c578d6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153621"
---
# <a name="ad_process_id_type"></a>AD_PROCESS_ID_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)構造体でプロセス ID を解釈する方法を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_AD_PROCESS_ID {  
   AD_PROCESS_ID_SYSTEM = 0,  
   AD_PROCESS_ID_GUID   = 1  
};  
typedef DWORD AD_PROCESS_ID_TYPE;  
```  
  
```csharp  
public enum enum_AD_PROCESS_ID {  
   AD_PROCESS_ID_SYSTEM = 0,  
   AD_PROCESS_ID_GUID   = 1  
};  
```  
  
## <a name="members"></a>メンバー  
 AD_PROCESS_ID_SYSTEM  
 プロセス ID はシステム識別子です。 `ProcessId.dwProcessId` [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)構造体のフィールドを使用します。  
  
 AD_PROCESS_ID_GUID  
 プロセス ID は GUID です。 `ProcessId.guidProcessId`構造体のフィールドを使用し `AD_PROCESS_ID` ます。  
  
## <a name="remarks"></a>注釈  
 `ProcessIdType`構造体に含まれているプロセス ID の種類を識別するために、 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)構造体のメンバーに使用されます。 構造体の共用体を解釈する方法を決定し `ProcessId` ます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
