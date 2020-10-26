---
title: 'IDiaEnumSectionContribs:: Item |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Item method
ms.assetid: 63a28f23-0ca0-44a7-b11b-ca0206d642a0
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 06a82fbb52ccdf0f9fb9fda50a74f2cfb30e7648
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190011"
---
# <a name="idiaenumsectioncontribsitem"></a>IDiaEnumSectionContribs::Item
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

インデックスを使ってセクションの貢献度を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Item (   
   DWORD                index,  
   IDiaSectionContrib** section  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 インデックス  
 から取得する [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) オブジェクトのインデックス。 インデックスの範囲は 0 ~ `count` -1 です。ここで `count` 、は [IDiaEnumSectionContribs:: get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md) メソッドによって返されます。  
  
 section  
 入出力目的のセクションの貢献度を表す [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumSectionContribs:: get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)   
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
