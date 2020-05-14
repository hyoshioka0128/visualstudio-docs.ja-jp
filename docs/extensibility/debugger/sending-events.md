---
title: イベントの送信 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5ec0d3aa29da562147b71b8efde49baf07d8ae0b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713039"
---
# <a name="send-events"></a>送信イベント
デバッガーとデバッグ エンジン (DE) の間の通信のメカニズムは、DCOM に基づくイベント モデルです。 イベントは COM オブジェクトとして送信され、各イベントには次のパラメータを指定します。

- イベントを呼び出した DE。

- 何が起こったかの説明。

- イベントが発生した場所のコンテキストを識別するプロセス、プログラム、およびスレッド情報。 プロセスは DE から送信されるイベントに送信されません。

- イベントが同期か非同期かを示すイベントの種類。

  すべてのデバッグ イベントは、メソッド[IDebugEventCallback2::Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md)を使用して送信されます。

## <a name="in-this-section"></a>このセクションの内容
 [イベントソース](../../extensibility/debugger/event-sources-visual-studio-sdk.md)イベントの 2 つのソースについて説明します: デバッグ エンジン (DE) とセッション デバッグ マネージャー (SDM)。

 [サポートされているイベントの種類](../../extensibility/debugger/supported-event-types.md)現在サポートされているイベントの種類 (非同期および同期) について説明します。

 [イベントの説明](../../extensibility/debugger/event-descriptions.md)イベントとその使用理由を定義します。

## <a name="related-sections"></a>関連項目
 [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)デがインタプリタまたはオペレーティング システムと連携してデバッグ サービスを提供するしくみについて説明します。
