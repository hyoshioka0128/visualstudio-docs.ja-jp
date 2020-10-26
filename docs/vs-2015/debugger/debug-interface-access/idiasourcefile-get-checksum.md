---
title: 'IDiaSourceFile:: get_checksum |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksum method
ms.assetid: aad63a7e-4e22-44e4-8a5b-81b5174ced1e
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0f87f5cdd937c0e172e7b96cf0858423b14686d8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190737"
---
# <a name="idiasourcefileget_checksum"></a>IDiaSourceFile::get_checksum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

チェックサムのバイト数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_checksum (   
   DWORD  cbData,  
   DWORD* pcbData,  
   BYTE   data[]  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cbData`  
 からデータバッファーのサイズ (バイト単位)。  
  
 `pcbData`  
 入出力チェックサムのバイト数を返します。 このパラメーターを `NULL` とすることはできません。  
  
 `data`  
 [入力、出力]チェックサムのバイトを格納するバッファー。 このパラメーターがの場合 `NULL` 、は `pcbData` 必要なバイト数を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 チェックサムバイトの生成に使用されたチェックサムアルゴリズムの種類を特定するには、 [IDiaSourceFile:: get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md) メソッドを呼び出します。  
  
 チェックサムは通常、ソースファイルのイメージから生成されるため、ソースファイルの変更はチェックサムバイトの変更に反映されます。 チェックサムのバイトが、ファイルの読み込み済みイメージから生成されたチェックサムと一致しない場合は、ファイルが破損しているか、改ざんされていると見なされます。  
  
 一般的なチェックサムは、サイズが32バイトを超えることはありませんが、がチェックサムの最大サイズであるとは限りません。 チェックサムを取得するために `data` `NULL` 必要なバイト数を取得するには、パラメーターをに設定します。 次に、適切なサイズのバッファーを割り当て、このメソッドを新しいバッファーでもう一度呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSourceFile::get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md)
