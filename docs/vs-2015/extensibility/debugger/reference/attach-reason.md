---
title: ATTACH_REASON |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- ATTACH_REASON
helpviewer_keywords:
- ATTACH_REASON enumeration
ms.assetid: 159fb70b-a344-4ba6-9115-b7eaa16e228f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c66894fe0515b28037bbb2a19715fa09cbf9fa62
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153589"
---
# <a name="attach_reason"></a>ATTACH_REASON
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグエンジン (DE) がプログラムノードにアタッチされる理由を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_ATTACH_REASON {   
   ATTACH_REASON_LAUNCH = 0x0001,  
   ATTACH_REASON_USER   = 0x0002,  
   ATTACH_REASON_AUTO   = 0x0003  
};  
typedef DWORD ATTACH_REASON;  
```  
  
```csharp  
public enum enum_ATTACH_REASON {   
   ATTACH_REASON_LAUNCH = 0x0001,  
   ATTACH_REASON_USER   = 0x0002,  
   ATTACH_REASON_AUTO   = 0x0003  
};  
```  
  
## <a name="members"></a>メンバー  
 ATTACH_REASON_AUTO  
 プロセスは現在デバッグモードであるため、アタッチします。  
  
 ATTACH_REASON_LAUNCH  
 プロセスが起動されたため、アタッチします。  
  
 ATTACH_REASON_USER  
 ユーザー要求のためにアタッチします。  
  
## <a name="remarks"></a>注釈  
 これらの値は、 [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドと [attach](../../../extensibility/debugger/reference/idebugprogramex2-attach.md) メソッドのパラメーターとして使用されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [外付け](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [[アタッチ]](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)
