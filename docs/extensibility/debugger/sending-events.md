---
title: イベントの送信 |Microsoft Docs
description: デバッガーとデバッグエンジンで DCOM に基づくイベントモデルを使用する方法について説明します。 イベントは COM オブジェクトとして送信されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: eb86be560f45941b1ca5eb04f38087c23c431fda
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99960859"
---
# <a name="send-events"></a>送信イベント
デバッガーとデバッグエンジン (DE) 間の通信機構は、DCOM に基づくイベントモデルです。 イベントは COM オブジェクトとして送信され、各イベントには次のものを指定するパラメーターがあります。

- イベントを呼び出した DE。

- 何が起こったかについての説明。

- イベントが発生したコンテキストを識別するプロセス、プログラム、スレッド情報。 このプロセスは、DE から送信されたイベントに対しては送信されません。

- イベントが同期または非同期のどちらであるかを示すイベントの種類。

  すべてのデバッグイベントは、メソッド [IDebugEventCallback2:: Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md)を使用して送信されます。

## <a name="in-this-section"></a>このセクションの内容
 [イベントソース](../../extensibility/debugger/event-sources-visual-studio-sdk.md) デバッグエンジン (DE) とセッションデバッグマネージャー (SDM) の2つのイベントソースについて説明します。

 [サポートされるイベントの種類](../../extensibility/debugger/supported-event-types.md) 現在サポートされているイベントの種類 (非同期および同期) について説明します。

 [イベントの説明](../../extensibility/debugger/event-descriptions.md) イベントとその用途の理由を定義します。

## <a name="related-sections"></a>関連項目
 [カスタムデバッグエンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md) インタープリターやオペレーティングシステムを使用してデバッグサービスを提供する方法について説明します。
