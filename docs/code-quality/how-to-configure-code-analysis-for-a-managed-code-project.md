---
title: コード分析の構成
ms.date: 04/04/2018
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.propertypages.csvb
- vs.codeanalysis.propertypages.solution
- vs.codeanalysis.propertypages.asp
dev_langs:
- CSharp
- VB
- FSharp
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: c94742b452bfd665dc35c59ef831bca2cdacf1f5
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801049"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>方法: マネージコードのレガシ分析を構成する

Visual Studio では、マネージコードプロジェクトに適用するコード分析 [規則セット](../code-quality/rule-set-reference.md) の一覧から選択できます。 既定では、" **Microsoft の最小推奨規則** " 規則セットが選択されていますが、必要に応じて別の規則セットを適用することもできます。 規則セットは、ソリューション内の1つまたは複数のプロジェクトに適用できます。

> [!NOTE]
> この記事は、 [.NET Compiler Platform ベースのコードアナライザー](use-roslyn-analyzers.md)ではなく、レガシ分析に適用されます。

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>.NET Framework プロジェクトの規則セットを構成する

1. プロジェクトのプロパティページで [ **コード分析** ] タブを開きます。 この操作は次のいずれかの方法で行うことができます。

   - **ソリューションエクスプローラー**で、プロジェクトを選択します。 メニューバーで、[**分析**] [  >  **コード分析**  >  **の \<projectname> **構成] を選択します。

   - **ソリューションエクスプローラー**でプロジェクトを右クリックし、[**プロパティ**] をクリックして、[**コード分析**] タブを選択します。

2. [ **構成** ] と [ **プラットフォーム** ] の一覧で、ビルド構成とターゲットプラットフォームを選択します。

::: moniker range="vs-2017"

3. 選択した構成を使用してプロジェクトがビルドされるたびにコード分析を実行するには、[ **ビルド時にコード分析を有効にする**] を選択します。 [**分析**]  >  [**実行コード**分析]  >  ** \<projectname> [実行コード分析**] を選択して、手動でコード分析を実行することもできます。

::: moniker-end

::: moniker range=">=vs-2019"

3. 選択した構成を使用してプロジェクトがビルドされるたびにコード分析を実行するには、[**バイナリアナライザー** ] セクションの [**ビルドで実行**] を選択します。 レガシコード分析を手動で実行することもできます。詳細については、「 [方法: マネージコードに対してレガシコード分析を手動で実行する](how-to-run-legacy-code-analysis-manually-for-managed-code.md) 」を参照してください。

::: moniker-end

4. 生成されたコードからの警告を表示するには、[ **生成されたコードから結果** を表示しない] チェックボックスをオフにします。

    > [!NOTE]
    > コード分析のエラーおよび警告がフォームやテンプレートで表示される場合、このオプションを使用しても、生成されたコードからこのエラーおよび警告の出力は抑制されません。 フォームまたはテンプレートのソースコードを表示して管理することができ、上書きされることはありません。

::: moniker range="vs-2017"

5. [ **この規則セットを実行** する] の一覧で、次のいずれかの操作を行います。

::: moniker-end

::: moniker range=">=vs-2019"

5. [ **アクティブな規則** ] の一覧で、次のいずれかの操作を行います。

::: moniker-end

   - 使用する規則セットを選択します。

   - **\<Browse>** 一覧にない既存のカスタム規則セットを検索する場合に選択します。

   - [カスタム規則セット](../code-quality/how-to-create-a-custom-rule-set.md)を定義します。

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>ソリューション内の複数のプロジェクトに対して規則セットを指定する

既定では、ソリューションのすべてのマネージプロジェクトに、 *Microsoft の最小推奨規則* のコード分析規則セットが割り当てられます。 ソリューションの [ **プロパティ** ] ダイアログボックスで、ソリューションのプロジェクトに割り当てられている規則セットを変更できます。

1. Visual Studio でソリューションを開きます。

2. [ **分析** ] メニューの [ **ソリューションのコード分析の構成**] をクリックします。

3. 必要に応じて、[ **共通プロパティ**] を展開し、[ **コード分析の設定**] を選択します。

4. 1つ以上のプロジェクトに対して規則セットを指定できます。

    - 個々のプロジェクトに対して規則セットを指定するには、プロジェクト名を選択します。

    - 複数のプロジェクトに対して規則セットを指定するには、 **Ctrl** とプロジェクト名を選択します。

    - ソリューション内のすべてのプロジェクトを指定するには、[ **Shift** ] と [プロジェクト] リストを選択します。

5. プロジェクトの [ **ルールセット** ] フィールドを選択し、適用するルールセットの名前を選択します。

## <a name="see-also"></a>関連項目

- [コード分析規則セットの参照](../code-quality/rule-set-reference.md)
