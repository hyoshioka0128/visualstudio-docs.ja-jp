---
title: コード分析を使用したマネージコードの品質の分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis,managed code
- managed code analyis
ms.assetid: 68510a55-da51-4381-81a5-0feba76b8b4f
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0d5f0646f26226e9895414db512681e0a7a71faa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671113"
---
# <a name="analyzing-managed-code-quality-by-using-code-analysis"></a>コード分析を使用したマネージド コードの品質の分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のコード分析ツールを使用すると、安全ではないデータ アクセス、使用法違反、デザイン上の問題など、コード内の潜在的な問題を検出できます。 コード分析の動作環境は、.NET Framework、ネイティブ (C と C++)、およびデータベース アプリケーションです。 マネージコードのコード分析を使用すると、特定のコーディングの問題を対象とするルール *セット* のルールが整理されます。

## <a name="common-tasks"></a>一般的なタスク

|一般的なタスク|関連する参照先|
|------------------|------------------------|
|**ハンズオンプラクティスをご利用ください。** 単純な .NET Framework アプリケーションで欠陥を修正することで、コード分析の基本について説明します。|-   [チュートリアル: マネージコードの分析によるコード障害の分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)|
|**プロジェクトのコード分析を構成します。** マネージコードの規則は、セキュリティや設計など、特定の領域を対象とする規則セットに分類されます。 Microsoft の標準の規則セットの 1 つを使用することも、独自のセットを作成することもできます。|-   [マネージコードのコード分析の概要](../code-quality/code-analysis-for-managed-code-overview.md)<br />-   [規則セットを使用したコード分析規則のグループ化](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)<br />-   [SuppressMessage 属性を使用して警告を抑制する](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md)|
|**コード分析の実行:** プロジェクト構成がビルドされるたびにコード分析を自動的に実行するように指定したり、プロジェクトでコード分析を手動で実行したりすることができます。|-   [方法: 自動コード分析を有効または無効にする](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)<br />-   [方法: コード分析を手動で実行する](../code-quality/how-to-run-code-analysis-manually-for-managed-code.md)|
|**コード分析結果の分析:** コード分析の警告とエラーは、[コード分析] ウィンドウに一覧表示されます。 警告またはエラーのタイトルを選択すると、警告に関する追加情報を表示し、規則を発動したソース コード行を表示および強調表示することができます。 警告 ID を選択すると、問題の解決方法に関する情報と例が含まれた、MSDN ライブラリの詳細情報を表示できます。|-   [方法: マネージコードの障害を表示する](../code-quality/how-to-view-managed-code-defects.md)<br />-   [マネージコードの警告のコード分析](../code-quality/code-analysis-for-managed-code-warnings.md)<br />-   [CheckId 別の警告](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)<br />-   [匿名メソッドとコード分析](../code-quality/anonymous-methods-and-code-analysis.md)|
|**コード分析を開発ライフサイクルと統合します。** のチェックインポリシー [!INCLUDE[esprscc](../includes/esprscc-md.md)] を使用すると、開発チームは、すべてのコードチェックインがコード分析標準の共通セットを満たしていることを確認できます。 コード分析規則違反の作業項目は、[エラー一覧] ウィンドウで簡単な手順により作成できます。|-   [チームプロジェクトチェックインポリシーによるコード品質の向上](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)<br />-   [方法: コードプロジェクト規則セットをチームプロジェクトのチェックインポリシーと同期させる](../code-quality/how-to-synchronize-code-project-rule-sets-with-team-project-check-in-policy.md)<br />-   [方法: マネージコードの障害に対する作業項目を作成する](../code-quality/how-to-create-a-work-item-for-a-managed-code-defect.md)|
