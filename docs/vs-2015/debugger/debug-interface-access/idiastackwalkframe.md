---
title: IDiaStackWalkFrame |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame interface
ms.assetid: 42d82845-d6f6-4846-9ecd-9dd169216077
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 27aab0ca87e589661798028ff38fb019dae815ed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150139"
---
# <a name="idiastackwalkframe"></a>IDiaStackWalkFrame
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[IDiaFrameData:: execute](../../debugger/debug-interface-access/idiaframedata-execute.md)メソッドの呼び出し間でスタックコンテキストを保持します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDiaStackWalkFrame : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDiaStackWalkFrame` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDiaStackWalkFrame::get_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-get-registervalue.md)|レジスタの値を取得します。|  
|[IDiaStackWalkFrame::put_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-put-registervalue.md)|レジスタの値を設定します。|  
|[IDiaStackWalkFrame::readMemory](../../debugger/debug-interface-access/idiastackwalkframe-readmemory.md)|イメージからメモリを読み取ります。|  
|[IDiaStackWalkFrame::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddress.md)|指定したスタックフレーム内で、最も近い関数の戻り先アドレスを検索します。|  
|[IDiaStackWalkFrame::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddressstart.md)|指定したスタックフレーム内で、指定したアドレスまたはその近くの戻りアドレスを検索します。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスは、プログラムの実行中に、レジスタの読み取りと書き込みと、メモリへのアクセス、およびリターンアドレスの検索のために使用されます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 クライアントアプリケーションは、このインターフェイスを実装し、インターフェイスのインスタンスを [IDiaFrameData:: execute](../../debugger/debug-interface-access/idiaframedata-execute.md) メソッドに渡します。 このインターフェイスの同じインスタンスを再度使用して、メソッドの呼び出し時にレジスタの状態を維持し `execute` ます。 また、メソッドは、 `execute` このインターフェイスを使用して、戻り先アドレスを決定します。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>参照  
 [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md)
