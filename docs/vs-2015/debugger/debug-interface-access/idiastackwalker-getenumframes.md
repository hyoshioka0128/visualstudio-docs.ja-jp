---
title: 'IDiaStackWalker:: getEnumFrames |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalker2::getEnumFrames method
ms.assetid: f9f09729-4c34-441c-989c-e0b7339ee32c
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8cbad02474af48ac4da72784659dd27007211e64
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68144710"
---
# <a name="idiastackwalkergetenumframes"></a>IDiaStackWalker::getEnumFrames
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

X86 プラットフォームのスタックフレーム列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT getEnumFrames(   
   IDiaStackWalkHelper*   pHelper,  
   IDiaEnumStackFrames**  ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pHelper`  
 からヘルパー [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md) オブジェクト。  
  
 `ppEnum`  
 入出力[IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)オブジェクトの一覧を含む[IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 その他のプラットフォームでスタックフレームリストを取得するには、 [IDiaStackWalker:: getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md) メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)   
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)   
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)   
 [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)
