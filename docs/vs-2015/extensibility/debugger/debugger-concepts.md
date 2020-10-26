---
title: デバッガーの概念 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK]
ms.assetid: 2d371d38-f1a0-4a9a-8ea3-100e8c0149b7
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0f8dd5567fb21fafbac3c63b84dae1e0e33b0b91
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200619"
---
# <a name="debugger-concepts"></a>デバッガーの概念
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio デバッグパッケージでビルドするには、パッケージのデザインに使用されるアーキテクチャの概念を理解している必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [デバッグ セッション](../../extensibility/debugger/debug-session.md)  
 デバッグアーキテクチャにおけるセッションの役割について説明します。  
  
 [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)  
 抽象と物理的の両方の条件において、デバッグアーキテクチャに関してサーバーがどのようなものかを定義します。  
  
 [ポート サプライヤー](../../extensibility/debugger/port-suppliers.md)  
 デバッグアーキテクチャに関してポートサプライヤーを定義します。  
  
 [ポート](../../extensibility/debugger/ports.md)  
 デバッグアーキテクチャの観点からポートを定義します。  
  
 [処理](../../extensibility/debugger/processes.md)  
 デバッグアーキテクチャの観点からプロセスを定義します。  
  
 [プログラム ノード](../../extensibility/debugger/program-nodes.md)  
 デバッグアーキテクチャの観点からプログラムノードを定義します。これには、それ自体と、それが実行されているプロセスを識別する方法も含まれます。  
  
 [Programs](../../extensibility/debugger/programs.md)  
 デバッグアーキテクチャに関してプログラムを定義します。  
  
 [スレッド](../../extensibility/debugger/threads.md)  
 デバッグアーキテクチャに関してスレッドの特性を定義します。  
  
 [スタック フレーム](../../extensibility/debugger/stack-frames.md)  
 デバッグアーキテクチャの観点でスタックフレームを定義します。 スタックフレームは、スレッドの実行コンテキストを提供するスタックを抽象化したものです。  
  
 [モジュール](../../extensibility/debugger/modules.md)  
 デバッグアーキテクチャに関して、実行可能ファイルや DLL などのコードの物理的なコンテナーとしてモジュールを定義します。  
  
 [[ブレークポイント]](../../extensibility/debugger/breakpoints-visual-studio-sdk.md)  
 デバッグアーキテクチャに関して、3種類のブレークポイント (保留、バインド、エラー) を定義します。  
  
## <a name="related-sections"></a>関連項目  
 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)  
 コード、ドキュメント、および式の評価コンテキスト内でデバッグエンジン (DE) を同時に動作させる方法について説明します。 3つのコンテキストのそれぞれについて、場所、位置、または評価に関連する評価について説明します。  
  
 [デバッガーのコンポーネント](../../extensibility/debugger/debugger-components.md)  
 デバッグエンジン (DE)、式エバリュエーター (EE)、およびシンボルハンドラー (SH) など、Visual Studio のデバッグコンポーネントの概要について説明します。  
  
 [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)  
 プログラムの起動や式の評価など、さまざまなデバッグタスクへのリンクが含まれています。
