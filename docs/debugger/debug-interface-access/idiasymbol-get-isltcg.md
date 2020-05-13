---
title: 'IDiaSymbol:: get_isLTCG |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isLTCG method
ms.assetid: 5f7f05b8-6b71-4958-9e1e-e4924ef9c59b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1d3fa97d5612b61151d9c435b91f500c87af0b23
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740216"
---
# <a name="idiasymbolget_isltcg"></a>IDiaSymbol::get_isLTCG
[コンパイル単位](../../debugger/debug-interface-access/compiland.md)がリンカースイッチ[/ltcg (リンク時のコード生成)](/cpp/build/reference/ltcg-link-time-code-generation)にリンクされているかどうかを指定するフラグを取得します。これにより、プログラム全体の最適化を支援します。 このスイッチは、マネージコードにのみ適用されます。

## <a name="syntax"></a>構文

```C++
HRESULT get_iSLTCG(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>パラメーター
 pFlag

入出力@No__t_1 が/LTCG リンカースイッチに関連付けられている場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラーコードを返します。

> [!NOTE]
> @No__t_0 の戻り値は、そのシンボルに対してプロパティを使用できないことを意味します。

## <a name="requirements"></a>［要件］

|必要条件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2|
|バージョン:|DIA SDK v1.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
