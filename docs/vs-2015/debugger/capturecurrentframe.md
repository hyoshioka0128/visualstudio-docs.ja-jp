---
title: CaptureCurrentFrame | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 4509311d-6fe2-4b65-9b4a-ff0522585d6a
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2718e800e2a31eb66319259ed1e43f2ab8b084c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161633"
---
# <a name="capturecurrentframe"></a>CaptureCurrentFrame
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

現在のフレームの残りの部分を、グラフィックス ログ ファイルにキャプチャします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void CaptureCurrentFrame();  
```  
  
## <a name="remarks"></a>Remarks  
 `BeginCapture` 関数によって開始されたキャプチャなど、別のキャプチャ操作が進行中の場合、そのキャプチャ操作は完了し、別個のフレームとしてグラフィックス ログに記録されます。 その直後、グラフィックス診断によって現在のフレームの残りの部分のキャプチャが開始され、それも個別のフレームとして記録されます。 present への呼び出しによって、現在のフレームの末尾がマークされます。  
  
 フレームをキャプチャするには、グラフィックス情報をキャプチャして記録するようにアプリケーションを準備する必要があります。つまり、`CaptureCurrentFrame` を呼び出す前に、`VsgDbg` クラスのインスタンスを通じて [Init](../debugger/init.md) を呼び出してしておく必要があります。  
  
## <a name="see-also"></a>参照  
 [初期化](../debugger/init.md)   
 [BeginCapture](../debugger/begincapture.md)
