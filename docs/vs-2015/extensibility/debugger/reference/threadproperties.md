---
title: THREADPROPERTIES |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- THREADPROPERTIES
helpviewer_keywords:
- THREADPROPERTIES structure
ms.assetid: 7d397207-db03-4ec0-9f79-3794056ed89f
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4815a1e42b98fba812e8a3c2a53516bff16081db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204819"
---
# <a name="threadproperties"></a>THREADPROPERTIES
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

スレッドのプロパティについて説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _tagTHREADPROPERTIES {   
   THREADPROPERTY_FIELDS dwFields;  
   DWORD                 dwThreadId;  
   DWORD                 dwSuspendCount;  
   DWORD                 dwThreadState;  
   BSTR                  bstrPriority;  
   BSTR                  bstrName;  
   BSTR                  bstrLocation;  
} THREADPROPERTIES;  
```  
  
```csharp  
public struct THREADPROPERTIES {   
   public uint   dwFields;  
   public uint   dwThreadId;  
   public uint   dwSuspendCount;  
   public uint   dwThreadState;  
   public string bstrPriority;  
   public string bstrName;  
   public string bstrLocation;  
};  
```  
  
## <a name="members"></a>メンバー  
 dwFields  
 この構造体のどのフィールドが有効であるかを示す、 [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md) 列挙型のフラグの組み合わせ。  
  
 dwThreadId  
 スレッド ID。  
  
 dwSuspendCount  
 スレッドの中断回数。  
  
 dwThreadState  
 オペレーティングスレッドの状態を示す [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md) 列挙の値です。  
  
 bstrPriority  
 スレッドの優先順位を指定する文字列。例として、"Normal"、"Normal"、"Time Critical" などがあります。  
  
 bstName  
 スレッド名。  
  
 bstrLocation  
 スレッドの場所 (通常は最上位のスタックフレーム)。通常は、実行が現在停止しているメソッドの名前として表されます。  
  
## <a name="remarks"></a>注釈  
 この構造体は、 [Getthreadproperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) メソッドの呼び出しによって格納されます。 返される情報は、通常、[ **スレッド** ] ウィンドウの設定に使用されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)   
 [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)   
 [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)
