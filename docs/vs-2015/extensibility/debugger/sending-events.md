---
title: イベントの送信 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 98247b894d2db628d508713875ba0ea7d0642729
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204744"
---
# <a name="sending-events"></a>イベントの送信
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーとデバッグエンジン (DE) 間の通信機構は、DCOM に基づくイベントモデルです。 イベントは COM オブジェクトとして送信され、各イベントには次のものを指定するパラメーターがあります。  
  
- イベントを呼び出した DE。  
  
- 何が起こったかについての説明。  
  
- イベントが発生したコンテキストを識別するプロセス、プログラム、スレッド情報。 このプロセスは、DE から送信されたイベントに対しては送信されません。  
  
- イベントが同期または非同期のどちらであるかを示すイベントの種類。  
  
  すべてのデバッグイベントは、メソッド [IDebugEventCallback2:: Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md)を使用して送信されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [イベントソース](../../extensibility/debugger/event-sources-visual-studio-sdk.md)  
 デバッグエンジン (DE) とセッションデバッグマネージャー (SDM) の2つのイベントソースについて説明します。  
  
 [サポートされているイベントの種類](../../extensibility/debugger/supported-event-types.md)  
 現在サポートされているイベントの種類 (非同期および同期) について説明します。  
  
 [イベントの説明](../../extensibility/debugger/event-descriptions.md)  
 イベントとその用途の理由を定義します。  
  
## <a name="related-sections"></a>関連項目  
 [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
 インタープリターやオペレーティングシステムを使用してデバッグサービスを提供する方法について説明します。
