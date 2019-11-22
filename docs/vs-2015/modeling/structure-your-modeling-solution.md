---
title: Structure your modeling solution | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 2ba70ba4-2cea-4e01-93c2-055903d59470
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 83606b56e6509f1db77b590ec44d991ef97cf82e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298173"
---
# <a name="structure-your-modeling-solution"></a>モデリング ソリューションの構築

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

開発プロジェクトでモデルを効果的に使用するため、チーム メンバーは、プロジェクトのさまざまな部分のモデルを同時に作業する必要があります。 このトピックでは、アプリケーションを、レイヤー図全体の各レイヤーに対応する複数の部分に分割するスキームを提案します。

プロジェクトやサブプロジェクトを迅速に開始するため、選択したプロジェクト構造に準拠したプロジェクト テンプレートを用意すると便利です。 ここでは、このようなテンプレートを作成して使用する方法について説明します。

このトピックでは、複数のチーム メンバーと、複数のチームを必要とするほどの大規模なプロジェクトでの作業を想定しています。 プロジェクトのコードとモデルは、[!INCLUDE[esprtfs](../includes/esprtfs-md.md)] などのソース管理システムに格納されます。 少なくとも数人のチーム メンバーが Visual Studio を使用してモデルを開発しているときに、他のチーム メンバーは他のバージョンの Visual Studio を使って、モデルを表示できます。

