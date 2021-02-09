---
title: 実行制御と状態の評価 |Microsoft Docs
description: デバッガーコンポーネント間で送信されるイベントに対して Visual Studio のデバッグが実行制御をどのように行うかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], execution control
- expression evaluation, control of execution
ms.assetid: 55adde38-1622-4b51-83cb-ce1b04c1ca7a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 187663390c1d3625e74db6cf397a304f5d699189
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921526"
---
# <a name="execution-control-and-state-evaluation"></a>実行制御と状態の評価
アプリケーションをデバッグするには、関数のステップイン、ブレークポイントでの停止、実行の継続といった実行制御機能を実装する必要があります。 Visual Studio のデバッグは、デバッガーコンポーネント間で送信されるイベントに基づいて実行制御を行います。

## <a name="in-this-section"></a>このセクションの内容
 [プログラムの制御](../../extensibility/debugger/program-control.md) プログラムレベルで発生する次のルーチンの一覧を示します。次のステートメントの設定、実行、ステップ実行、続行、中断、および再開します。

 [ブレークポイントに関連するメソッド](../../extensibility/debugger/breakpoint-related-methods.md) Visual Studio でサポートされているブレークポイントのバインドおよび保留の種類を定義します。

 [呼び出し履歴の評価](../../extensibility/debugger/call-stack-evaluation.md) 中断モード中に呼び出し履歴のスタックフレームを表示できるようにするメソッドの実装について説明します。

 [式の評価](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md) デバッグエンジン (DE)、式の評価 (EE)、およびセッションデバッグマネージャーが、IDE のいずれかのウィンドウに入力された式の解析と評価にどのように関係しているかについて説明します。

 [コントロールイベント](../../extensibility/debugger/control-events.md) プログラムの制御された実行中にイベントを送信するために使用するインターフェイスについて説明します。
