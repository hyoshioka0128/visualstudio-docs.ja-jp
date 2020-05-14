---
title: 'IDiaSymbol:: get_frontEndMinor |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_frontEndMinor method
ms.assetid: 40792153-827c-4859-be7c-6aa16d5abab6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b329cd69d010cba4e3667bde0d7b976389037bb
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740643"
---
# <a name="idiasymbolget_frontendminor"></a>IDiaSymbol::get_frontEndMinor
フロントエンドのマイナーバージョン番号を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_frontEndMinor ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

入出力最上位のマイナーバージョン番号を返します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="remarks"></a>Remarks
 通常、コンパイラは、ソースコードを中間形式に解析するフロントエンド (パーサー) とバックエンド (コードジェネレーター) という2つの主要要素で構成されています。この要素は、中間形式をアセンブリに変換します。 フロントエンドがバックエンドとは異なるバージョンを持つことは珍しくありません。

 フロントエンドまたはバックエンドのバージョン番号は、\<major > の3つの部分で構成されます。> を \<minor します。> \<build、> \<major メジャーバージョン番号、\<minor > がマイナーバージョン番号、\<build > がビルド番号です。 例: 13.10.3077。

## <a name="requirements"></a>［要件］

|必要条件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2|
|バージョン:|DIA SDK v1.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)