---
title: 'IDiaLoadCallback:: NotifyDebugDir |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyDebugDir method
ms.assetid: bd04e2f6-0dbf-4742-a556-96f2cd99aa19
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2e8fe8ffe9d7d495e40c8c84b08aeaefb03e8d17
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152008"
---
# <a name="idialoadcallbacknotifydebugdir"></a>IDiaLoadCallback::NotifyDebugDir
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグディレクトリが .exe ファイルで見つかったときに呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT NotifyDebugDir (   
   BOOL  fExecutable,  
   DWORD cbData,  
   BYTE  data[]  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `fExecutable`  
 [入力] `TRUE` デバッグディレクトリが、拡張子が dbg ではなく、実行可能ファイルから読み取られる場合はです。  
  
 `cbData`  
 からデバッグディレクトリ内のデータのバイト数。  
  
 `data[]`  
 からデバッグディレクトリを使用して入力された配列。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 通常、リターンコードは無視されます。  
  
## <a name="remarks"></a>注釈  
 [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)メソッドは、実行可能ファイルの処理中にデバッグディレクトリを検出すると、このコールバックを呼び出します。  
  
 このメソッドを使用すると、.pdb ファイルに存在しないデバッグ情報をサポートするために、クライアントが実行可能ファイルやデバッグファイルをリバースエンジニアリングする必要がなくなります。 このデータを使用すると、クライアントは使用可能なデバッグ情報の種類と、実行可能ファイルまたは dbg ファイルのどちらに存在するかを認識できます。  
  
 メソッドは、 `IDiaDataSource::loadDataForExe` シンボルの提供に必要なときに .pdb ファイルと dbg ファイルの両方を透過的に開くため、ほとんどのクライアントはこのコールバックを必要としません。  
  
## <a name="see-also"></a>参照  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)   
 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
