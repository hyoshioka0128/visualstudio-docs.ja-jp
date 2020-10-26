---
title: '方法: ASP.NET Web アプリケーションのコード分析を構成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.asp
ms.assetid: b3000b31-fd9d-489e-81a2-a4bee49453ba
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 423264362118343d573b417cd055d2d722df995e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657462"
---
# <a name="how-to-configure-code-analysis-for-an-aspnet-web-application"></a>方法: ASP.NET Web アプリケーション用にコード分析を構成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsPreShort](../includes/vspreshort-md.md)]およびで [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)] は、Web アプリケーションに適用するコード分析*規則セット*の一覧から選択でき [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ます。 既定の規則セットは、Microsoft Mininimum 推奨規則です。 Web サイトに適用する別の規則セットを選択できます。

### <a name="to-configure-a-rule-set-for-an-aspnet-page-framework-project"></a>ASP.NET ページ フレームワーク プロジェクトの規則セットを構成するには

1. **ソリューションエクスプローラー**で Web サイトを選択します。

2. [ **分析** ] メニューの [ **Web サイトのコード分析の構成**] をクリックします。

3. ソリューションを選択し、ソリューションに複数のプロジェクトがある場合は、[ **構成** ] と [ **プラットフォーム** ] の一覧から、ビルド構成とターゲットオペレーティングシステムを選択します。

4. ソリューション内の各プロジェクトについて、[ **ルールセット** ] 列をクリックし、実行するルールセットの名前をクリックします。

5. 既定では、コード分析はソリューション内のすべてのプロジェクトで実行されます。 特定のプロジェクトのコード分析を無効または有効にするには、次の手順を実行します。

    1. プロジェクト名を右クリックし、[プロパティ] をクリックします。

    2. [ **コード分析を有効にする** ] チェックボックスをオンまたはオフにします。 [**分析**] メニューから [ **Web サイトでコード分析を実行**] を選択して、手動でコード分析を実行することもできます。

6. [ **この規則セットを実行** ] ドロップダウンリストで、次の手順に従います。

    - 使用する規則セットを選択します。

    - **\<Browse>** 一覧にない既存のカスタム規則セットを指定する場合に選択します。

    - カスタム規則セットを定義します。 詳細については、「 [カスタム規則セットの作成](../code-quality/creating-custom-code-analysis-rule-sets.md)」を参照してください。
