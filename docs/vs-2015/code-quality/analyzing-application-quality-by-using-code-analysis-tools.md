---
title: コード分析ツールを使用したアプリケーション品質の分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.analysisresults
helpviewer_keywords:
- application quality, analyzing
- code analysis
- team-based development, analyzing application quality
ms.assetid: 21680516-ddb5-446d-90d4-19d94f6ec699
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8b85bbad909a05bacab361a49cc7e029482ad606
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74291205"
---
# <a name="analyzing-application-quality-by-using-code-analysis-tools"></a>コード分析ツールを使用したアプリケーション品質の分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このセクションの「マネージコード[品質の分析](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)」では、「マネージコードの Visual Studio Code analysis」では、マネージアセンブリに関する情報を提供しています。たとえば、Microsoft .NET Framework デザインガイドラインに規定されているプログラミング規則やデザイン規則に違反しています。 警告メッセージは、プログラミングやデザイン上の問題を識別し、可能であれば問題の解決方法を提供します。

 [コード分析をC++使用した c/コード品質](../code-quality/analyzing-c-cpp-code-quality-by-using-code-analysis.md)の分析C++ c/コード分析ツールは、c/C++ソースコードで発生する可能性のある欠陥に関する情報を開発者に提供します。 このツールによってレポートされる一般的なコーディング エラーとしては、バッファー オーバーラン、初期化されていないメモリ、null ポインターの逆参照、メモリ リーク、リソース リークなどがあります。

 [規則セットを使用したコード分析規則のグループ化](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)プロジェクトに適用する*規則セット*を選択して作成します。

 [コード分析アプリケーションエラー](../code-quality/code-analysis-application-errors.md)コード分析機能のエラーを修正します。

 [チームプロジェクトチェックインポリシーによるコード品質の向上](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)Team Foundation バージョン管理 (TFVC) を使用すると、チームプロジェクトのチェックインポリシーを作成して、コードの向上とグループ開発の効率化を実現するプラクティスを適用することができます。 チェックイン ポリシーとは、チーム プロジェクト レベルで設定され、コードをチェックインする前に開発者のコンピューターに適用される規則です。

### <a name="code-analysis-for-drivers"></a>ドライバーのコード分析
 コード分析ツールでドライバーのソース コードを系統的に分析することにより、ドライバーの安定性と信頼性を向上させることができます。

 [コード分析ツールを使用したドライバー品質の分析](/windows-hardware/drivers/devtest/tools-for-verifying-drivers)ドライバーのコード分析は、C およびC++プログラムの基本的なコーディングエラーを検出するコンパイル時の静的検証ツールであり、(主にカーネルモードのドライバーコード) のエラーを検出するように設計された特殊なモジュールが含まれています。 静的ドライバー検証ツール (SDV) は、Windows カーネル モードのドライバーのソース コードを系統的に分析する静的検証ツールです。 SDV は、ドライバーが Windows オペレーティング システムのカーネルと適切にやり取りしているかどうかを判定します。

 [ドライバーの警告のコード分析](https://go.microsoft.com/fwlink/?LinkId=225920)ドライバーのコード分析によってドライバーコードでエラーが検出された場合に報告される警告について説明します。

## <a name="related-tasks"></a>関連タスク
 [マネージコードの複雑さと保守性の測定](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)ここに説明を挿入します。

 [コードの単体テスト](../test/unit-test-your-code.md)ここに説明を挿入します。
