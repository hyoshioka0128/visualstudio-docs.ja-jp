---
title: BeginCapture | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 9edbb52d-ee0b-4cc4-a382-972bcee067d3
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b16fdc4d0a12d7082400e697ca44a7ca4c549f9a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62431798"
---
# <a name="begincapture"></a>BeginCapture
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`EndCapture` で終了するキャプチャ区間を開始します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void BeginCapture();  
```  
  
## <a name="remarks"></a>Remarks  
 特定種類の描画呼び出しに関するグラフィック情報だけをキャプチャするときなど、キャプチャ区間は通常 1 つのフレームのサブセットに及びます。 キャプチャ区間が present への呼び出しに及ぶ場合は、2 つのフレームのグラフィックス情報がキャプチャされます。 最初のフレームは、`BeginCapture` への呼び出しと present への呼び出しの間の区間に及びます。2 つ目のフレームは、present への呼び出しの後の最初の Direct3D イベントと `EndCapture` への呼び出しの間の区間に及びます。  
  
 区間をキャプチャするには、グラフィックス情報をキャプチャして記録するようにアプリケーションを準備する必要があります。つまり、`BeginCapture` または `EndCapture` を呼び出す前に、`VsgDbg` クラスのインスタンスを通じて [Init](../debugger/init.md) を呼び出してしておく必要があります。  
  
## <a name="see-also"></a>参照  
 [EndCapture](../debugger/endcapture.md)   
 [CaptureCurrentFrame](../debugger/capturecurrentframe.md)
