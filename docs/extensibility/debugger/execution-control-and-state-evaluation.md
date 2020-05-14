---
title: 実行制御と状態評価 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], execution control
- expression evaluation, control of execution
ms.assetid: 55adde38-1622-4b51-83cb-ce1b04c1ca7a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dc76ae97e8baa6ce78dd4d565109d6a19e2051e2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738755"
---
# <a name="execution-control-and-state-evaluation"></a>実行制御と状態評価
アプリケーションのデバッグでは、関数へのステップイン、ブレークポイントでの停止、実行の継続などの実行制御機能を実装する必要があります。 Visual Studio のデバッグは、デバッガー コンポーネント間で送信されるイベントに基づいて実行制御を行います。

## <a name="in-this-section"></a>このセクションの内容
 [プログラム制御](../../extensibility/debugger/program-control.md)プログラム レベルで発生する次のルーチンの一覧です: 次のステートメントの設定、実行、ステップ実行、続行、中断、および再開します。

 [ブレークポイント関連のメソッド](../../extensibility/debugger/breakpoint-related-methods.md)Visual Studio でサポートされるブレークポイントのバインド型と保留中の種類を定義します。

 [コール スタックの評価](../../extensibility/debugger/call-stack-evaluation.md)中断モード中に呼び出し履歴のスタック フレームを表示できるようにするメソッドの実装について説明します。

 [式評価](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)デバッグ エンジン (DE)、式評価 (EE)、およびセッション デバッグ マネージャーが、IDE のウィンドウの 1 つに入力された式の解析と評価にどのように関与するかを説明します。

 [コントロール イベント](../../extensibility/debugger/control-events.md)プログラムの制御された実行中にイベントを送信するために使用されるインターフェイスについて説明します。
