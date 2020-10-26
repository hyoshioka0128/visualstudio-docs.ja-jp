---
title: '方法: マネージコードプロジェクトのコード分析を構成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.csvb
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
ms.assetid: 618f6ff3-db0e-46cb-b08d-dfa35e62c9e7
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1ac04a3d8834e3fc24f148fc36327d101e43720a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72658856"
---
# <a name="how-to-configure-code-analysis-for-a-managed-code-project"></a>方法: マネージド コード プロジェクトのコード分析を構成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、およびでは [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] [!INCLUDE[vsPro](../includes/vspro-md.md)] 、マネージコードプロジェクトに適用するコード分析*規則セット*の一覧から選択できます。 既定の規則セットは Microsoft 最小推奨規則です。 ソリューション内の 1 つのプロジェクトまたはすべてのプロジェクトに別の規則セットを適用することもできます。

> [!NOTE]
> ASP.NET Web アプリケーションのルールセットを構成する方法の詳細については、「 [方法: ASP.NET Web アプリケーションのコード分析を構成](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md)する」を参照してください。

### <a name="to-configure-a-rule-set-for-a-net-framework-project"></a>.NET Framework プロジェクトの規則セットを構成するには

1. **ソリューションエクスプローラー**で、プロジェクトをクリックします。

2. [**分析**] メニューの [ *ProjectName***のコード分析の構成**] をクリックします。

3. [ **構成** ] と [ **プラットフォーム** ] の一覧で、ビルド構成とターゲットプラットフォームをクリックします。

4. 選択した構成を使用してプロジェクトがビルドされるたびにコード分析を実行するには、[ **ビルド時にコード分析を有効にする (CODE_ANALYSIS 定数を定義する)** ] チェックボックスをオンにします。 [**分析**] メニューを開き、[ *ProjectName***でコード分析を実行**] をクリックして、手動でコード分析を実行することもできます。

5. 既定では、外部ツールによって自動的に生成されたコードからの警告はコード分析では報告されません。 生成されたコードからの警告を表示するには、[ **生成されたコードから結果** を表示しない] チェックボックスをオフにします。

    > [!NOTE]
    > コード分析のエラーおよび警告がフォームやテンプレートで表示される場合、このオプションを使用しても、生成されたコードからこのエラーおよび警告の出力は抑制されません。 フォームまたはテンプレートのソース コードは表示することも保持することもできます。

6. [ **この規則セットを実行** する] の一覧で、次のいずれかの操作を行います。

    - 使用する規則セットをクリックします。

    - **\<Browse...>** 一覧にない既存のカスタム規則セットを指定する場合にクリックします。

    - カスタム規則セットを定義します。

         詳細については、「 [カスタム規則セットの作成](../code-quality/creating-custom-code-analysis-rule-sets.md)」を参照してください。

## <a name="see-also"></a>参照
 [チュートリアル: カスタム規則セットの構成と使用](../code-quality/walkthrough-configuring-and-using-a-custom-rule-set.md)
