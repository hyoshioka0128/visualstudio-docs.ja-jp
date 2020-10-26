---
title: パッケージのデバッグ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dda8b1ac6eaa2cd5352d441600ae720c3aac321c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68181295"
---
# <a name="debug-package"></a>パッケージのデバッグ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグパッケージは、Visual Studio シェルで実行され、すべての UI を処理します。 このメソッドは、Visual Studio のデバッグインターフェイスを使用し、セッションデバッグマネージャー (SDM) と通信します。  
  
 SDM を介して送信されたイベントを中断するデバッガーを実行モードから中断モードに切り替え、中断が発生したプログラムにフォーカスを移動します。 デバッグパッケージは、イベントによって送信された情報から、スタックフレームとスレッドを追跡します。  
  
 デバッグパッケージには、言語または実行時の環境依存関係はありません。 デバッグパッケージを実装または変更する必要はありません。  
  
 デバッグパッケージは vsdebug.dll によって実装されます。  
  
## <a name="see-also"></a>参照  
 [セッションデバッグマネージャー](../../extensibility/debugger/session-debug-manager.md)   
 [スタックフレーム](../../extensibility/debugger/stack-frames.md)   
 [レッド](../../extensibility/debugger/threads.md)   
 [デバッガーのコンポーネント](../../extensibility/debugger/debugger-components.md)
