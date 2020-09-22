---
title: 'IDebugProcess3:: Getenc State |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess3::GetENCAvailableState
helpviewer_keywords:
- IDebugProcess3::GetENCAvailableState
ms.assetid: 98a5d527-8a72-476c-8e92-0bff3d97c195
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5cf5941ff75360c64add85e72a4c02c3ad716309
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841713"
---
# <a name="idebugprocess3getencavailablestate"></a>IDebugProcess3::GetENCAvailableState
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、プロセスの現在のエディットコンティニュの状態を取得します。 カスタムポート供給業者は常にを返す必要があり `E_NOTIMPL` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetENCAvailableState(  
   EncUnavailableReason* pReason  
);  
```  
  
```csharp  
int GetENCAvailableState(  
   EncUnavailableReason[] pReason  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pReason`  
 入出力 [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md) 列挙の値です。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
> [!NOTE]
> カスタムポート供給業者は常にを返す必要があり `E_NOTIMPL` ます。  
  
## <a name="remarks"></a>注釈  
 この状態は、 [Disableenc](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)によって影響を受ける可能性があります。  
  
## <a name="see-also"></a>参照  
 [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)   
 [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)   
 [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)
