---
title: 'IDebugProcessSecurity:: Querycansaf Elyattach |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::QueryCanSafelyAttach
ms.assetid: 63ec1ae8-27da-4574-aa15-1c986fe9fe58
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ec541b6dc4ccae57628d4b33e7c188008da6edae
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187955"
---
# <a name="idebugprocesssecurityquerycansafelyattach"></a>IDebugProcessSecurity::QueryCanSafelyAttach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドを使用すると、ユーザーが安全でないプロセスにアタッチする前に、ポート供給者が警告を表示できます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT QueryCanSafelyAttach();  
```  
  
```csharp  
int QueryCanSafelyAttach();  
```  
  
## <a name="return-value"></a>戻り値  
 戻り値は次のとおりです。  
  
- `S_OK`: プロセスへのアタッチは安全であり、警告ダイアログボックスは表示されません。  
  
- `S_FALSE`: アタッチがセキュリティ上の問題であり、警告が表示されたダイアログボックスが表示される場合があります。  
  
- `FAILURE`: プロセスにアタッチできません。  
  
## <a name="see-also"></a>参照  
 [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
