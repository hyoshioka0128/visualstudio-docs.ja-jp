---
title: コード分析の構成
ms.date: 04/04/2018
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.csvb
- vs.codeanalysis.propertypages.solution
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 98db7cda02495d207d6e9387341173ea2efe22ca
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431353"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>方法: マネージ コードのレガシ分析を構成する

Visual Studio では、コード分析[規則セット](../code-quality/rule-set-reference.md)の一覧から、マネージ コード プロジェクトに適用するように選択できます。 既定では **、[Microsoft 最小推奨規則]** 規則セットが選択されていますが、必要に応じて別の規則セットを適用できます。 ルール セットは、ソリューション内の 1 つまたは複数のプロジェクトに適用できます。

> [!NOTE]
> この資料は、.NET コンパイラ[プラットフォーム ベースのコード アナライザ](use-roslyn-analyzers.md)ーではなく、レガシ分析に適用されます。

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>.NET Framework プロジェクトのルール セットを構成する

1. プロジェクトのプロパティ ページの [**コード分析**] タブを開きます。 この操作は次のいずれかの方法で行うことができます。

   - **ソリューション エクスプローラ**で、プロジェクトを選択します。 メニュー バーで、[ > **\<プロジェクト名の** > **コード分析の分析]** を選択>。 **Analyze**

   - **ソリューション エクスプローラー**でプロジェクトを右クリックし、[**プロパティ ]** をクリックし、[**コード分析**] タブを選択します。

2. **[構成**] および **[プラットフォーム**] の一覧で、ビルド構成とターゲット プラットフォームを選択します。

::: moniker range="vs-2017"

3. 選択した構成を使用してプロジェクトをビルドするたびにコード分析を実行するには、[**ビルド時にコード分析を有効にする**] チェック ボックスをオンにします。 プロジェクト名>で [**コード分析の実行コード分析の実行** > ]**を選択** > して、コード**分析を手動で\<** 実行することもできます。

::: moniker-end

::: moniker range=">=vs-2019"

3. 選択した構成を使用してプロジェクトをビルドするたびにコード分析を実行するには、[**バイナリ アナライザー]** セクションの [**ビルド時に実行**] を選択します。 また、レガシ コード分析[を](how-to-run-legacy-code-analysis-manually-for-managed-code.md)手動で実行することもできます。

::: moniker-end

4. 生成されたコードからの警告を表示するには、[**生成されたコードから結果を表示しない**] チェック ボックスをオフにします。

    > [!NOTE]
    > コード分析のエラーおよび警告がフォームやテンプレートで表示される場合、このオプションを使用しても、生成されたコードからこのエラーおよび警告の出力は抑制されません。 フォームまたはテンプレートのソース コードを表示および管理でき、上書きされることはありません。

::: moniker range="vs-2017"

5. [**このルール セットを実行する]** ボックスの一覧で、次のいずれかの操作を行います。

::: moniker-end

::: moniker range=">=vs-2019"

5. [**アクティブなルール**] ボックスの一覧で、次のいずれかの操作を行います。

::: moniker-end

   - 使用するルール セットを選択します。

   - [**\<参照>]** を選択して、リストにない既存のカスタムルールセットを検索します。

   - [カスタムルールセット](../code-quality/how-to-create-a-custom-rule-set.md)を定義する:

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>ソリューション内の複数のプロジェクトのルール セットを指定する

既定では、ソリューションのすべてのマネージ プロジェクトに *、Microsoft 最小推奨規則*コード分析規則セットが割り当てられます。 ソリューションの **[プロパティ]** ダイアログ ボックスで、ソリューションのプロジェクトに割り当てられているルール セットを変更できます。

1. Visual Studio でソリューションを開きます。

2. [**分析**] メニューの [**ソリューションのコード分析の構成**] をクリックします。

3. 必要に応じて、[**共通プロパティ]** を展開し、[**コード分析の設定]** を選択します。

4. 1 つまたは複数のプロジェクトに対してルール セットを指定できます。

    - 個々のプロジェクトの規則セットを指定するには、プロジェクト名を選択します。

    - 複数のプロジェクトのルール セットを指定するには **、Ctrl キー**を押しながらプロジェクト名を選択します。

    - ソリューション内のすべてのプロジェクトを指定するには **、Shift キー**を押しながらプロジェクト リスト内をクリックします。

5. プロジェクトの **[ルール セット**] フィールドを選択し、適用するルール セットの名前を選択します。

## <a name="see-also"></a>関連項目

- [コード分析規則セットの参照](../code-quality/rule-set-reference.md)
