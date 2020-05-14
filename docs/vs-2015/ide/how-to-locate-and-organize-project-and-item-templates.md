---
title: '方法 : プロジェクト テンプレートと項目テンプレートを配置して整理する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- project templates [Visual Studio], locations
- custom template locations [Visual Studio]
- item templates, locations
- Visual Studio templates, locations
- project templates [Visual Studio], displaying
- templates [Visual Studio], locations
ms.assetid: 71f9ed52-c9c9-4818-9bce-c279ffaa0438
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b5f55de910eb77ec7ccbd205b78d5c95039e6b39
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651868"
---
# <a name="how-to-locate-and-organize-project-and-item-templates"></a>方法 : プロジェクト テンプレートと項目テンプレートを配置して整理する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テンプレート ファイルは、テンプレートが **[新しいプロジェクト]** ダイアログ ボックスや **[新しい項目の追加]** ダイアログ ボックスに表示されるように、Visual Studio が認識する場所に配置する必要があります。 テンプレートにはカスタム サブカテゴリを作成できます。作成したサブカテゴリも、ユーザー インターフェイスに表示されます。

## <a name="locating-templates"></a>テンプレートの配置
 既定では、Visual Studio はプロジェクト テンプレートと項目テンプレートを 2 つの場所で検索します。 .vstemplate ファイルを含む圧縮ファイルがこれらの場所に存在する場合、テンプレートは **[新しいプロジェクト]** ダイアログ ボックスまたは **[新しい項目の追加]** ダイアログ ボックスに表示されます。

### <a name="installed-templates"></a>インストールされたテンプレート
 既定では、製品と共にインストールされたテンプレートは次の場所に配置されます。

- \\*VisualStudioInstallationDirectory*\Common7\IDE\ItemTemplates\\*言語*\\*ロケール*\

- \\*VisualStudioInstallationDirectory*\Common7\IDE\ProjectTemplates\\*言語*\\*ロケール*\\

  たとえば、次のディレクトリには英語用の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクト テンプレートが含まれています。

  C:\\*VisualStudioInstallationDirectory*\Common7\IDE\ItemTemplates\VisualBasic\1033\

### <a name="custom-templates"></a>カスタム テンプレート
 既定では、カスタム テンプレートは次の場所に配置されます。

- \My Documents\Visual Studio *バージョン*\Templates\ProjectTemplates\\*言語*\

- \My Documents\Visual Studio *バージョン*\Templates\ItemTemplates\\*言語*\

  たとえば、次のディレクトリにはカスタム [!INCLUDE[csprcs](../includes/csprcs-md.md)] プロジェクト テンプレートが含まれています。

  C:\Documents and Settings\<ユーザー名>\My Documents\\<Visual Studio バージョン\>\Templates\ProjectTemplates\Visual C#\

  カスタム テンプレートには、ローカライズされたテンプレート用のサブディレクトリは含まれていません。 カスタム テンプレートの既定ディレクトリは、 **[オプション]** ダイアログ ボックスの **[環境] > [プロジェクトおよびソリューション]** で変更できます。

## <a name="organizing-templates"></a>テンプレートの整理
 **[新しいプロジェクト]** ダイアログ ボックスおよび **[新しい項目の追加]** ダイアログ ボックスには、インストールされたテンプレートやカスタム テンプレートの場所のディレクトリ構造がカテゴリとして反映されます。 これらのディレクトリ構造を変更することにより、自分にとってわかりやすいようにテンプレートを整理できます。

> [!NOTE]
> プログラミング言語のレベルでは、新しいカテゴリを作成できません。 新しいカテゴリは、各言語内でのみ作成できます。

 特定言語について、インストールされたテンプレートとカスタム テンプレートのディレクトリ構造が異なる場合 (あるフォルダーについて、片方では下位にディレクトリがあり、もう片方ではディレクトリがない場合)、 **[新しいプロジェクト]** ダイアログ ボックスでは、すべてのカテゴリをマージしたカテゴリのセットが表示されます。

### <a name="organizing-installed-templates"></a>インストールされたテンプレートの整理
 インストールされたテンプレートを整理するには、プログラミング言語のフォルダー内にサブディレクトリを作成します。 これらのサブディレクトリは、各言語の **[新しいプロジェクト]** ダイアログ ボックスおよび **[新しい項目の追加]** ダイアログ ボックスで、仮想フォルダーとして表示されます。

##### <a name="to-create-new-installed-project-template-categories"></a>インストールされたプロジェクト テンプレートの新しいカテゴリを作成するには

1. インストールされたテンプレートのディレクトリの言語フォルダーに、フォルダーを作成します。 たとえば、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクト テンプレートに対して Office カテゴリを作成するには、次のディレクトリを作成する必要があります。

    \\*Visual Studio のインストール ディレクトリ*\Common7\IDE\ProjectTemplates\VisualBasic\1033\Office\

2. このカテゴリのすべてのテンプレートを新しいフォルダーに配置します。

3. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のすべてのインスタンスを閉じます。

4. **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックし、「**cmd**」と入力し、 **[OK]** をクリックします。

5. コマンド プロンプトで、devenv.exe を含むディレクトリに移動し、「**devenv /installvstemplates**」と入力します。

6. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を実行します。

7. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

8. Office カテゴリが **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** ウィンドウの [[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]] の下に表示されることを確認します。

   プロジェクト項目テンプレートのサブセットをカスタム フォルダーとしてグループ化することもできます。

