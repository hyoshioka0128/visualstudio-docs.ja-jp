---
title: デバッガコンポーネント |マイクロソフトドキュメント
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
ms.openlocfilehash: 03c400fd03c5ee0f2629e9f436b65f53f8f2ac8b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739017"
---
# <a name="debugger-components"></a>デバッガー コンポーネント
デバッガー[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は VSPackage として実装され、デバッグ セッション全体を管理します。 デバッグ セッションは、次の要素で構成されます。

- **デバッグ パッケージ:** デバッガー[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、デバッグ対象に関係なく、同じユーザー インターフェイスを提供します。

- **セッション デバッグ マネージャー (SDM):** さまざまなデバッグ エンジンを管理するための[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]一貫したプログラム インターフェイスをデバッガーに提供します。 によって[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]実装されます。

- **プロセス デバッグ マネージャー (PDM):** の実行中のすべてのインスタンス[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]について、デバッグ可能なすべてのプログラムの一覧を管理します。 によって[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]実装されます。

- **デバッグ エンジン (DE):** デバッグ中のプログラムの監視、実行中のプログラムの状態を SDM および PDM に通信する、および式エバリュエーターとシンボル プロバイダーと対話して、プログラムのメモリと変数の状態をリアルタイムで分析する責任があります。 (サポートする言語の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]場合) と、独自のランタイムをサポートするサードパーティ ベンダによって実装されます。

- **式エバリュエーター (EE):** 特定の時点でプログラムが停止したときにユーザーが提供する変数と式を動的に評価するサポートを提供します。 (サポートする言語の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]場合) と、独自の言語をサポートするサードパーティ ベンダによって実装されます。

- **シンボルプロバイダー (SP):** シンボル ハンドラーとも呼ばれ、プログラムのデバッグ シンボルをプログラムの実行中のインスタンスにマップして、意味のある情報 (ソース コード レベルのデバッグや式の評価など) を提供できるようにします。 (共通言語ランタイム [CLR] シンボルとプログラム DataBase [PDB] シンボル ファイル形式) と、独自のデバッグ情報を格納する独自の方法を持つサード パーティ ベンダーによって[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]実装されます。

  次の図は、Visual Studio デバッガーのこれらの要素間の関係を示しています。

  ![デバッグ コンポーネントの概要](../../extensibility/debugger/media/dbugcompovrview.gif "ドバグコンポヴルビュー")

## <a name="in-this-section"></a>このセクションの内容
 [デバッグ パッケージ](../../extensibility/debugger/debug-package.md)シェルで実行され、すべての UI[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を処理するデバッグ パッケージについて説明します。

 [プロセス デバッグ マネージャー](../../extensibility/debugger/process-debug-manager.md)デバッグ可能なプロセスのマネージャーである PDM の機能の概要を示します。

 [セッション デバッグ マネージャー](../../extensibility/debugger/session-debug-manager.md)デバッグ セッションの統一されたビューを IDE に提供する SDM を定義します。 SDM は DE を管理します。

 [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)DE が提供するデバッグ サービスについて説明します。

 [運用モード](../../extensibility/debugger/operational-modes.md)IDE が動作できる 3 つのモードの概要を示します。 また、移行メカニズムについても説明します。

 [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)実行時の EE の目的について説明します。

 [シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md)実装時に、シンボル プロバイダーが変数と式を評価する方法について説明します。

 [型ビジュアライザーとカスタム ビューアー](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)型ビジュアライザーとカスタム ビューアーとは何か、および式エバリュエーターが両方をサポートする役割について説明します。

## <a name="related-sections"></a>関連項目
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)デバッグアーキテクチャの主要な概念について説明します。

 [デバッガーのコンテキスト](../../extensibility/debugger/debugger-contexts.md)コード、ドキュメント、および式の評価コンテキスト内で DE が同時に動作する方法について説明します。 3 つのコンテキストのそれぞれについて、そのコンテキストに関連する場所、位置、または評価について説明します。

 [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)プログラムの起動や式の評価など、さまざまなデバッグ タスクへのリンクが含まれています。

## <a name="see-also"></a>関連項目
- [はじめに](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
