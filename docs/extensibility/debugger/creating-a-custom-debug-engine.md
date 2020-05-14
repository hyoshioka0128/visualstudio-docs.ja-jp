---
title: カスタム デバッグ エンジンの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementing
- debug engines, custom
- debugging [Debugging SDK], custom debug engines
ms.assetid: 52794238-6fae-451c-bf1c-99f344c6f173
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a350d640fffcc6e09cf8f981c797b97071a0cacf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739042"
---
# <a name="create-a-custom-debug-engine"></a>カスタム デバッグ エンジンを作成する
デバッグ エンジン (DE) は、特定のランタイム アーキテクチャのデバッグを可能にするコンポーネントです。 通常、実行時環境ごとに 1 つの DE 実装しかありません。

> [!NOTE]
> TRANSACT-SQL と JScript には個別の DE 実装がありますが、VBScript と JScript は 1 つの DE を共有します。

 DE はインタプリタまたはオペレーション システムと連携して、実行制御、ブレークポイント、式評価などのデバッグ サービスを提供します。 これらのサービスは、DE インターフェイスを通じて実装され、デバッガーが異なる操作モード間で遷移する可能性があります。 詳細については、[操作モード](../../extensibility/debugger/operational-modes.md)を参照してください。

 DE の作成は、次の手順で構成されます。

1. デを登録する

2. プログラムのデバッグを有効にする

3. 実行制御と状態評価の実装

4. 送信イベント

5. 終了とデタッチの設定

## <a name="in-this-section"></a>このセクションの内容
 [カスタム デバッグ エンジンを登録する](../../extensibility/debugger/registering-a-custom-debug-engine.md)デバッグ エンジンを使用できるように Visual Studio に登録するために必要な手順について説明します。

 [プログラムのデバッグを有効にする](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)DE がプログラムをデバッグする前に、まず DE を起動するか、既存のプログラムにアタッチする必要があることを説明します。

 [実行制御と状態評価の実装](../../extensibility/debugger/execution-control-and-state-evaluation.md)アプリケーションのデバッグで実行制御機能を実装する必要がある理由について説明します。

 [イベントの送信](../../extensibility/debugger/sending-events.md)DCOM に基づくイベント モデルとして、デバッガーと DE 間の通信について説明します。

 [終了とデタッチの設定](../../extensibility/debugger/termination-and-detaching.md)デバッグするアプリケーションにブレークポイント、例外、ランタイム エラー、または無限ループが存在しない、正常な終了を実現する方法について説明します。

 [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)デバッグ セッションで発生するイベントの呼び出し順序を文書化します。

 [方法: カスタム デバッグ エンジンをデバッグする](../../extensibility/debugger/how-to-debug-a-custom-debug-engine.md)カスタム DE をデバッグする方法について説明します。

## <a name="see-also"></a>関連項目
- [デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
