---
title: Stackフレーム Typeenum |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- StackFrameTypeEnum enumeration
ms.assetid: 61e40163-eee0-4c1f-af47-cef3771bdc41
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 655911bac1efbafe1838e24e2056282f9036479b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179192"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

スタックフレームの種類を指定します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
enum StackFrameTypeEnum {  
   FrameTypeFPO,  
   FrameTypeTrap,  
   FrameTypeTSS,  
   FrameTypeStandard,  
   FrameTypeFrameData,  
   FrameTypeUnknown = -1  
};  
```  
  
## <a name="elements"></a>要素  
 `FrameTypeFPO`  
 フレームポインターを省略します。FPO info を利用できます。  
  
 `FrameTypeTrap`  
 カーネルトラップフレーム。  
  
 `FrameTypeTSS`  
 カーネルトラップフレーム。  
  
 `FrameTypeStandard`  
 標準 EBP スタックフレーム。  
  
 `FrameTypeFrameData`  
 フレームポインターを省略します。使用可能なフレームデータ情報です。  
  
 `FrameTypeUnknown`  
 デバッグ情報が含まれていないフレーム。  
  
## <a name="remarks"></a>注釈  
 この列挙体の値は、 [IDiaStackFrame:: get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md) メソッドへの呼び出しによって返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: cvconst. h  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
