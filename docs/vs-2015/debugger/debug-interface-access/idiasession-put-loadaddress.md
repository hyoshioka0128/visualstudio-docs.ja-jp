---
title: IDiaSession::p ut_loadAddress |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::put_loadAddress method
ms.assetid: b157b245-1ea0-4b80-8962-d8b278dbc742
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f697384874726904960fc5ba04733c3acfe1cd06
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841332"
---
# <a name="idiasessionput_loadaddress"></a>IDiaSession::put_loadAddress
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このシンボルストア内のシンボルに対応する実行可能ファイルの読み込みアドレスを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT put_loadAddress (   
   ULONGLONG NewVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `NewVal`  
 から実行可能ファイルのアドレスを読み込みます。  
  
## <a name="remarks"></a>注釈  
 シンボル仮想アドレス (VA) のプロパティは、このメソッドの値を使用して計算されます。 このプロパティがゼロ以外に設定されている場合を除き、仮想アドレスは計算されません。  
  
> [!NOTE]
> シンボルに対して仮想プロパティを使用する必要がある場合は、 [IDiaSession](../../debugger/debug-interface-access/idiasession.md) オブジェクトを取得し、オブジェクトの使用を開始する前に、このメソッドを呼び出す必要があります。  
  
## <a name="see-also"></a>参照  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
