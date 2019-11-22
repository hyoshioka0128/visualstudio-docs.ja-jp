---
title: Create UML modeling projects and diagrams | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.addnewdiagramdialog
- vs.teamarch.createnewmodelingprojectdialog
helpviewer_keywords:
- projects [Visual Studio ALM], modeling
- diagrams - modeling, modeling
- modeling diagrams
- projects, UML
- UML, deleting diagrams
- UML
- UML diagrams, adding
- UML, projects
- Visual Studio ALM, modeling projects
- modeling projects
- UML diagrams
- projects, modeling
ms.assetid: c178b04b-4fd2-4bed-97e3-d793dae8649c
caps.latest.revision: 50
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d5884dcd3f9e3cb8f1910d2e23ec80f910ed2fc9
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301009"
---
# <a name="create-uml-modeling-projects-and-diagrams"></a>UML モデリング プロジェクトおよびダイアグラムを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML モデルは、ソフトウェア システムを理解したり設計したりする上で、また、ソフトウェア システムについて話し合う際に役立ちます。 Visual Studio には、最もよく使用される 5 つの UML 図 (アクティビティ図、クラス図、コンポーネント図、シーケンス図、およびユース ケース図) のテンプレートが用意されています。 また、システムの構造の定義に役立つレイヤー図も作成できます。

 UML モデリング図とレイヤー図が存在することが可能なのは、モデリング プロジェクト内のみです。 各モデリング プロジェクトには、1 つの共有 UML モデルといくつかの UML 図が含まれています。 各図はモデルの部分ビューです。 UML モデルは、UML 図にあるすべての要素が含まれていて、UML モデル エクスプローラーを使用して表示することができます。 For information about models and their relationship to diagrams, see [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md). For information about modeling projects under version control, see [Manage models and diagrams under version control](../modeling/manage-models-and-diagrams-under-version-control.md) and [Structure your modeling solution](../modeling/structure-your-modeling-solution.md)

