---
title: デバッガの概念 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK]
ms.assetid: 2d371d38-f1a0-4a9a-8ea3-100e8c0149b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ad8a450f9e79c1d44b8e098c8a00bb4b816e1af
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738985"
---
# <a name="debugger-concepts"></a>デバッガーの概念
Visual Studio デバッグ パッケージをビルドするには、パッケージのデザインに使用するアーキテクチャの概念を理解している必要があります。

## <a name="in-this-section"></a>このセクションの内容
 [デバッグ セッション](../../extensibility/debugger/debug-session.md)デバッグ アーキテクチャにおけるセッションの役割について説明します。

 [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)アーキテクチャのデバッグに関して、サーバーが抽象用語と物理用語の両方で何であるかを定義します。

 [港湾サプライヤー](../../extensibility/debugger/port-suppliers.md)デバッグ アーキテクチャの観点から、ポート サプライヤーが何であるかを定義します。

 [ポート](../../extensibility/debugger/ports.md)デバッグ アーキテクチャの観点から、ポートが何であるかを定義します。

 [プロセス](../../extensibility/debugger/processes.md)デバッグ アーキテクチャの観点から、プロセスが何であるかを定義します。

 [プログラムノード](../../extensibility/debugger/program-nodes.md)プログラム ノードをデバッグ アーキテクチャの観点から定義します。

 [プログラム](../../extensibility/debugger/programs.md)デバッグ アーキテクチャの観点からプログラムを定義します。

 [スレッド](../../extensibility/debugger/threads.md)デバッグ アーキテクチャの観点から、スレッドの特性を定義します。

 [スタック フレーム](../../extensibility/debugger/stack-frames.md)デバッグ アーキテクチャの観点からスタック フレームを定義します。 スタック フレームは、スレッドの実行コンテキストを提供するスタックの抽象化です。

 [モジュール](../../extensibility/debugger/modules.md)デバッグ アーキテクチャの観点から、実行可能ファイルや DLL などのコードの物理的なコンテナーとしてモジュールを定義します。

 [ブレークポイント](../../extensibility/debugger/breakpoints-visual-studio-sdk.md)デバッグ アーキテクチャの観点から、3 種類のブレークポイント (保留中、バインド、エラー) を定義します。

## <a name="related-sections"></a>関連項目
 [デバッガーのコンテキスト](../../extensibility/debugger/debugger-contexts.md)デバッグ エンジン (DE) がコード、ドキュメント、および式の評価コンテキスト内で同時に動作する方法について説明します。 3 つのコンテキストのそれぞれについて、そのコンテキストに関連する場所、位置、または評価について説明します。

 [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)デバッグ エンジン (DE)、式エバリュエーター (EE)、およびシンボル ハンドラー (SH) を含む Visual Studio のデバッグ コンポーネントの概要を説明します。

 [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)プログラムの起動や式の評価など、さまざまなデバッグ タスクへのリンクが含まれています。
