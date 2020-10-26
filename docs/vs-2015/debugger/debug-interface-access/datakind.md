---
title: DataKind |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- DataKind enumeration
ms.assetid: b64be708-22d6-4360-99e7-8f4e6b196de7
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a6a72d1093bc8acd9aae788ff357aee2efeb9e52
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197634"
---
# <a name="datakind"></a>DataKind
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

データ値の特定のスコープを示します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
enum DataKind {   
   DataIsUnknown,  
   DataIsLocal,  
   DataIsStaticLocal,  
   DataIsParam,  
   DataIsObjectPtr,  
   DataIsFileStatic,  
   DataIsGlobal,  
   DataIsMember,  
   DataIsStaticMember,  
   DataIsConstant  
};  
```  
  
## <a name="elements"></a>要素  
 DataIsUnknown  
 データシンボルを特定できません。  
  
 DataIsLocal  
 データ項目はローカル変数です。  
  
 DataIsStaticLocal  
 データ項目は静的なローカル変数です。  
  
 Dataisparc  
 データ項目は、仮パラメーターです。  
  
 DataIsObjectPtr  
 データ項目はオブジェクトポインター ( `this` ) です。  
  
 DataIsFileStatic  
 データ項目はファイルスコープの変数です。  
  
 DataIsGlobal  
 データ項目はグローバル変数です。  
  
 DataIsMember  
 データ項目はオブジェクトメンバー変数です。  
  
 DataIsStaticMember  
 データ項目は、クラスの静的変数です。  
  
 DataIsConstant  
 データ項目は定数値です。  
  
## <a name="remarks"></a>注釈  
 この列挙体の値は、 [IDiaSymbol:: get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md) メソッドによって返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: cvconst. h  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)