##### <a name="to-create-new-installed-item-template-categories"></a>インストールされた項目テンプレートの新しいカテゴリを作成するには

1. インストールされたテンプレートのディレクトリの言語フォルダーに、フォルダーを作成します。 たとえば、[!INCLUDE[csprcs](../includes/csprcs-md.md)] 項目テンプレートに対して Web カテゴリを作成するには、次のディレクトリを作成する必要があります。

     \\*Visual Studio のインストール ディレクトリ*\Common7\IDE\ItemTemplates\CSharp\1033\Web\

2. このカテゴリのすべてのテンプレートを新しいフォルダーに配置します。

3. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のすべてのインスタンスを閉じます。

4. **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックし、「**cmd**」と入力し、 **[OK]** をクリックします。

5. コマンド プロンプトで、devenv.exe を含むディレクトリに移動し、「**devenv /setup**」と入力します。

6. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を実行します。

7. プロジェクトを作成するか、既存のプロジェクトを開きます。

8. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

9. Web カテゴリが **[新しい項目の追加]** ダイアログ ボックスの **[プロジェクトの種類]** ウィンドウに表示されることを確認します。

### <a name="organizing-custom-templates"></a>カスタム テンプレートの整理
 カスタム テンプレートを独自のカテゴリに整理するには、カスタム テンプレートの場所に新しいフォルダーを追加します。 **[新しいプロジェクト]** ダイアログ ボックスには、テンプレート カテゴリに加えた変更が反映されます。

##### <a name="to-create-new-custom-project-template-categories"></a>カスタム プロジェクト テンプレートの新しいカテゴリを作成するには

1. カスタム プロジェクト テンプレートのディレクトリの言語フォルダーに、フォルダーを作成します。 たとえば、[!INCLUDE[csprcs](../includes/csprcs-md.md)] テンプレートに対して HelloWorld カテゴリを作成するには、次のディレクトリを作成する必要があります。

    \My Documents\\<Visual Studio バージョン\>\Templates\ProjectTemplates\CSharp\HelloWorld\

2. このカテゴリのすべてのテンプレートを新しいフォルダーに配置します。

3. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

4. HelloWorld カテゴリが **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** ウィンドウの [[!INCLUDE[csprcs](../includes/csprcs-md.md)]] の下に表示されることを確認します。

   カスタム項目テンプレートのサブセットをカスタム フォルダーとしてグループ化することもできます。

##### <a name="to-create-new-custom-item-template-categories"></a>カスタム項目テンプレートの新しいカテゴリを作成するには

1. カスタム項目テンプレートのディレクトリの言語フォルダーに、フォルダーを作成します。 たとえば、[!INCLUDE[csprcs](../includes/csprcs-md.md)] テンプレートに対して HelloWorld カテゴリを作成するには、次のディレクトリを作成する必要があります。

     \My Documents\\<Visual Studio バージョン\>\Templates\ItemTemplates\CSharp\HelloWorld\

2. このカテゴリのすべてのテンプレートを新しいフォルダーに配置します。

3. プロジェクトを作成するか、既存のプロジェクトを開きます。

4. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

5. HelloWorld カテゴリが **[新しい項目の追加]** ダイアログ ボックスの **[プロジェクトの種類]** ウィンドウに表示されることを確認します。

### <a name="displaying-templates-in-parent-categories"></a>親カテゴリでのテンプレートの表示
 .vstemplate ファイルの `NumberOfParentCategoriesToRollUp` 要素を使用して、サブカテゴリのテンプレートを親カテゴリに表示できます。 この手順は、プロジェクト テンプレートと項目テンプレートのどちらでも同じです。

##### <a name="to-display-templates-in-parent-categories"></a>親カテゴリにテンプレートを表示するには

1. テンプレートを含む .zip ファイルを探します。

2. .zip ファイルを展開します。

3. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で .vstemplate ファイルを開きます。

4. `TemplateData` 要素に、`NumberOfParentCategoriesToRollUp` 要素を追加します。 たとえば、次のコードを実行すると、テンプレートが親カテゴリに表示されますが、親カテゴリよりも上のレベルでは表示されません。

    ```
    <TemplateData>
        ...
        <NumberOfParentCategoriesToRollUp>
            1
        </NumberOfParentCategoriesToRollUp>
        ...
    </TemplateData>
    ```

5. .vstemplate ファイルを保存して、閉じます。

6. テンプレートでファイルを選択して右クリックし、 **[送る]** をクリックして **[圧縮 (zip 形式) フォルダー]** をクリックします。 ファイルは .zip ファイルに圧縮されます。

7. 抽出したテンプレート ファイルと古いテンプレート .zip ファイルを削除します。

8. 削除した .zip ファイルが含まれていたディレクトリに、新しい .zip ファイルを配置します。

## <a name="see-also"></a>参照
 [テンプレートのカスタマイズ](../ide/customizing-project-and-item-templates.md) [Visual Studio テンプレートスキーマ参照](../extensibility/visual-studio-template-schema-reference.md) [NumberOfParentCategoriesToRollUp (visual Studio テンプレート)](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md) [方法: プロジェクトテンプレートを作成](../ide/how-to-create-project-templates.md)する方法[: 項目テンプレートを作成する](../ide/how-to-create-item-templates.md)