> [!NOTE]
> また、プログラム コードを視覚化するために使用される、.NET クラス図と呼ばれる別の種類の図もあります。 For more information, see [Designing and Viewing Classes and Types](https://go.microsoft.com/fwlink/?LinkId=142231).

## <a name="CreatingModelingDiagrams"></a> Create a Diagram in a Modeling Project
 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

#### <a name="to-create-a-diagram-and-add-it-to-a-project"></a>図を作成してプロジェクトに追加するには

1. On the **Architecture** menu, choose **New UML or Layer Diagram**.

2. In the **Add New Diagram** dialog box, click the type of modeling diagram that you want.

    ![Add New Diagram dialog](../modeling/media/uml-adddiagram.png "UML_AddDiagram")

3. 新しい図の名前を入力します。

4. In the **Add to modeling project** box:

   - Select a modeling project that already exists in your solution, and then click **OK**.

     \- または

   1. Select **Create a new modeling project**, and then click **OK**.

   2. In the **Create New Modeling Project** dialog box, type a name and location for the new project, and then click **OK**.

        ![Create New Modeling Project dialog](../modeling/media/uml-createmodel.png "UML_CreateModel")

        ソリューションが開いている場合は、新しいプロジェクトがソリューションに追加されます。 開いているソリューションがない場合は、新しいソリューションの名前を入力できます。

   モデリング プロジェクトが既に存在する場合は、次の手順を使用することもできます。

#### <a name="to-add-a-diagram-to-an-existing-modeling-project"></a>既存のモデリング プロジェクトに図を追加するには

1. In **Solution Explorer**, click the modeling project node.

    > [!NOTE]
    > The modeling project contains a model definition folder named **ModelDefinition**.

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. In the **Add New Item -** *\<project name>* dialog box, under **Templates**, click the modeling diagram type, for example, **UML Component Diagram**.

4. Type a name for the diagram, and then click **Add**.

     モデリング図が開き、モデリング プロジェクトに表示されます。

    > [!CAUTION]
    > 他のモデリング プロジェクト、またはソリューション内の他の場所に、既存の図ファイルを追加、コピー、またはドラッグしないでください。 そのようにすると、コピーした図から要素が消えたり、図を開いた際にエラーが発生したりします。 図のファイルは、そのファイルが作成されたモデリング プロジェクトから開く必要があります。 これは、UML 図がそのモデリング プロジェクトによって所有されるモデルのビューであるためです。 図のファイルをコピーするには、新しい図を作成し、コピー元の図から新しい図に要素をコピーします。 For more information, see [Troubleshooting Modeling Projects and Diagrams](#TroubleshootingModelingProjects).

#### <a name="to-create-a-blank-modeling-project"></a>空のモデリング プロジェクトを作成するには

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

2. In the **New Project** dialog box, under **Installed Templates**, click **Modeling Projects**.

3. In the middle window, click **Modeling Project**.

4. Name the project and specify a location in the **Name** and **Location** boxes.

5. In the **Solution** box, select **Add to Solution** to add the new project to a solution you already have open; or **Create new Solution** to close any open solution and add the project to a new solution.

## <a name="RemovingModelingDiagrams"></a> Removing Modeling Diagrams from a Project
 図を完全に削除することも、プロジェクトから図を一時的に除外し、後で元に戻すこともできます。

#### <a name="to-permanently-delete-a-diagram-from-a-project"></a>プロジェクトから図を完全に削除するには

- In **Solution Explorer**, right-click the main file that represents the diagram, and then click **Delete**.

     プロジェクトとファイル システムから図が削除されます。 The elements shown on the diagram are not removed from **UML Model Explorer**.

    > [!NOTE]
    > 各図は 2 つのファイルを持ちます。一方のファイルは、もう一方の付属ファイルです。 たとえば、`CD1` という名前のコンポーネント図がある場合は、`CD1.componentdiagram` という名前のファイルを削除する必要があります。 `CD1.componentdiagram.layout` という名前の付属ファイルは自動的に削除されます。

#### <a name="to-temporarily-exclude-a-diagram-from-a-project"></a>プロジェクトから図を一時的に除外するには

- In **Solution Explorer**, right-click the diagram file, and then click **Exclude from Project**.

     図が、プロジェクトから削除されます。 ファイル システムからは削除されません。

    > [!NOTE]
    > The elements shown on the diagram are not removed from **UML Model Explorer**.

#### <a name="to-restore-a-temporarily-excluded-diagram-to-a-project"></a>一時的に除外した図をプロジェクトに戻すには

1. In **Solution Explorer**, click the modeling project node.

    > [!NOTE]
    > The modeling project contains a model definition folder named **ModelDefinition**.

2. On the **Project** menu, click **Add Existing Item**.

3. In the **Add Existing Item** dialog box, locate the diagram file, select the file, and then click **Add**.

     モデリング図が開き、モデリング プロジェクトに表示されます。

    > [!NOTE]
    > それぞれの図に対応するファイルは、ファイル システム内に 2 つ存在します。 `.layout` という拡張子のファイルは選択しないでください。 また、Visual Studio において、既存の UML 図を複数のモデリング プロジェクトに追加する機能はサポートされていません。 各図のファイルは、そのファイルが作成されたモデリング プロジェクトの中で開く必要があります。 これは、UML 図にそのモデリング プロジェクトが所有するモデルのビューが表示されるためです。

## <a name="NonModelDiagrams"></a> Diagrams that Do Not Require Modeling Projects
 次の種類の図は、モデリング プロジェクトには含まれません。

- ソース コードのビューとして作成されるクラス図。 これらは、UML クラス図とは無関係です。 For more information, see [Designing and Viewing Classes and Types](../ide/designing-and-viewing-classes-and-types.md).

- コード マップ。 「 [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md)」を参照してください。

- UML 図でもレイヤー図でもない図 (ドメイン固有の言語など)。

## <a name="TroubleshootingModelingProjects"></a> Troubleshooting Modeling Projects and Diagrams
 次の表で、モデリング プロジェクトまたは図で発生する可能性のある問題と、その解決方法を説明します。

|**問題点**|**Causes**|**解決策**|
|---------------|----------------|--------------------|
|モデリング プロジェクトを開くことも、ソリューションに読み込むこともできません。<br /><br /> 次のメッセージが表示されます。<br /><br /> "ソリューション内の 1 つ以上のプロジェクトが正しく読み込まれていません。 詳細については、出力ウィンドウを確認してください。"<br /><br /> [出力] ウィンドウに次のメッセージが表示されます。<br /><br /> "*ModelingProjectFilenameAndPath*.modelproj: error: Unrecognized Guid format."|モデリング プロジェクトに、同じソリューション内にある同じ名前のプロジェクトへの参照が含まれています。<br /><br /> たとえば、同じソリューション内にある同じ名前のプロジェクトにレイヤーがリンクされています。|テキスト エディターを使用してモデリング プロジェクト ファイルを開き、参照を削除して、モデリング プロジェクトを再度開きます。<br /><br /> この問題を回避するには、同じ名前のプロジェクトへの参照を追加しないようにします。 プロジェクト名が一意であることを確認します。|
|他のモデリング プロジェクト、またはソリューション内の他の場所に図を追加、コピー、ドラッグすると、その図の要素がなくなります。<br /><br /> または<br /><br /> 図を開こうとすると、次のメッセージが表示されます。<br /><br /> -   "Some shapes or connectors on the diagram are missing because their definitions do not exist in this project. 図を閉じている間に定義がモデルから削除されたか、これらの定義を含まない別のプロジェクトに図がコピーされました。"<br /><br /> または<br /><br /> -   "This document is opened by another project."|モデリング プロジェクトから別のモデリング プロジェクトまたはソリューション内の別の場所に、図のファイルが追加、ドラッグ、またはコピーされました。|図のファイルをコピーするには、新しい図を作成し、コピー元の図から新しい図に要素をコピーします。|

## <a name="see-also"></a>参照
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [Structure your modeling solution](../modeling/structure-your-modeling-solution.md)
