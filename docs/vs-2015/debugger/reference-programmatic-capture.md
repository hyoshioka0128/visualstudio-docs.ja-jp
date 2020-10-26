---
title: 参照 (プログラムによるキャプチャ) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
ms.assetid: ef60eb8d-1ac2-4e3a-9b4b-f6da0bdd9da8
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8cebeb7eb651c11b5f560b981df30213fc726c66
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68162261"
---
# <a name="reference-programmatic-capture"></a>参照 (プログラムによるキャプチャ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

グラフィックス診断は、プログラム キャプチャ API によってキャプチャ機能のプログラムによる制御をサポートします。 この API を使用すると、メッセージをグラフィックス診断 HUD (ヘッドアップ ディスプレイ) に切り替えたり、追加したり、グラフィック ログ ファイルを初期化および作成したり、グラフィックス情報をキャプチャしたりできます。  
  
## <a name="programmatic-capture-apis"></a>プログラム キャプチャ API  
  
### <a name="classes"></a>クラス  
  
|名前|説明|  
|----------|-----------------|  
|[VsgDbg クラス](../debugger/vsgdbg-class.md)|グラフィックス診断のアプリ内コンポーネントのプログラムによる制御に使用するインターフェイスを表します。|  
  
### <a name="preprocessor-symbols"></a>プリプロセッサ シンボル  
  
|名前|説明|  
|----------|-----------------|  
|[DONT_SAVE_VSGLOG_TO_TEMP](../debugger/dont-save-vsglog-to-temp.md)|その存在によって、グラフィックス ログ ファイルがユーザーの一時ファイル ディレクトリに保存されるかどうかを定義します。|  
|[VSG_DEFAULT_RUN_FILENAME](../debugger/vsg-default-run-filename.md)|グラフィックス ログ ファイルの既定のファイル名を定義します。|  
|[VSG_NODEFAULT_INSTANCE](../debugger/vsg-nodefault-instance.md)|その存在によって、`VsgDbg` クラスの既定のインスタンスが提供されるかどうかを定義します。|  
  
## <a name="related-articles"></a>関連トピック  
  
|Title|説明|  
|-----------|-----------------|  
|[Capturing Graphics Information](../debugger/capturing-graphics-information.md)|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のグラフィックス診断ツールを使用してレンダリングに関する問題を診断できるように、DirectX ベースのアプリからグラフィックス情報をキャプチャする方法を示します。|  
|[概要](../debugger/overview-of-visual-studio-graphics-diagnostics.md)|グラフィックス診断によって、DirectX ベースのゲームやアプリのレンダリング エラーのデバッグがどのように簡単になるかを示します。|
