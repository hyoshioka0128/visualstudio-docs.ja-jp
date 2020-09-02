---
title: 'IDebugPortSupplier3:: CanPersistPorts |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::CanPersistPorts
helpviewer_keywords:
- IDebugPortSupplier3::CanPersistPorts
ms.assetid: 4127760c-e602-4e86-9232-457e382a52c7
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: edc989771b41cc4a5cc5b4710de4cbb5632873e2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188187"
---
# <a name="idebugportsupplier3canpersistports"></a>IDebugPortSupplier3::CanPersistPorts
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、ポート供給元がデバッガーの呼び出し間でポートを (ディスクに書き込むことによって) 永続化できるかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CanPersistPorts();  
```  
  
```csharp  
int CanPersistPorts();  
```  
  
#### <a name="parameters"></a>パラメーター  
 [なし] :  
  
## <a name="return-value"></a>戻り値  
 `S_OK` ポートを永続化できる場合は `S_FALSE` 。ポートを永続化できない場合は。  
  
## <a name="remarks"></a>注釈  
 ポートの供給元がポートを永続化できる場合は、破棄されたときに、再度インスタンス化されたときに再読み込みする必要があります。  
  
## <a name="see-also"></a>参照  
 [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
