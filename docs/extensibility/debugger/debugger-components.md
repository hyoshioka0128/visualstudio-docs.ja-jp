---
title: デバッガーコンポーネント |Microsoft Docs
description: VSPackage として実装されている Visual Studio デバッガーによって管理されるデバッグセッションを構成する要素について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], components
- components [Visual Studio SDK], debugging
- debugging [Debugging SDK], components
ms.assetid: 8b8ab77f-a134-495c-be42-3bc51aa62dfb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2fa0a7feb85437cc8173d52695ddb1ba0d2c06b7
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914102"
---
# <a name="debugger-components"></a>デバッガーコンポーネント
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッガーは VSPackage として実装され、デバッグセッション全体を管理します。 デバッグセッションは、次の要素で構成されています。

- **パッケージのデバッグ:** デバッガーは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグされている内容に関係なく、同じユーザーインターフェイスを提供します。

- **セッションデバッグマネージャー (SDM):** さまざまなデバッグエンジンを管理するための、一貫したプログラムインターフェイスをデバッガーに提供し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 これはによって実装され [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- **プロセスデバッグマネージャー (PDM):** のすべての実行中のインスタンスについて、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] またはデバッグ中のすべてのプログラムの一覧を管理します。 これはによって実装され [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- **デバッグエンジン (DE):** は、デバッグ中のプログラムの監視、実行中のプログラムの状態と SDM および PDM との通信、および式エバリュエーターとシンボルプロバイダーとの対話によって、プログラムのメモリと変数の状態をリアルタイムに分析します。 これは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (サポートされる言語について) およびサードパーティベンダーが独自の実行時間をサポートすることによって実装されます。

- **式エバリュエーター (EE):** 特定の時点でプログラムが停止したときに、ユーザーが指定した変数および式を動的に評価するためのサポートを提供します。 この機能は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (サポートされる言語について) およびサードパーティベンダーが独自の言語をサポートすることによって実装されます。

- **シンボルプロバイダー (SP):** シンボルハンドラーとも呼ばれ、プログラムのデバッグシンボルをプログラムの実行中のインスタンスにマップして、意味のある情報を提供できるようにします (ソースコードレベルのデバッグや式の評価など)。 これは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (共通言語ランタイム [CLR] シンボルとプログラムデータベースの [PDB] シンボルファイル形式) によって実装され、独自の独自のメソッドを使用してデバッグ情報を格納するサードパーティベンダーによって実装されます。

  次の図は、Visual Studio デバッガーのこれらの要素間の関係を示しています。

  ![デバッグコンポーネントの概要](../../extensibility/debugger/media/dbugcompovrview.gif "Dバグの表示")

## <a name="in-this-section"></a>このセクションの内容
 [パッケージのデバッグ](../../extensibility/debugger/debug-package.md) シェルで実行され、すべての UI を処理するデバッグパッケージについて説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

 [プロセスデバッグマネージャー](../../extensibility/debugger/process-debug-manager.md) PDM の機能の概要について説明します。これは、デバッグ可能なプロセスのマネージャーです。

 [セッションデバッグマネージャー](../../extensibility/debugger/session-debug-manager.md) IDE にデバッグセッションの統合ビューを提供する SDM を定義します。 SDM は、DE を管理します。

 [デバッグエンジン](../../extensibility/debugger/debug-engine.md) DE によって提供されるデバッグサービスについて説明します。

 [操作モード](../../extensibility/debugger/operational-modes.md) IDE が動作する3つのモード (デザインモード、実行モード、および中断モード) の概要について説明します。 移行メカニズムについても説明します。

 [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md) 実行時の EE の目的について説明します。

 [シンボルプロバイダー](../../extensibility/debugger/symbol-provider.md) 実装時に、シンボルプロバイダーが変数と式を評価する方法について説明します。

 [型ビジュアライザーとカスタムビューアー](../../extensibility/debugger/type-visualizer-and-custom-viewer.md) 型ビジュアライザーとカスタムビューアーの概要、および式エバリュエーターが両方をサポートするために果たす役割について説明します。

## <a name="related-sections"></a>関連項目
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md) 主要なデバッグ アーキテクチャの概念について説明します。

 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md) コード、ドキュメント、式の評価コンテキスト内で DE がどのように同時操作されるかについて説明します。 場所、位置、それに関連する評価の 3 つのコンテキストそれぞれについて説明します。

 [デバッグタスク](../../extensibility/debugger/debugging-tasks.md) プログラムの起動や式の評価など、さまざまなデバッグタスクへのリンクが含まれています。

## <a name="see-also"></a>関連項目
- [開始するには](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
