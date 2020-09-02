---
title: 'IDiaLoadCallback:: NotifyOpenDBG |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyOpenDBG method
ms.assetid: dbc4dcf0-4ace-4dce-9790-0fdaf3a23d3b
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 12dd028cac885978589524aaf02f110a5a6994c4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151976"
---
# <a name="idialoadcallbacknotifyopendbg"></a>IDiaLoadCallback::NotifyOpenDBG
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Dbg ファイルが開かれたときに呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT NotifyOpenDBG (   
   LPCOLESTR dbgPath,  
   HRESULT   resultCode  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dbgPath`  
 からDbg ファイルの完全パス。  
  
 `resultCode`  
 から`S_OK`このファイルに適用された読み込みの成功 () または失敗を示すコード。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 通常、リターンコードは無視されます。  
  
## <a name="see-also"></a>参照  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
