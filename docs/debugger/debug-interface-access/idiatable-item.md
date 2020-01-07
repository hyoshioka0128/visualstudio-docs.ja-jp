---
title: 'IDiaTable:: Item |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::Item method
ms.assetid: eae11b26-4807-400c-be25-e85bbc0c6b20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d402f5ad54d5c0f487cebb3a8c53f68d17828ed4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738727"
---
# <a name="idiatableitem"></a>IDiaTable::Item
テーブル内の指定されたエントリへの参照を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Item ( 
   DWORD      index,
   IUnknown** element
);
```

#### <a name="parameters"></a>パラメーター
 `index`

から[IDiaTable:: get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)メソッドによって返される、0 ~ `count`-`count` 1 の範囲のテーブルエントリのインデックス。

 `element`

入出力指定されたテーブルエントリを表す `IUnknown` オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>Remarks
 テーブルは、オブジェクトのコレクションを表します。 これらのオブジェクトに応じて、要素パラメーターを適切なインターフェイスにキャストできます。 たとえば、テーブルに[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)オブジェクトが含まれている場合は、要素パラメーターを `IDiaSegment` インターフェイスにキャストできます。

 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)インターフェイスで適切な列挙子インターフェイスの `QueryInterface` メソッドを呼び出し、列挙子の特定のメソッドを使用してテーブルの内容にアクセスすることは、より一般的な方法です。 例については、 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)インターフェイスを参照してください。

## <a name="see-also"></a>関連項目
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
