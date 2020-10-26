---
title: 'IDebugProgramPublisher2:: UnpublishProgram |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::UnpublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::UnpublishProgram
ms.assetid: 627e7d38-b2ac-4873-9a40-37ff7f47cd1d
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 05efc566cec0e7e885b16a4bb7c7e7d6256ac7b8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146280"
---
# <a name="idebugprogrampublisher2unpublishprogram"></a>IDebugProgramPublisher2::UnpublishProgram
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プログラムをデバッグできないようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT UnpublishProgram(  
   IUnknown* pDebuggeeInterface  
);  
```  
  
```csharp  
int UnpublishProgram(  
   object pDebuggeeInterface  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pDebuggeeInterface`  
 から `IUnknown` プログラムへのインターフェイス。 これは、 [publishprogram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md) メソッドに指定された値と同じであり、削除されるプログラムを一意に識別します (つまり、cookie として使用されます)。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 プログラムをデバッグエンジンとセッションデバッグマネージャーで使用できるようにするには、 [publishprogram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md) メソッドを使用します。  
  
## <a name="see-also"></a>参照  
 [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)   
 [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)
