---
title: 規則セットを使用したコード分析規則のグループ化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.rulesets.learnmore
helpviewer_keywords:
- code analysis, rule sets
ms.assetid: ed0f3a2a-1516-42e2-92de-b8986dc75d42
caps.latest.revision: 38
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 30bd2e53531d9abc7d27adba05c3b724c88d61c3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72603476"
---
# <a name="using-rule-sets-to-group-code-analysis-rules"></a>規則セットを使用したコード分析規則のグループ化
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

、、またはでコード分析を構成する場合は、 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] [!INCLUDE[vsPro](../includes/vspro-md.md)] Microsoft の組み込みの *規則セット*の一覧から選択できます。 規則セットは、対象の問題および特定の条件を識別するコード分析規則の論理的なグループです。 たとえば、一般に公開されている API 用のコードをスキャンするように設計された規則セットを適用したり、最小推奨規則のみが含まれた規則セットを適用したりできます。 また、すべての規則が含まれた規則セットを適用することもできます。

 ルールセットをカスタマイズするには、ルールを追加または削除するか、[ **エラー一覧** ] ウィンドウに警告またはエラーとして表示されるようにルールを変更します。 カスタマイズした規則セットで、特定の開発環境の要件を満たすことができます。 規則セットをカスタマイズする場合、処理に役立つ検索ツールおよびフィルター処理ツールが規則セットのページに表示されます。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連するコンテンツ|
|----------|---------------------|
|**ハンズオンプラクティスをご利用ください。** コード分析ツールを使用して、簡単な .NET Framework アプリケーションの問題を検出して修正するためのカスタム規則セットを指定します。|-   [チュートリアル: カスタム規則セットの構成と使用](../code-quality/walkthrough-configuring-and-using-a-custom-rule-set.md)|
|**プロジェクトのコード分析を構成します。** プロジェクト、Web サイト、またはソリューションに対して既存の規則セットを選択します。|-   [方法: マネージコードプロジェクトのコード分析を構成する](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)<br />-   [規則セットを使用して実行する C++ 規則を指定する](../code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run.md)<br />-   [方法: ASP.NET Web アプリケーションのコード分析を構成する](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md)<br />-   [方法: ソリューション内の複数のプロジェクトに対して規則セットを指定する](../code-quality/how-to-specify-managed-code-rule-sets-for-multiple-projects-in-a-solution.md)|
|**規則セットをカスタマイズします。** プロジェクトに適用する規則を指定します。|-   [カスタム規則セットの作成](../code-quality/creating-custom-code-analysis-rule-sets.md)|
|**組み込みの規則セットについて理解する:** 組み込みの規則セットを構成するコード分析規則を表示します。|-   [コード分析規則セットの参照](../code-quality/code-analysis-rule-set-reference.md)|
|**コード分析を Team Foundation Server と統合します。** [!INCLUDE[esprtfs](../includes/esprtfs-md.md)] チェックインポリシーを使用すると、開発チームは、すべてのコードチェックインがコード分析標準の共通セットを満たすようにすることができます。|-   [方法: コードプロジェクト規則セットをチームプロジェクトのチェックインポリシーと同期させる](../code-quality/how-to-synchronize-code-project-rule-sets-with-team-project-check-in-policy.md)|
