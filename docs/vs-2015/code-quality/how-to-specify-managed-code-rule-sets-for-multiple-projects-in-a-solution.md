---
title: '方法: ソリューション内の複数のプロジェクトに対してマネージコード規則セットを指定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.solution
ms.assetid: 92dc3250-a010-4396-b515-f03a0b30cd2a
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e5333f6133dd3fd56077c14d6e56cd6fdada4404
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656423"
---
# <a name="how-to-specify-managed-code-rule-sets-for-multiple-projects-in-a-solution"></a>方法: ソリューション内の複数のプロジェクトに対してマネージド コード規則セットを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

既定では、ソリューションのすべてのマネージプロジェクトに、Microsoft の最小推奨規則のコード分析 *規則セット*が割り当てられます。 ソリューションのプロパティ ダイアログ ボックスで、ソリューションのプロジェクトに割り当てられる規則セットを変更できます。

> [!NOTE]
> 既定では、プロジェクトのコード分析はビルド ステップとして実行されません。 コード分析をビルドステップとして有効にする方法については、「 [方法: マネージコードプロジェクトのコード分析を構成](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)する」を参照してください。

### <a name="to-specify-a-rule-set-for-multiple-projects-in-a-managed-code--solution"></a>マネージド コード ソリューション内の複数のプロジェクトに対して規則セットを指定するには

1. [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]、 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]または [!INCLUDE[vsPro](../includes/vspro-md.md)] ソリューションを開きます。

2. [ **分析** ] メニューの [ **ソリューションのコード分析の構成**] をクリックします。

3. 必要に応じて、[ **共通プロパティ**] を展開し、[ **コード分析の設定**] をクリックします。

4. 1 つ以上のプロジェクトに対して規則セットを指定できます。

    - 個々のプロジェクトに対して規則セットを指定するには、プロジェクト名をクリックします。

    - 複数のプロジェクトに対して規則セットを指定するには、Ctrl キーを押しながらプロジェクト名をクリックします。

    - ソリューションに含まれるすべてのプロジェクトを指定するには、Shift キーを押しながらプロジェクトの一覧内をクリックします。

5. プロジェクトの [ **ルールセット** ] フィールドをクリックし、適用するルールセットの名前をクリックします。
