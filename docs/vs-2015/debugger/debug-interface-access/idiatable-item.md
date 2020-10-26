---
title: 'IDiaTable:: Item |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::Item method
ms.assetid: eae11b26-4807-400c-be25-e85bbc0c6b20
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6112a4580a68a98407723afab1ec3310d0f1cca9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62574802"
---
# <a name="idiatableitem"></a>IDiaTable::Item
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

テーブル内の指定されたエントリへの参照を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Item (   
   DWORD      index,  
   IUnknown** element  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `index`  
 から0 ~-1 の範囲のテーブルエントリのインデックス `count` 。ここで、 `count` は [IDiaTable:: get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)メソッドによって返されます。  
  
 `element`  
 入出力 `IUnknown` 指定されたテーブルエントリを表すオブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 テーブルは、オブジェクトのコレクションを表します。 これらのオブジェクトに応じて、要素パラメーターを適切なインターフェイスにキャストできます。 たとえば、テーブルに [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) オブジェクトが含まれている場合は、要素パラメーターをインターフェイスにキャストでき `IDiaSegment` ます。  
  
 `QueryInterface` [IDiaTable](../../debugger/debug-interface-access/idiatable.md)インターフェイスで適切な列挙子インターフェイスのメソッドを呼び出し、列挙子の特定のメソッドを使用してテーブルの内容にアクセスすることは、より一般的な方法です。 例については、 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) インターフェイスを参照してください。  
  
## <a name="see-also"></a>参照  
 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)   
 [IDiaTable:: get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)   
 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)   
 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
