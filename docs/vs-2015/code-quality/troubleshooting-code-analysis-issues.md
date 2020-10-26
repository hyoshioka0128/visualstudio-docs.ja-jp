---
title: コード分析に関する問題のトラブルシューティング | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: troubleshooting
ms.assetid: 61c7e44d-2780-4df5-9bcb-49e40c1152fc
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6fd2735b7e601afb5a80dd027a8ae107cab58e4a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672432"
---
# <a name="troubleshooting-code-analysis-issues"></a>コード分析に関する問題のトラブルシューティング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、次の Visual Studio コード分析の問題についてのトラブルシューティング情報を示します。

- [Visual Studio 2010 の規則セットでの変更は、以前のバージョンの Visual Studio には反映されません。](#ChildRuleSetChangesInPreviousVersions)

## <a name="changes-in-a-visual-studio-2010-rule-set-are-not-reflected-in-previous-visual-studio-versions"></a><a name="ChildRuleSetChangesInPreviousVersions"></a>Visual Studio 2010 規則セットでの変更が以前のバージョンの Visual Studio に反映されない
 子規則セットを含む [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 規則セットを作成すると、子規則セットに対する変更が、旧バージョンの Visual Studio を使用するコンピューターで実行されるコード分析に適用されない場合があります。 この問題を解決するには、親規則セット、つまり子規則セットを含む規則セットを強制的に書き換える必要があります。

1. [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] で親規則セットを開きます。

2. 規則の追加、削除などの変更を加え、規則セットを保存します。

3. 規則セットを再度開き、変更を元に戻し、規則セットを再度保存します。

## <a name="see-also"></a>参照
 [アプリケーション品質の分析](../code-quality/analyzing-application-quality-by-using-code-analysis-tools.md)[ルールセットを使用してコード分析ルールをグループ化し、](../code-quality/using-rule-sets-to-group-code-analysis-rules.md) [マネージコード品質を分析](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)する
