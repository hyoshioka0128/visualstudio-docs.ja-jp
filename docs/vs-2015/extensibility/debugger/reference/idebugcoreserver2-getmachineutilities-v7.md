---
title: 'IDebugCoreServer2:: GetMachineUtilities_V7 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
helpviewer_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
ms.assetid: 64c1f08f-853b-4498-9810-29791581ef2f
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 131f5a5f276b3f93d2ede3d088556b6832cc3651
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842220"
---
# <a name="idebugcoreserver2getmachineutilities_v7"></a>IDebugCoreServer2::GetMachineUtilities_V7
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、サーバーのマシンユーティリティを取得します。  
  
> [!NOTE]
> このメソッドは互換性のために残されています。使用しないでください ( [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] `E_NOTIMPL` このメソッドが呼び出された場合は、常にを返します)。 この情報は、履歴上の理由で保持されます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetMachineUtilities_V7(  
   IDebugMDMUtil2_V7** ppUtil  
);  
```  
  
```csharp  
int GetMachineUtilities_V7(  
   out IDebugMDMUtil2_V7 ppUtil  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppUtil`  
 入出力 `IDebugMDMUtil2_V7` コンピューターユーティリティ情報を表すインターフェイスを返します。  
  
## <a name="return-value"></a>戻り値  
 は常にを返し `E_NOTIMPL` ます。これは、メソッドが実装されていないことを示します。  
  
## <a name="remarks"></a>注釈  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]`E_NOTIMPL`このメソッドが呼び出された場合は、常にを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
