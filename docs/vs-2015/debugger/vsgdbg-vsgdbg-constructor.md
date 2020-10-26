---
title: VsgDbg::VsgDbg (コンストラクター) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 670651e6-5e79-4845-b0c2-671beb7055a8
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f3bd179aea7d961df6145b7af2f074927fcdc3e3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157440"
---
# <a name="vsgdbgvsgdbg-constructor"></a>VsgDbg::VsgDbg (コンストラクター)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定されたブール値パラメーターに基づいて、既定でグラフィックス情報をアクティブにキャプチャして記録するようにグラフィックス診断のアプリ内コンポーネントを準備をするか、または準備しないで、`VsgDbg` クラスのインスタンスを構築します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
VsgDbg(  
  bDefaultInit  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `bDefaultInit`  
 `true` グラフィックス情報をアクティブにキャプチャして記録するためにグラフィックス診断のアプリ内コンポーネントを準備するように指定するには、現時点 `false` では、グラフィックス情報をアクティブにキャプチャして記録するようにアプリを準備しないことを指定する場合。  
  
## <a name="remarks"></a>Remarks  
 `bDefaultInit` に `true` が設定された状態でコンストラクターが呼び出された場合、グラフィックス ログ ファイルの名前は、`vsgcapture.h` がアプリケーションに含まれる前にプリプロセッサ シンボル `DONT_SAVE_VSGLOG_TO_TEMP` および `VSG_DEFAULT_RUN_FILENAME` がどのように定義されているかによって決まります。  
  
 `bDefaultInit` が `false` に設定された状態でコンストラクターが呼び出された場合、後で `Init` 関数を呼び出して、グラフィックス情報をアクティブにキャプチャして記録するようにグラフィックス診断のアプリ内コンポーネントを準備できます。  
  
## <a name="see-also"></a>参照  
 [VsgDbg:: ~ VsgDbg (デストラクター)](../debugger/vsgdbg-tilde-vsgdbg-destructor.md)   
 [初期化](../debugger/init.md)   
 [DONT_SAVE_VSGLOG_TO_TEMP](../debugger/dont-save-vsglog-to-temp.md)   
 [VSG_DEFAULT_RUN_FILENAME](../debugger/vsg-default-run-filename.md)
