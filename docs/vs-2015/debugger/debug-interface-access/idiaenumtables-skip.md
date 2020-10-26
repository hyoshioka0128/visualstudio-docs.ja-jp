---
title: 'IDiaEnumTables:: Skip |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Skip method
ms.assetid: 5c9db956-0654-4f1a-8775-530aa980d8ec
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4498789b3497ea70faf9948fcf0d03c6196f250e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161454"
---
# <a name="idiaenumtablesskip"></a>IDiaEnumTables::Skip
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

列挙シーケンス内の指定された数のテーブルをスキップします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Skip (   
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `celt`  
 からスキップする列挙シーケンス内のテーブルの数。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返します。 `S_OK` それ以外の場合は、 `S_FALSE` スキップするテーブルがない場合はを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
