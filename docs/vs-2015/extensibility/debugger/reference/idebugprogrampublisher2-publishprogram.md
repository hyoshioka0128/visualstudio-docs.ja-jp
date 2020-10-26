---
title: IDebugProgramPublisher2::P ublishProgram |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgram
ms.assetid: 92ff63f0-e869-4040-b3ae-b2c899e708ff
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 21bc6e558eff662874ac35eb8557f01838914ca9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62547339"
---
# <a name="idebugprogrampublisher2publishprogram"></a>IDebugProgramPublisher2::PublishProgram
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドにより、プログラムがデバッグエンジン (DEs) とセッションデバッグマネージャーで使用できるようになります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT PublishProgram(  
   CONST_GUID_ARRAY Engines,  
   LPCOLESTR        szFriendlyName,  
   IUnknown*        pDebuggeeInterface  
);  
```  
  
```csharp  
int PublishProgram(  
   CONST_GUID_ARRAY Engines,  
   string           szFriendlyName,  
   object           pDebuggeeInterface  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `Engines`  
 からこのプログラムに対して起動またはアタッチできる DEs の Guid の配列。  
  
 `szFriendlyName`  
 からプログラムのフレンドリ名です (これは、ユーザーに表示されるメニューまたはダイアログで表示されます)。  
  
 `pDebuggeeInterface`  
 [入力] `IUnknown` プログラムのインターフェイス (この値はプログラムを一意に識別するためにクッキーとして使用されます。この同じ値を使用してプログラムを "発行解除" します)  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 プログラムをデバッグに使用できないようにするには、 [Unpublishprogram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)を呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)   
 [UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)
