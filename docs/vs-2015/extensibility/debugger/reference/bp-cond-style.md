---
title: BP_COND_STYLE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_COND_STYLE
helpviewer_keywords:
- BP_COND_STYLE enumeration
ms.assetid: a93b1412-f447-48a1-af9d-38f3dbb3092f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fbb2674381992bd86f0144af103615f0a3922fcf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153570"
---
# <a name="bp_cond_style"></a>BP_COND_STYLE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

保留中のブレークポイントとバインドされたブレークポイントのブレークポイントの条件スタイルを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_BP_COND_STYLE {   
   BP_COND_NONE         = 0x0000,  
   BP_COND_WHEN_TRUE    = 0x0001,  
   BP_COND_WHEN_CHANGED = 0x0002  
};  
typedef DWORD BP_COND_STYLE;  
```  
  
```csharp  
public enum enum_BP_COND_STYLE {   
   BP_COND_NONE         = 0x0000,  
   BP_COND_WHEN_TRUE    = 0x0001,  
   BP_COND_WHEN_CHANGED = 0x0002  
};  
```  
  
## <a name="members"></a>メンバー  
 BP_COND_NONE  
 ブレークポイントの位置に達したときにブレークポイントを発生させます。 ブレークポイント条件が指定されていません。  
  
 BP_COND_WHEN_TRUE  
 ブレークポイントに関連付けられている条件式がと評価された場合にのみ、ブレークポイントを発生させ `true` ます。  
  
 BP_COND_WHEN_CHANGED  
 ブレークポイントに関連付けられている条件式の値が以前の評価から変更された場合にのみ、ブレークポイントを発生させます。  
  
## <a name="remarks"></a>注釈  
 `styleCondition` [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)構造体のメンバーに使用されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
