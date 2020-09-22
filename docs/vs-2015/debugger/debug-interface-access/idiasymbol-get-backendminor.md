---
title: 'IDiaSymbol:: get_backEndMinor |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_backEndMinor method
ms.assetid: 37f38d19-6685-440d-a477-7127c4f8699e
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: db90118a1c8d235637f78edd9daa51f3531c628d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842173"
---
# <a name="idiasymbolget_backendminor"></a>IDiaSymbol::get_backEndMinor
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

コンパイラのバックエンドマイナーバージョン番号を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_backEndMinor (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力バックエンドのマイナーバージョン番号を返します。 「解説」を参照してください。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、その `S_FALSE` シンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="remarks"></a>注釈  
 通常、コンパイラは、ソースコードを中間形式に解析するフロントエンド (パーサー) とバックエンド (コードジェネレーター) という2つの主要要素で構成されています。この要素は、中間形式をアセンブリに変換します。 フロントエンドがバックエンドとは異なるバージョンを持つことは珍しくありません。  
  
 フロントエンドまたはバックエンドのバージョン番号は、.. という3つの部分で構成されます。 \<major> \<minor> はメジャーバージョン番号、は \<build> \<major> \<minor> マイナーバージョン番号、 \<build> はビルド番号です。 例: 13.10.3077。  
  
## <a name="requirements"></a>要件  
  
|要件|説明|  
|-----------------|-----------------|  
|ヘッダー:|dia2|  
|バージョン:|DIA SDK v1.0|  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
