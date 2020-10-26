---
title: 'IDiaEnumSectionContribs:: Clone |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Clone method
ms.assetid: 81d3f3a7-3684-4e5c-b028-29b268684a2c
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 56267cbbffd6b5ff123dcf08ee71200a9b343fac
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190023"
---
# <a name="idiaenumsectioncontribsclone"></a>IDiaEnumSectionContribs::Clone
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

現在の列挙子と同じ列挙状態を含む列挙子を作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Clone(   
   IDiaEnumSectionContrib** ppenum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 ppenum  
 入出力列挙子の複製を含む [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md) オブジェクトを返します。 セクションの投稿は重複しておらず、列挙子だけが複製されます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
