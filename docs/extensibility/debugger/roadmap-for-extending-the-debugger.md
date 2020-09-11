---
title: デバッガーを拡張するためのロードマップ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], roadmap
- Debugging SDK, roadmap
ms.assetid: 1f4096a8-f7aa-4dfa-84e1-6d59263e70bb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9d97a7edd62540d12a0a60d15b3179ca0a623c26
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90011828"
---
# <a name="roadmap-for-extending-the-debugger"></a>デバッガーを拡張するためのロードマップ
このドキュメントでは、を使用してデバッガーを拡張するためのガイドとリファレンス情報を提供し [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグドキュメントには、サンプル、包括的なリファレンス、デバッガーをカスタマイズする一般的な方法を示すいくつかの代表的なシナリオが含まれています。

 コンパイラとその出力によって、製品のデバッグを設定するために必要なものが決まります。 コンパイラの場合:

- Windows ネイティブオペレーティングシステムを対象とし、を書き込み *ます。PDB* ファイルは、に統合されているネイティブコードデバッグエンジン (DE) を使用してプログラムをデバッグでき [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 DE または式エバリュエーターを実装する必要はありません。 式エバリュエーターは、C++ プログラミング言語の構文用に記述されています。

- Microsoft 中間言語 (MSIL) 出力を生成します。マネージコードデバッグエンジン DE を使用してプログラムをデバッグできます。これは、にも統合されてい [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 したがって、式エバリュエーターだけを実装する必要があります。 サンプル式エバリュエーターが用意されています。 詳細については、次のトピックを参照してください。

   [式の評価](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)

   [式の評価](../../extensibility/debugger/evaluating-expressions.md)

   [式の評価コンテキスト](../../extensibility/debugger/expression-evaluation-context.md)

   [中断モードでの式の評価](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

   [共通言語ランタイムの式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

- 独自のオペレーティングシステムまたはその他の実行時環境を対象とする場合は、独自の DE を作成する必要があります。 ATL COM を使用して単純な DE を作成するチュートリアルが用意されています。 詳細については、次のトピックを参照してください。

   [カスタムデバッグエンジンを作成する](../../extensibility/debugger/creating-a-custom-debug-engine.md)

   [チュートリアル: ATL COM を使用してデバッグエンジンをビルドする](/previous-versions/bb147024(v=vs.90))

   [ポートサプライヤーを実装する](../../extensibility/debugger/implementing-a-port-supplier.md)

   [サンプル](../../extensibility/debugger/visual-studio-debugging-samples.md)

## <a name="see-also"></a>関連項目
- [開始するには](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)