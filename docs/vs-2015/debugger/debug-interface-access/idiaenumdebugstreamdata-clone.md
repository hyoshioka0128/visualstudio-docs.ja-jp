---
title: 'IDiaEnumDebugStreamData:: Clone |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Clone method
ms.assetid: e7f17750-0694-4634-bf34-c821cd265c2f
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0c97018adad246674c672fc1b081944f05e5913c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198580"
---
# <a name="idiaenumdebugstreamdataclone"></a>IDiaEnumDebugStreamData::Clone
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

現在の列挙子と同じ列挙シーケンスを含む列挙子を作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Clone (   
   IDiaEnumDebugStreamData** ppenum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 ppenum  
 入出力デバッグデータストリームレコードの重複するシーケンスを含む [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
