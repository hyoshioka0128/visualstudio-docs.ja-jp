---
title: 'IDiaFrameData:: get_program |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_program method
ms.assetid: 9201409e-b4b1-4e2e-a9f8-d17678ac538b
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d87f5c7fda25a901d44b9f511b9a92eb4471f845
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180011"
---
# <a name="idiaframedataget_program"></a>IDiaFrameData::get_program
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

現在の関数の呼び出しの前にレジスタセットを計算するために使用されるプログラム文字列を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_program (   
   BSTR* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力プログラム文字列を返します。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`このプロパティがサポートされていない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 プログラム文字列は、プロローグを確立するために解釈されるマクロのシーケンスです。 たとえば、一般的なスタックフレームでは、プログラム文字列を使用する場合があり `"$T0 $ebp = $eip $T0 4 + ^ = $ebp $T0 ^ = $esp $T0 8 + ="` ます。 形式は、逆ポーランド表記で、演算子はオペランドに従います。 `T0` スタック上の一時変数を表します。 この例では、次の手順を実行します。  
  
1. レジスタの内容 `ebp` をに移動 `T0` します。  
  
2. アドレスを生成するには、 `4` の値にを追加 `T0` し、そのアドレスから値を取得して、値を register に格納し `eip` ます。  
  
3. に格納されているアドレスから値を取得 `T0` し、その値を register に格納し `ebp` ます。  
  
4. `8`の値にを追加 `T0` し、その値を register に格納し `esp` ます。  
  
   プログラム文字列は CPU と、現在のスタックフレームによって表される関数に設定されている呼び出し規約に固有であることに注意してください。  
  
## <a name="see-also"></a>参照  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
