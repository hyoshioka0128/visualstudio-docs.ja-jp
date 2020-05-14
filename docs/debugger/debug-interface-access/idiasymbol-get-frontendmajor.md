---
title: 'IDiaSymbol:: get_frontEndMajor |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_frontEndMajor method
ms.assetid: f8a067c5-3306-4fc5-bc20-8910a47ed504
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd15bb798d35ebac1a8f3af7b766ffd9aeea7d8e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740636"
---
# <a name="idiasymbolget_frontendmajor"></a>IDiaSymbol::get_frontEndMajor
フロントエンドメジャーバージョン番号を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_frontEndMajor ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

入出力フロントエンドメジャーバージョン番号を返します。 「解説」を参照してください。

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