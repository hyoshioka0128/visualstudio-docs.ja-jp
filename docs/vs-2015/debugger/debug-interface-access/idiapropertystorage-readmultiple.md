---
title: 'IDiaPropertyStorage:: ReadMultiple |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadMultiple
ms.assetid: 6ccc9397-ce41-4f72-b261-72ac252cd4a5
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 40cd84e00f2e6abea285368a6206c7400abf8877
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538084"
---
# <a name="idiapropertystoragereadmultiple"></a>IDiaPropertyStorage::ReadMultiple
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定されたプロパティを現在のプロパティセットから読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT ReadMultiple(   
   ULONG          cpspec,  
   PROPSPEC const rgpspec,  
   PROPVARIANT    rgvar  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cpspec`  
 から配列に指定されたプロパティの数 `rgpspec` 。 0の場合、メソッドはプロパティを返しませんが、 `S_OK` 成功コードとしてを返します。  
  
 `rgpspec`  
 から読み取るプロパティの配列。 プロパティは、プロパティ ID または省略可能な文字列名のいずれかで指定できます。 配列内の特定の順序でプロパティを指定する必要はありません。 配列には重複するプロパティを含めることができます。その結果、単純なプロパティに対して戻り値のプロパティ値が重複します。 非単純なプロパティは、2回目に開こうとしたときにアクセスが拒否されたことを返します。 配列には、プロパティ Id と文字列 Id の組み合わせを含めることができます。 この配列には、少なく `cpspec` ともプロパティ値の数が含まれている必要があります。  
  
 `rgvar`  
 [入力、出力] `PROPVARIANT` 各プロパティの値が格納される構造体の配列 (VisualStudio 名前空間内) を指定します。 配列は、少なくともサイズの要素である必要があり `cpspec` ます。 呼び出し元は、配列内の値を初期化する必要はありません。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`1 つ以上のプロパティが見つからなかった場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 プロパティが見つからなかった場合、配列内の対応するエントリに `rgvar` は、の型のが含まれ `VARIANT` `VT_EMPTY` ます。  
  
## <a name="see-also"></a>参照  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
