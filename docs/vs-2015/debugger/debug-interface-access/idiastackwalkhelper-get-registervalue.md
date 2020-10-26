---
title: 'IDiaStackWalkHelper:: get_registerValue |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::get_registerValue method
ms.assetid: 46ac5eee-73a3-44a1-8635-6c58ba193cb6
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4dde30ebcda46d75271b15ec5b7f7c1ac49f384b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150117"
---
# <a name="idiastackwalkhelperget_registervalue"></a>IDiaStackWalkHelper::get_registerValue
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

レジスタの値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_registerValue (   
   DWORD      index,  
   ULONGLONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `index`  
 から値を取得するレジスタを指定する [CV_HREG_e 列挙](../../debugger/debug-interface-access/cv-hreg-e.md) 列挙の値。  
  
 `pRetVal`  
 入出力レジスタの現在の値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 パラメーターのサイズにかかわらず `pRetVal` 、実装には、通常、レジスタが保持しているものだけを格納する必要があります。 たとえば、8ビットレジスタは、指定された値のうち最も下位の8ビットだけを保持します。 この8ビット値は、このメソッドから返された場合は64ビットに拡張されます。  
  
## <a name="see-also"></a>参照  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)   
 [CV_HREG_e 列挙型](../../debugger/debug-interface-access/cv-hreg-e.md)
