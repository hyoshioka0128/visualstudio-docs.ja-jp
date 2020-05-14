---
title: デバッガの拡張に関するロードマップ |マイクロソフトドキュメント
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
ms.openlocfilehash: e809eeb6a1a5d2c24368932713d69c7199b5af38
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713147"
---
# <a name="roadmap-for-extending-the-debugger"></a>デバッガーを拡張するためのロードマップ
このドキュメントでは、 を使用して[!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)]デバッガーを拡張するためのガイドと[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]リファレンス情報を提供します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグ ドキュメントには、サンプル、包括的なリファレンス、およびデバッガーをカスタマイズする一般的な方法を示すいくつかの代表的なシナリオが含まれています。

 コンパイラとその出力によって、製品のデバッグをセットアップするために必要なものが決まります。 コンパイラの場合:

- Windows ネイティブ オペレーティング システムを対象とし、 *.PDB*ファイルには、ネイティブ コード デバッグ エンジン (DE) に統合された[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プログラムをデバッグできます。 DE または式エバリュエーターを実装する必要はありません。 式エバリュエーターは、C++ プログラミング言語の構文用に記述されています。

- Microsoft 中間言語 (MSIL) 出力を生成し、マネージ コードデバッグ エンジン DE を使用して[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プログラムをデバッグできます。 したがって、式エバリュエーターを実装するだけで済みます。 サンプル式エバリュエーターが提供されています。 詳細については、次のトピックを参照してください。

   [式評価](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)

   [式の評価](../../extensibility/debugger/evaluating-expressions.md)

   [式評価コンテキスト](../../extensibility/debugger/expression-evaluation-context.md)

   [ブレークモードでの式評価](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

   [共通言語ランタイム式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

- 独自のオペレーティング システムまたは他のランタイム環境を対象とし、独自の DE を記述する必要があります。 ATL COM を使用して簡単な DE を作成するチュートリアルが提供されています。 詳細については、次のトピックを参照してください。

   [カスタム デバッグ エンジンを作成する](../../extensibility/debugger/creating-a-custom-debug-engine.md)

   [チュートリアル: ATL COM を使用してデバッグ エンジンをビルドします。](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)

   [ポート サプライヤーの実装](../../extensibility/debugger/implementing-a-port-supplier.md)

   [サンプル](../../extensibility/debugger/visual-studio-debugging-samples.md)

## <a name="see-also"></a>関連項目
- [はじめに](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
