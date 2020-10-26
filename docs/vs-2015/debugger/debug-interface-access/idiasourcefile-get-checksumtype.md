---
title: 'IDiaSourceFile:: get_checksumType |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksumType method
ms.assetid: 4c363e61-a6a9-409a-9cc0-d06eb2bee645
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f859bce63e2976b23ab613e249dad41b2bc63486
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190697"
---
# <a name="idiasourcefileget_checksumtype"></a>IDiaSourceFile::get_checksumType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

チェックサムの種類を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_checksumType (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力チェックサムの種類を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 チェックサムの種類は、チェックサムアルゴリズムにマップできる値です。 たとえば、標準の PDB ファイル形式には、通常、次のいずれかの値を指定できます。  
  
|チェックサムの種類|CryptoAPI ラベル|説明|  
|-------------------|---------------------|-----------------|  
|0|\<none>|チェックサムが存在しません。|  
|1|`CALG_MD5`|MD5 ハッシュアルゴリズムを使用して生成されたチェックサム。|  
|2|`CALG_SHA1`|SHA1 ハッシュアルゴリズムを使用して生成されたチェックサム。|  
  
 `CryptoAPI`ラベルは列挙体からのものです `ALG_ID` 。 ハッシュアルゴリズムの詳細については、 `CryptoAPI` Microsoft の「」セクションを参照してください [!INCLUDE[winsdkshort](../../includes/winsdkshort-md.md)] 。  
  
 ソースファイルの実際のチェックサムのバイト数を取得するには、 [IDiaSourceFile:: get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md) メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)
