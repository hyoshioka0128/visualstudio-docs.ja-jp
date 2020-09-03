---
title: 'IDiaEnumSourceFiles:: Clone |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Clone method
ms.assetid: 87a9a9b6-3927-4131-927c-ad95f8f098b9
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7283a41908b41ae59c5651384f11c996e9b7265f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189838"
---
# <a name="idiaenumsourcefilesclone"></a>IDiaEnumSourceFiles::Clone
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

現在の列挙子と同じ列挙状態を含む列挙子を作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Clone (   
   IDiaEnumSourceFiles** ppenum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 ppenum  
 入出力列挙子の複製を含む [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md) オブジェクトを返します。 ソースファイルは重複していません。列挙子だけが対象となります。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
