---
title: IDebugProgramPublisher2::P ublishProgramNode |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgramNode
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgramNode
ms.assetid: d4b72e04-f726-46cf-8e56-5203ff205b12
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: eac08c35afe407358b7e2d37216dda202c490bd3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146312"
---
# <a name="idebugprogrampublisher2publishprogramnode"></a>IDebugProgramPublisher2::PublishProgramNode
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プログラムノードをデバッグエンジン (DEs) およびセッションデバッグマネージャー (SDM) で使用できるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT PublishProgramNode(  
   IDebugProgramNode2 *pProgramNode  
);  
```  
  
```csharp  
int PublishProgramNode(  
   IDebugProgramNode2 pProgramNode  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pProgramNode`  
 から使用できるようにするプログラムノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 この方法では、デバッグのためにプログラムを選択して起動する前に、プログラムに対してクエリを実行できます。  
  
 プログラムノードを可用性から削除するには、 [Unpublishprogramnode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md) メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)
