---
title: カスタムデバッグエンジンを作成する |Microsoft Docs
description: この記事では、特定のランタイムアーキテクチャのデバッグを可能にするデバッグエンジンの作成について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, implementing
- debug engines, custom
- debugging [Debugging SDK], custom debug engines
ms.assetid: 52794238-6fae-451c-bf1c-99f344c6f173
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7c0aa8550bc402520052003b59cf4ab1deaad7b2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888967"
---
# <a name="create-a-custom-debug-engine"></a>カスタムデバッグエンジンを作成する
デバッグエンジン (DE) は、特定の実行時アーキテクチャのデバッグを可能にするコンポーネントです。 通常、実行時環境ごとに1つの DE 実装のみが存在します。

> [!NOTE]
> Transact-sql と JScript には個別の DE が実装されていますが、VBScript と JScript は1つの DE を共有します。

 DE はインタープリターやオペレーティングシステムと連携して、そのようなデバッグサービスを実行制御、ブレークポイント、および式の評価として提供します。 これらのサービスは、DE インターフェイスを介して実装されます。これにより、デバッガーが異なる動作モード間で移行する可能性があります。 詳細については、「 [操作モード](../../extensibility/debugger/operational-modes.md)」を参照してください。

 DE の作成は、次の手順で構成されます。

1. Visual Studio での DE の登録

2. プログラムのデバッグを有効にする

3. 実行制御と状態評価の実装

4. 送信イベント

5. 終了とデタッチの設定

## <a name="in-this-section"></a>このセクションの内容
 [カスタムデバッグエンジンを登録する](../../extensibility/debugger/registering-a-custom-debug-engine.md) デバッグエンジンを Visual Studio に登録して使用できるようにするために必要な手順について説明します。

 [プログラムのデバッグを有効に](../../extensibility/debugger/enabling-a-program-to-be-debugged.md) するDE を使用してプログラムをデバッグする前に、DE を起動するか、既存のプログラムにアタッチする必要があることについて説明します。

 [実行制御と状態評価の実装](../../extensibility/debugger/execution-control-and-state-evaluation.md) アプリケーションをデバッグするために実行コントロール機能を実装する必要がある理由について説明します。

 [イベントの送信](../../extensibility/debugger/sending-events.md) デバッガーと、DCOM に基づくイベントモデルとしての逆の通信について説明します。

 [終了とデタッチの設定](../../extensibility/debugger/termination-and-detaching.md) 通常の終了を実現する方法について説明します。これは、デバッグ対象のアプリケーションにブレークポイント、例外、実行時エラー、または無限ループがないことを意味します。

 [デバッガーイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md) デバッグセッションで発生しているイベントの呼び出し順序を文書に記録します。

 [方法: カスタムデバッグエンジンをデバッグする](../../extensibility/debugger/how-to-debug-a-custom-debug-engine.md) カスタム DE をデバッグする方法について説明します。

## <a name="see-also"></a>関連項目
- [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
