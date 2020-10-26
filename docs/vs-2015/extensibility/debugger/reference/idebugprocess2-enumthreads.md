---
title: 'IDebugProcess2:: EnumThreads |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumThreads
helpviewer_keywords:
- IDebugProcess2::EnumThreads
ms.assetid: 05677385-7a7f-4545-8438-af00dde85db0
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3e9b6447827baa80da2843c992a8d2233dd1a4b6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188022"
---
# <a name="idebugprocess2enumthreads"></a>IDebugProcess2::EnumThreads
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プロセスで実行されているすべてのスレッドの一覧を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT EnumThreads(  
   IEnumDebugThreads2** ppEnum  
);  
```  
  
```csharp  
int EnumThreads(  
   out IEnumDebugThreads2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力プロセス内のすべてのプログラム内のすべてのスレッドの一覧を含む [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、各プログラムで実行されているスレッドを列挙し、それらをスレッドのプロセスビューに結合します。 1つのスレッドが複数のプログラムで実行される場合があります。このメソッドは、そのスレッドを1回だけ列挙します。  
  
 このメソッドは、重複しないプロセスのスレッドの一覧を表示します。 それ以外の場合、特定のプログラムで実行されているスレッドを列挙するには、 [Enumthreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) メソッドを使用します。  
  
## <a name="see-also"></a>参照  
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)   
 [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
