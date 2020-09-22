---
title: カスタムデバッグエンジンを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementing
- debug engines, custom
- debugging [Debugging SDK], custom debug engines
ms.assetid: 52794238-6fae-451c-bf1c-99f344c6f173
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b2a73dfae7772d8edec076238704aa1b52c9b028
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842161"
---
# <a name="creating-a-custom-debug-engine"></a>カスタム デバッグ エンジンの作成
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグエンジン (DE) は、特定の実行時アーキテクチャのデバッグを可能にするコンポーネントです。 通常、実行時環境ごとに1つの DE 実装のみが存在します。  
  
> [!NOTE]
> Transact-sql と JScript には個別の DE が実装されていますが、VBScript と JScript は1つの DE を共有します。  
  
 DE はインタープリターやオペレーティングシステムと連携して、そのようなデバッグサービスを実行制御、ブレークポイント、および式の評価として提供します。 これらのサービスは、DE インターフェイスを介して実装されます。これにより、デバッガーが異なる動作モード間で移行する可能性があります。 詳細については、「 [操作モード](../../extensibility/debugger/operational-modes.md)」を参照してください。  
  
 DE の作成は、次の手順で構成されます。  
  
1. Visual Studio での DE の登録  
  
2. プログラムのデバッグを有効にする  
  
3. 実行制御と状態の評価  
  
4. イベントの送信  
  
5. 終了とデタッチ  
  
## <a name="in-this-section"></a>このセクションの内容  
 [カスタム デバッグ エンジンの登録](../../extensibility/debugger/registering-a-custom-debug-engine.md)  
 デバッグエンジンを Visual Studio に登録して使用できるようにするために必要な手順について説明します。  
  
 [デバッグするプログラムの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)  
 DE を使用してプログラムをデバッグする前に、DE を起動するか、既存のプログラムにアタッチする必要があることについて説明します。  
  
 [実行の制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)  
 アプリケーションをデバッグするために実行コントロール機能を実装する必要がある理由について説明します。  
  
 [イベントの送信](../../extensibility/debugger/sending-events.md)  
 デバッガーと、DCOM に基づくイベントモデルとしての逆の通信について説明します。  
  
 [切り離しとデタッチ](../../extensibility/debugger/termination-and-detaching.md)  
 通常の終了を実現する方法について説明します。これは、デバッグ対象のアプリケーションにブレークポイント、例外、実行時エラー、または無限ループがないことを意味します。  
  
 [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)  
 デバッグセッションで発生しているイベントの呼び出し順序を文書に記録します。  
  
 [方法: カスタム デバッグ エンジンのデバッグ](../../extensibility/debugger/how-to-debug-a-custom-debug-engine.md)  
 カスタム DE をデバッグする方法について説明します。  
  
## <a name="see-also"></a>参照  
 [Visual Studio デバッガーの拡張性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
