---
title: 複数プロジェクトのテンプレートを作成する
description: Visual Studio で、多くのプロジェクトのコンテナーとして同時に使用できる、複数プロジェクトのテンプレートを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 04/17/2019
ms.topic: how-to
helpviewer_keywords:
- Visual Studio templates, creating multi-project
- project templates, multi-project
- multi-project templates
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: c4cfc7f51999056379acd73ec7ec3933c1f31a51
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875407"
---
# <a name="how-to-create-multi-project-templates"></a>方法: 複数プロジェクトのテンプレートを作成する

複数プロジェクトのテンプレートは、2 つ以上のプロジェクトのコンテナーとして機能します。 複数プロジェクトのテンプレートに基づくプロジェクトが作成されると、テンプレート内のすべてのプロジェクトがソリューションに追加されます。

複数プロジェクトのテンプレートには、2 つ以上のプロジェクト テンプレートと **ProjectGroup** 型のルート テンプレートが含まれます。

複数プロジェクトのテンプレートは、1 つのプロジェクトのテンプレートとは動作が異なります。 これらには、次の固有の特性があります。

- 複数プロジェクトのテンプレートの個別のプロジェクトには、テンプレートを使用して新しいプロジェクトを作成するとき、名前を割り当てることができません。 代わりに、*vstemplate* ファイルの **ProjectTemplateLink** 要素の **ProjectName** 属性を使用して、各プロジェクトの名前を指定します。

- 複数プロジェクトのテンプレートには別の言語のプロジェクトを含めることができますが、テンプレート全体そのものは 1 つのカテゴリにのみ配置できます。 *vstemplate* ファイルの **ProjectType** 要素でテンプレートのカテゴリを指定します。

複数プロジェクトのテンプレートは、次の項目を含み、 *.zip* ファイルに圧縮する必要があります。

- 複数プロジェクトのテンプレート全体のルート *vstemplate* ファイル。 このルート *vstemplate* ファイルには、新しいプロジェクトを作成するダイアログ ボックスに表示されるメタデータが含まれています。 これによって、テンプレート内のプロジェクト用の *vstemplate* ファイルを検索する場所も指定されます。 このファイルは、 *.zip* ファイルのルートに配置する必要があります。

- 完全なプロジェクト テンプレートに必要なファイルを含む 2 つ以上のフォルダー。 フォルダーにはプロジェクトのすべてのコード ファイルが含まれ、プロジェクトの *vstemplate* ファイルも含まれます。

たとえば、2 つのプロジェクトを含む複数プロジェクトのテンプレート *.zip* ファイルは、次のファイルとディレクトリを持つことが考えられます。

- *MultiProjectTemplate.vstemplate*
- *\Project1\MyTemplate.vstemplate*
- *\Project1\Project1.vbproj*
- *\Project1\Class.vb*
- *\Project2\MyTemplate.vstemplate*
- *\Project2\Project2.vbproj*
- *\Project2\Class.vb*

複数プロジェクトのテンプレートのルート *vstemplate* ファイルは、単一プロジェクトのテンプレートとは次の点が異なります。

- **VSTemplate** 要素の **Type** 属性は、**Project** の代わりに **ProjectGroup** という値を持っています。 次に例を示します。

    ```xml
    <VSTemplate Version="2.0.0" Type="ProjectGroup"
        xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    ```

- **TemplateContent** 要素には、含まれるプロジェクトの *vstemplate* ファイルへのパスを定義する 1 つ以上の **ProjectTemplateLink** 要素を持つ **ProjectCollection** 要素が含まれます。 次に例を示します。

    ```xml
    <TemplateContent>
        <ProjectCollection>
            <ProjectTemplateLink>
                Project1\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink>
                Project2\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
    ```

> [!TIP]
> 複数プロジェクトのテンプレートのみを新しいプロジェクト ダイアログ ボックスに表示し、それに含まれる個々のプロジェクトを表示しない場合は、内部テンプレートに[非表示](../extensibility/hidden-element-visual-studio-templates.md)とマークを付けます。 次に例を示します。
>
> ```xml
> <VSTemplate Type="Project" ... >
>     <TemplateData>
>         ...
>         <Hidden>true</Hidden>
>     </TemplateData>
>     ...
> </VSTemplate>
> ```

## <a name="create-a-multi-project-template-from-an-existing-solution"></a>既存のソリューションから複数プロジェクトのテンプレートを作成する

1. ソリューションを作成して 2 つ以上のプロジェクトを追加します。