To see which versions of Visual Studio support each tool and modeling feature, see [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="solution-structure"></a>ソリューション構造

中規模または大規模プロジェクトでは、チームの構造はアプリケーションの構造に基づいています。 各チームが、Visual Studio ソリューションを使用します。

#### <a name="to-divide-an-application-into-layers"></a>1 つのアプリケーションを複数のレイヤーに分割するには

1. Web アプリケーション、サービス アプリケーション、デスクトップ アプリケーションなど、アプリケーションの構造に基づいて、ソリューションの構造を決定します。 A variety of common architectures is discussed in [Application Archetypes in the Microsoft Application Architecture Guide](https://go.microsoft.com/fwlink/?LinkId=196681).

2. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションを作成します。このソリューションを「アーキテクチャ ソリューション」と呼びます。 このソリューションは、システムの全体設計の作成に使われます。 このソリューションにはモデルは含まれますが、コードは含まれません。

    このソリューションにレイヤー図を追加します。 レイヤー図で、作成するアプリケーション用に選択した構造を描画します。 たとえば、この図には、プレゼンテーション、ロジック、データの各レイヤーと、そのレイヤー間の依存関係が示されることがあります。

    You can create the layer diagram and a new Visual Studio solution at the same time by using the **New UML or Layer Diagram** command on the **Architecture** menu.

3. 重要なビジネス概念を表すアーキテクチャ モデル UML 図や、すべてのレイヤーのデザインで参照されるユース ケースに追加します。

4. アーキテクチャ レイヤー図で、レイヤーごとに個別の Visual Studio ソリューションを作成します。

    これらのソリューションを使って、レイヤーのコードを開発します。

5. レイヤーのデザインと、すべてのレイヤーに共通する概念を表す UML モデルを作成します。 すべてのモデルがアーキテクチャ ソリューションから確認できるように、また関連モデルが各レイヤーから確認できるように、モデルを配置します。

    これは、次の手順のいずれかを使用して実現できます。 最初の方法は、レイヤーごとに個別のモデリング プロジェクトを作成する方法、2 つ目の方法は、レイヤー間で共有されるモデリング プロジェクトを 1 つ作成する方法です。

###### <a name="to-use-a-separate-modeling-project-for-each-layer"></a>レイヤーごとに個別のモデリング プロジェクトを使用するには

1. 各レイヤー ソリューションでモデリング プロジェクトを作成します。

    このモデルには、要件とそのレイヤーのデザインを記述する UML 図が含まれます。 また、入れ子になったレイヤーを表すレイヤー図が含まれることもあります。

    これで、レイヤーごとのモデルと、アプリケーション アーキテクチャ用のモデルが準備できました。 各モデルは、独自のソリューションに含まれます。 これにより、チーム メンバーが同時に、複数のレイヤー上で作業できます。

2. アーキテクチャ ソリューションに、各レイヤー ソリューションのモデリング プロジェクトを追加します。 そのためには、アーキテクチャ ソリューションを開きます。 In Solution Explorer, right-click the solution node, point to Add, and then click **Existing Project**. 1 つのレイヤー ソリューションのモデリング プロジェクト (.modelproj) に移動します。

    各モデルは 2 つのソリューション ("ホーム" ソリューションとアーキテクチャ ソリューション) に表示されるようになりました。

3. 各レイヤーのモデリング プロジェクトに、レイヤー図を追加します。 アーキテクチャ レイヤー図のコピーを使って作業を開始します。 レイヤー図と依存関係がない部分は削除できます。

    このレイヤーの詳細な構造を表すレイヤー図を追加することもできます。

    これらの図は、このレイヤーで開発されたコードの検証に使用されます。

4. アーキテクチャ ソリューションでは、Visual Studio を使って、すべてのレイヤーの要件と設計モデルを編集します。

    各レイヤー ソリューションでは、モデルを参照しながら、そのレイヤーのコードを開発します。 開発が終了し、同じコンピューターを使ってモデルを更新する必要がなくなったら、モデルの作成を実行できないバージョンの Visual Studio を使って、モデルの読み取りとコードの開発を実行できます。 また、これらのバージョンで、モデルからコードを生成することもできます。

    この方法を使用すると、同時にレイヤー モデルを編集する複数の開発者によって、干渉が発生することはありません。

    ただし、モデルは個別に作成されるため、共通の概念を参照することは難しくなります。 各モデルには、他のレイヤーやアーキテクチャと依存関係にある要素の独自コピーが存在する必要があります。 各レイヤーのレイヤー図は、アーキテクチャ レイヤー図と同期を維持する必要があります。 これを実現するツールを開発することはできますが、これらの要素の変更時に同期を維持するのは困難です。

###### <a name="to-use-a-separate-package-for-each-layer"></a>レイヤーごとに個別のパッケージを使用するには

1. 各レイヤーのソリューションで、アーキテクチャ モデリング プロジェクトを追加します。 In Solution Explorer, right-click the solution node, point to **Add**, and then click **Existing Project**. これで 1 つのモデリング プロジェクトに、すべてのソリューション (アーキテクチャ プロジェクトと各レイヤーの開発プロジェクト) からアクセスできるようになりました。

2. 共有 UML モデルで、各レイヤーのパッケージを作成します。ソリューション エクスプローラーで、モデリング プロジェクトを選択します。 In UML Model Explorer, right-click the model root node, point to **Add**, and then click **Package**.

    各モデルには、要件と、対応するレイヤーのデザインを記述する UML 図が入ります。

3. 必要に応じて、各レイヤーの内部構造を表すローカル レイヤー図を追加します。

    この方法を使用すると、各レイヤーの設計要素から、レイヤーの設定要素と、そのレイヤーが依存している共通アーキテクチャを直接参照することができます。

    複数のパッケージに対する同時作業では競合が発生することがありますが、パッケージは個別ファイルに保存されるため、競合を非常に簡単に管理できます。 依存パッケージから参照されている要素を削除した場合には、大きな問題が発生します。 For more information, see [Manage models and diagrams under version control](../modeling/manage-models-and-diagrams-under-version-control.md).

## <a name="creating-architecture-templates"></a>アーキテクチャ テンプレートの作成

実際は、すべての Visual Studio ソリューションを同時に作成することはありませんが、プロジェクトが進行するにつれて、ソリューションが追加されます。 将来のプロジェクトで、同じソリューションの構造が使われる可能性もあります。  新しいソリューションを短時間で作成しやすくするため、ソリューションまたはプロジェクトのテンプレートを作成できます。 簡単に他のコンピューターに配布してインストールできるようにするため、Visual Studio Integration Extension (VSIX) でテンプレートをキャプチャすることができます。

たとえば、プレゼンテーション、ビジネス、およびデータの各レイヤーが存在するソリューションを頻繁に使用する場合、その構造を持つ新しいソリューションを作成するテンプレートを構成できます。

#### <a name="to-create-a-solution-template"></a>ソリューション テンプレートを作成するには

1. [Download and install the Export Template Wizard](https://go.microsoft.com/fwlink/?LinkId=196686), if you have not already done this.

2. 将来のプロジェクトの開始点として使用するソリューション構造を作成します。

3. **[ファイル]** メニューの **[VSIX としてテンプレートをエクスポート]** をクリックします。 The **Export Template as VSIX Wizard** opens.

4. ウィザードの指示に従って、テンプレートに含めるプロジェクトを追加し、テンプレートの名前と説明を入力して、出力する場所を指定します。

> [!NOTE]
> このトピックの内容は、Visual Studio ALM Rangers が作成した『Visual Studio アーキテクチャ ツーリング ガイダンス』から抽出して、わかりやすくしたものです。このガイダンスは、Most Valued Professional (MVP)、Microsoft Services、および Visual Studio 製品チームとライターのコラボレーションにより作成されました。 [Click here to download the complete Guidance package.](https://go.microsoft.com/fwlink/?LinkID=191984)

## <a name="related-materials"></a>関連資料

[Organizing and Managing Your Models](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-9-organizing-and-managing-your-models) - video by Clint Edmondson.

[Visual Studio Architecture Tooling Guidance](../modeling/visual-studio-architecture-tooling-guidance.md) – Further guidance on managing models in a team

## <a name="see-also"></a>参照

[Manage models and diagrams under version control](../modeling/manage-models-and-diagrams-under-version-control.md)
[Use models in your development process](../modeling/use-models-in-your-development-process.md)
