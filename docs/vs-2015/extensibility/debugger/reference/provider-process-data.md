---
title: PROVIDER_PROCESS_DATA |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- PROVIDER_PROCESS_DATA
helpviewer_keywords:
- PROVIDER_PROCESS_DATA structure
ms.assetid: ec2362ed-4a0c-4a09-9d66-8ff04e4f41ee
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 89192d814ccee3dd2a134807d8ce01880689d951
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204937"
---
# <a name="provider_process_data"></a>PROVIDER_PROCESS_DATA
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

この構造体は、コンピューター上で実行されているプロセスに関する情報を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct tagPROVIDER_PROCESS_DATA {  
   PROVIDER_FIELDS    Fields;  
   PROGRAM_NODE_ARRAY ProgramNodes;  
   BOOL               fIsDebuggerPresent;  
} PROVIDER_PROCESS_DATA;  
```  
  
```csharp  
public struct PROVIDER_PROCESS_DATA {  
   public uint               Fields;  
   public PROGRAM_NODE_ARRAY ProgramNodes;  
   public int                fIsDebuggerPresent;  
}  
```  
  
## <a name="members"></a>メンバー  
 フィールド  
 [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)列挙のフラグの組み合わせ。入力されているフィールドを示します。  
  
 ProgramNodes  
 プログラムノードの配列を格納する [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md) 構造体。  
  
 Fisデバッガが存在します  
 `TRUE`デバッガーが実行されている場合は0以外 () [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 、そうでない場合は 0 () `FALSE` です。  
  
## <a name="remarks"></a>注釈  
 この構造体は、 [Getproviderprocessdata](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) メソッドに渡されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)   
 [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)   
 [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