2. テンプレートにエクスポートする準備ができるまで、プロジェクトをカスタマイズします。

   > [!TIP]
   > [テンプレート パラメーター](template-parameters.md)を使用していて、親テンプレートの変数を参照したい場合は、パラメーターの名前にプレフィックス `ext_` を付加します。 たとえば、`$ext_safeprojectname$` のようにします。 また、**ProjectTemplateLink** 要素の **CopyParameters** 属性を **true** に設定します。
   >
   > ```xml
   > <ProjectTemplateLink ProjectName="MyProject" CopyParameters="true">...</ProjectTemplateLink>
   > ```

3. **[プロジェクト]** メニューの **[テンプレートのエクスポート]** を選択します。

   **テンプレートのエクスポート ウィザード** が開きます。

4. **[テンプレートの種類の選択]** ページで、 **[プロジェクト テンプレート]** を選択します。 テンプレートにエクスポートするプロジェクトを 1 つ選択し、 **[次へ]** を選択します。 (ソリューション内のプロジェクトごとに、この手順を繰り返します。)

5. **[テンプレート オプションの選択]** ページで、テンプレートの名前および省略可能な説明、アイコン、プレビュー画像を入力します。 **[完了]** を選択します。

   プロジェクトが *.zip* ファイルにエクスポートされ、指定した出力場所に置かれます。

   > [!NOTE]
   > 各プロジェクトはテンプレートに個別にエクスポートする必要があるため、ソリューションのプロジェクトごとに上記の手順を繰り返します。

6. テンプレートのディレクトリを作成し、プロジェクトごとにサブディレクトリを作ります。

7. 各プロジェクトの *.zip* ファイルの内容を、作成した対応するサブディレクトリに抽出します。

8. ベース ディレクトリ内に、 *.vstemplate* ファイル拡張子を持つ XML ファイルを作成します。 このファイルには、複数プロジェクトのテンプレートのメタデータが含まれます。 ファイルの構造については、この後の例をご覧ください。 プロジェクトごとに *vstemplate* ファイルの相対パスを指定してください。

9. ベース ディレクトリ内のすべてのファイルを選び、右クリック メニューまたはコンテキスト メニューから、 **[送る]**  >  **[圧縮 (zip 形式) フォルダー]** の順に選びます。

   ファイルとフォルダーが *.zip* ファイルに圧縮されます。

10. ユーザー プロジェクト テンプレートのディレクトリに *.zip* ファイルをコピーします。 既定では、このディレクトリは *%USERPROFILE%\Documents\Visual Studio \<version\>\Templates\ProjectTemplates* です。

11. Visual Studio で **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択し、ご自分のテンプレートが表示されることを確認します。

## <a name="two-project-example"></a>2 つのプロジェクトの例

基本的なマルチプロジェクトのルート *vstemplate* ファイルの例を以下に示します。 この例では、テンプレートに **My Windows Application** と **My Class Library** という 2 つのオブジェクトが含まれます。 **ProjectTemplateLink** 要素の **ProjectName** 属性で、プロジェクトに適用する名前を指定します。

> [!TIP]
> **ProjectName** 属性を指定しない場合、*vstemplate* ファイルの名前がプロジェクト名として使用されます。

```xml
<VSTemplate Version="2.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <ProjectTemplateLink ProjectName="My Windows Application">
                WindowsApp\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink ProjectName="My Class Library">
                ClassLib\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="example-with-solution-folders"></a>ソリューション フォルダーでの例

この例では、**SolutionFolder** 要素を使用して、プロジェクトを **Math Classes** と **Graphics Classes** という 2 つのグループに分割します。 テンプレートには 4 つのプロジェクトがあり、その 2 つは各ソリューション フォルダーに配置されます。

```xml
<VSTemplate Version="2.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <SolutionFolder Name="Math Classes">
                <ProjectTemplateLink ProjectName="MathClassLib1">
                    MathClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="MathClassLib2">
                    MathClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
            <SolutionFolder Name="Graphics Classes">
                <ProjectTemplateLink ProjectName="GraphicsClassLib1">
                    GraphicsClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="GraphicsClassLib2">
                    GraphicsClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目

- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [方法: プロジェクト テンプレートを作成する](../ide/how-to-create-project-templates.md)
- [Visual Studio テンプレート スキーマ参照 (機能拡張)](../extensibility/visual-studio-template-schema-reference.md)
- [SolutionFolder 要素 (Visual Studio テンプレート)](../extensibility/solutionfolder-element-visual-studio-templates.md)
- [ProjectTemplateLink 要素 (Visual Studio テンプレート)](../extensibility/projecttemplatelink-element-visual-studio-templates.md)
