---
title: BP_LOCATION_DATA_STRING |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION_DATA_STRING
helpviewer_keywords:
- BP_LOCATION_DATA_STRING structure
ms.assetid: 445d6f3f-95b0-47ac-85e2-51b778240687
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 82caf285d73ab1b9b49b9546012bbb45f25c3320
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153434"
---
# <a name="bp_location_data_string"></a>BP_LOCATION_DATA_STRING
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

統合開発環境 (IDE: integrated development environment) からユーザーが入力できる文字列に基づいてデータブレークポイントを設定するために使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _BP_LOCATION_DATA_STRING {   
   IDebugThread2* pThread;  
   BSTR           bstrContext;  
   BSTR           bstrDataExpr;  
   DWORD          dwNumElements;  
} BP_LOCATION_DATA_STRING;  
```  
  
## <a name="members"></a>メンバー  
 `pThread`  
 ブレークポイントが発生したスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。  
  
 `bstrContext`  
 コード内のブレークポイントのコンテキスト。通常は、呼び出し履歴に表示されるメソッドまたは関数の名前です。  
  
 `bstrDataExpr`  
 ブレークポイントを設定するためにユーザーが入力するデータ文字列。  
  
 `dwNumElements`  
 ブレークポイントが発生するデータ文字列内の要素の数。  
  
## <a name="remarks"></a>注釈  
 この構造体は、共用体の一部として [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 構造体のメンバーになります。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
