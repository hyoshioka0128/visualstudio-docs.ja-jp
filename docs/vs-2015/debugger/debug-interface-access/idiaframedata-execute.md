---
title: 'IDiaFrameData:: execute |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::execute method
ms.assetid: 7a6c7d03-1ff1-4059-bd54-5f407eeebc26
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4042cf58ee34b5f49df601b94e1110f03e0b6f5b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197560"
---
# <a name="idiaframedataexecute"></a>IDiaFrameData::execute
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

スタックアンワインドを実行し、結果をスタックウォークフレームインターフェイスに返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT execute (   
   IDiaStackWalkFrame* frame  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `frame`  
 からフレームレジスタの状態を保持する [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md) オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 次の表に、このメソッドで使用できる戻り値を示します。  
  
|値|説明|  
|-----------|-----------------|  
|E_DIA_INPROLOG|プロローグコードでスタックフレームを実行することはできません。|  
|E_DIA_SYNTAX|フレームプログラムで解析エラーが発生しました。|  
|E_DIA_FRAME_ACCESS|レジスタまたはメモリにアクセスできません。|  
|E_DIA_VALUE|値の計算中にエラーが発生した (たとえば、0による除算)。|  
  
## <a name="remarks"></a>注釈  
 このメソッドは、デバッグ中にスタックをアンワインドするために呼び出されます。 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)オブジェクトは、クライアントアプリケーションによって実装され、レジスタの更新を受け取り、メソッドによって使用されるメソッドを提供し `execute` ます。  
  
## <a name="see-also"></a>参照  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
