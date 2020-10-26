---
title: 'IDiaStackWalkFrame:: searchForReturnAddress |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::searchForReturnAddress method
ms.assetid: 1a54c50d-94af-4a43-ac4e-d80c5df156c3
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bf23ad6c0edd2a662650e57c3582ec0e1dc1a5d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150156"
---
# <a name="idiastackwalkframesearchforreturnaddress"></a>IDiaStackWalkFrame::searchForReturnAddress
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定したスタックフレーム内で、最も近い関数の戻り先アドレスを検索します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT searchForReturnAddress (   
   IDiaFrameData* frame,  
   ULONGLONG*     returnAddress  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `frame`  
 から現在のスタックフレームを表す [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) オブジェクト。  
  
 `returnAddress`  
 入出力最も近い関数の戻り先アドレスを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)   
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
