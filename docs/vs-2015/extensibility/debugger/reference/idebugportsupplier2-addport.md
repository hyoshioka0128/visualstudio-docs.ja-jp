---
title: 'IDebugPortSupplier2:: AddPort |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::AddPort
helpviewer_keywords:
- IDebugPortSupplier2::AddPort
ms.assetid: df491161-6bf3-4fcc-b478-b9ec88ec995f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bf5bf281e794bde04ae0c2e86c6d27edb7edc5a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188306"
---
# <a name="idebugportsupplier2addport"></a>IDebugPortSupplier2::AddPort
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ポートを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT AddPort(   
   IDebugPortRequest2* pRequest,  
   IDebugPort2**       ppPort  
);  
```  
  
```csharp  
int AddPort(   
   IDebugPortRequest2 pRequest,  
   out IDebugPort2    ppPort  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRequest`  
 から追加するポートを記述する [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) オブジェクト。  
  
 `ppPort`  
 入出力ポートを表す [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、要求されたポートを実際に作成するだけでなく、ポート供給元のアクティブなポートの内部リストに追加します。 [Canaddport](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)メソッドは、時間がかかる可能性のある遅延を回避するために最初に呼び出すことができます。  
  
## <a name="see-also"></a>参照  
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)   
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)   
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)
