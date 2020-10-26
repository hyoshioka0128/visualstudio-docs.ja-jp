---
title: VsgDbg::~VsgDbg (デストラクター) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c0ae3dd206953e728175f4479920861295feae00
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200303"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg (デストラクター)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`VsgDbg` クラスのインスタンスを破棄します。 グラフィックス情報がアクティブに記録されている場合、グラフィック ログ ファイルは終了して閉じられ、グラフィックス情報がアクティブにキャプチャされているときに使用されたリソースが解放されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
~VsgDbg();  
```  
  
## <a name="see-also"></a>参照  
 [VsgDbg::VsgDbg (コンストラクター)](../debugger/vsgdbg-vsgdbg-constructor.md)
