---
title: デバッガーを拡張するためのロードマップ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], roadmap
- Debugging SDK, roadmap
ms.assetid: 1f4096a8-f7aa-4dfa-84e1-6d59263e70bb
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 89a07bc5a5c4c8b7a6054b53610325c654355bc8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695961"
---
# <a name="roadmap-for-extending-the-debugger"></a>デバッガーを拡張するためのロードマップ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このドキュメントでは、を使用してデバッガーを拡張するためのガイドとリファレンス情報を提供し [!INCLUDE[vs_current_short](../../includes/vs-current-short-md.md)] [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] ます。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] デバッグドキュメントには、サンプル、包括的なリファレンス、デバッガーをカスタマイズする一般的な方法を示すいくつかの代表的なシナリオが含まれています。  
  
 コンパイラとその出力によって、製品にデバッグを実装するために必要なものが決まります。 コンパイラの場合:  
  
- Windows ネイティブオペレーティングシステムを対象とし、を書き込みます。PDB ファイルは、に統合されているネイティブコードデバッグエンジン (DE) を使用してプログラムをデバッグでき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 DE または式エバリュエーターを実装する必要はありません。 式エバリュエーターは、C++ プログラミング言語の構文用に記述されています。  
  
- Microsoft 中間言語 (MSIL) 出力を生成します。マネージコードデバッグエンジン DE を使用してプログラムをデバッグできます。これは、にも統合されてい [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 したがって、式エバリュエーターだけを実装する必要があります。 サンプル式エバリュエーターが用意されています。 詳細については、次のトピックを参照してください。  
  
     [式の評価](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)  
  
     [式の評価](../../extensibility/debugger/evaluating-expressions.md)  
  
     [式の評価のコンテキスト](../../extensibility/debugger/expression-evaluation-context.md)  
  
     [中断モードでの式の評価](../../extensibility/debugger/expression-evaluation-in-break-mode.md)  
  
     [共通言語ランタイム式エバリュエーターの書き込み](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)  
  
- 独自のオペレーティングシステムまたはその他の実行時環境を対象とする場合は、独自の DE を作成する必要があります。 ATL COM を使用して単純な DE を作成するチュートリアルが用意されています。 詳細については、次のトピックを参照してください。  
  
     [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
  
     [チュートリアル: ATL COM を使用したデバッグエンジンの構築](https://msdn.microsoft.com/9097b71e-1fe7-48f7-bc00-009e25940c24)  
  
     [ポートのサプライヤーの実装](../../extensibility/debugger/implementing-a-port-supplier.md)  
  
     [サンプル](../../extensibility/debugger/visual-studio-debugging-samples.md)  
  
## <a name="see-also"></a>参照  
 [はじめに](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
