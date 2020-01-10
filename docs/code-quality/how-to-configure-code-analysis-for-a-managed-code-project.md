---
title: コード分析を構成します。
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
ms.openlocfilehash: fe144e8de67264c9d89f6a240ef815afac9a4655
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587564"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>方法: マネージコードのレガシ分析を構成する

Visual Studio では、マネージコードプロジェクトに適用するコード分析[規則セット](../code-quality/rule-set-reference.md)の一覧から選択できます。 既定で、 **Microsoft 最小推奨規則**規則セットを選択するが必要な場合は、設定、別の規則を適用できます。 規則セットは、ソリューション内の 1 つまたは複数のプロジェクトに適用できます。

> [!NOTE]
> この記事は、 [.NET Compiler Platform ベースのコードアナライザー](use-roslyn-analyzers.md)ではなく、レガシ分析に適用されます。

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>.NET Framework プロジェクトの規則セットを構成する

1. 開く、**コード分析**プロジェクトのプロパティ ページのタブ。 この操作は次のいずれかの方法で行うことができます。

   - **ソリューション エクスプ ローラー**プロジェクトを選択します。 メニュー バーで選択**分析** > **コード分析を構成する** > **の\<projectname >** します。

   - プロジェクトを右クリックして**ソリューション エクスプ ローラー**選択**プロパティ**を選び、**コード分析**タブ。

2. **構成**と**プラットフォーム**一覧で、ビルド構成とターゲット プラットフォームを選択します。

::: moniker range="vs-2017"

3. 選択した構成を使用してプロジェクトがビルドされるたびにコード分析を実行するには、 **[ビルド時にコード分析を有効にする]** を選択します。 手動では選択してもコード分析を実行することができます**分析** > **コード分析を実行** > **でコード分析を実行\<projectname >** .

::: moniker-end

::: moniker range=">=vs-2019"

3. 選択した構成を使用してプロジェクトがビルドされるたびにコード分析を実行するには、 **[バイナリアナライザー]** セクションの **[ビルドで実行]** を選択します。 手動では選択してもコード分析を実行することができます**分析** > **コード分析を実行** > **でコード分析を実行\<projectname >** .

::: moniker-end

4. 生成されたコードからの警告を表示するには、オフ、**結果生成されたコードを表示しない**チェック ボックスをオンします。

    > [!NOTE]
    > コード分析のエラーおよび警告がフォームやテンプレートで表示される場合、このオプションを使用しても、生成されたコードからこのエラーおよび警告の出力は抑制されません。 フォームまたはテンプレートのソースコードを表示して管理することができ、上書きされることはありません。

::: moniker range="vs-2017"

5. **この規則セットを実行**ボックスの一覧で、次のいずれかの操作を行います。

::: moniker-end

::: moniker range=">=vs-2019"

5. **[アクティブな規則]** の一覧で、次のいずれかの操作を行います。

::: moniker-end

   - 使用する規則セットを選択します。

   - 一覧に含まれていない既存のカスタムルールセットを検索するには、[ **\<> 参照**] を選択します。

   - 定義、[カスタム規則セット](../code-quality/how-to-create-a-custom-rule-set.md)します。

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>ソリューションに複数のプロジェクトに対して規則セットを指定します。

既定では、ソリューションのすべてのマネージ プロジェクトが割り当てられている、 *Microsoft 最小推奨規則*コード分析規則セット。 ソリューションのプロジェクトに割り当てられている規則セットを変更することができます、**プロパティ**ソリューションのダイアログ ボックス。

1. Visual Studio でソリューションを開きます。

2. **分析**メニューの **ソリューションのコード分析を構成する**します。

3. 必要に応じて、展開**共通プロパティ**、し、**コード分析設定**します。

4. 1 つまたは複数のプロジェクトに対して規則セットを指定できます。

    - 個々 のプロジェクトに対して規則セットを指定するには、プロジェクト名を選択します。

    - 押しながら複数のプロジェクトに対して規則セットを指定する**Ctrl**プロジェクト名を選択します。

    - 押しながら、ソリューション内のすべてのプロジェクトを指定する**Shift**プロジェクトの一覧内をクリックします。

5. 選択、**ルール セットの**ルールの名前では、適用する設定、プロジェクトのフィールドと順に選択します。

## <a name="see-also"></a>関連項目

- [コード分析規則セットの参照](../code-quality/rule-set-reference.md)
