---
title: Analyzing Application Quality by Using Code Analysis Tools | Microsoft Docs
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

In This Section [Analyzing Managed Code Quality](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md) Visual Studio code analysis for managed code provides information about managed assemblies, such as violations of the programming and design rules set forth in the Microsoft .NET Framework Design Guidelines. 警告メッセージは、プログラミングやデザイン上の問題を識別し、可能であれば問題の解決方法を提供します。

 [Analyzing C/C++ Code Quality by Using Code Analysis](../code-quality/analyzing-c-cpp-code-quality-by-using-code-analysis.md) The C/C++ Code Analysis tool provides information to developers about possible defects in their C/C++ source code. このツールによってレポートされる一般的なコーディング エラーとしては、バッファー オーバーラン、初期化されていないメモリ、null ポインターの逆参照、メモリ リーク、リソース リークなどがあります。

 [Using Rule Sets to Group Code Analysis Rules](../code-quality/using-rule-sets-to-group-code-analysis-rules.md) Select and create *rule sets* to apply to your project.

 [Code Analysis Application Errors](../code-quality/code-analysis-application-errors.md) Fix errors in the code analysis functionality.

 [Enhancing Code Quality with Team Project Check-in Policies](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md) When you use Team Foundation Version Control (TFVC), you can create check-in policies for your team projects that enforce practices that lead to better code and more efficient group development. チェックイン ポリシーとは、チーム プロジェクト レベルで設定され、コードをチェックインする前に開発者のコンピューターに適用される規則です。

### <a name="code-analysis-for-drivers"></a>ドライバーのコード分析
 コード分析ツールでドライバーのソース コードを系統的に分析することにより、ドライバーの安定性と信頼性を向上させることができます。

 [Analyzing Driver Quality by Using Code Analysis Tools](/windows-hardware/drivers/devtest/tools-for-verifying-drivers) Code Analysis for Drivers is a compile-time static verification tool that detects basic coding errors in C and C++ programs and includes a specialized module that is designed to detect errors in (primarily) kernel-mode driver code. 静的ドライバー検証ツール (SDV) は、Windows カーネル モードのドライバーのソース コードを系統的に分析する静的検証ツールです。 SDV は、ドライバーが Windows オペレーティング システムのカーネルと適切にやり取りしているかどうかを判定します。

 [Code Analysis for Drivers Warnings](https://go.microsoft.com/fwlink/?LinkId=225920) Describes the warnings that the Code Analysis for Drivers reports when it detects a possible error in driver code.

## <a name="related-tasks"></a>関連タスク
 [Measuring Complexity and Maintainability of Managed Code](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md) Insert description here.

 [Unit Test Your Code](../test/unit-test-your-code.md) Insert description here.
