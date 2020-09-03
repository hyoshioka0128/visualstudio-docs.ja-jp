---
title: ProjectItem 要素 (Visual Studio プロジェクトテンプレート) |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- ProjectItem element [Visual Studio project templates]
- <ProjectItem> element [Visual Studio project templates]
ms.assetid: 82879fbe-7756-42cd-9a07-c10edf5b4673
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 943f50823892e3cd942709bdcd4556b65c006b58
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85770308"
---
# <a name="projectitem-element-visual-studio-project-templates"></a>ProjectItem 要素 (Visual Studio プロジェクトテンプレート)
プロジェクトテンプレートに含まれるファイルを指定します。

> [!NOTE]
> 要素は、 `ProjectItem` テンプレートがプロジェクトと項目のどちらであるかに応じて、異なる属性を受け取ります。 このトピックでは、プロジェクトテンプレートの要素について説明し `ProjectItem` ます。 `ProjectItem`項目テンプレートの要素の説明については、「 [ProjectItem 要素 (Visual Studio 項目テンプレート)](../extensibility/projectitem-element-visual-studio-item-templates.md)」を参照してください。

 \<VSTemplate> \<TemplateContent>
 \<Project>
 \<ProjectItem>

## <a name="syntax"></a>構文

```
<ProjectItem
    TargetFileName="TargetFileName.ext"
    ReplaceParameters="true/false"
    OpenInEditor="true/false"
    OpenInWebBrowser="true/false"
    OpenInHelpBrowser="true/false"
    OpenOrder="Value">
        FileName.ext
</ProjectItem>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

| 属性 | 説明 |
|---------------------| - |
| `TargetFileName` | 省略可能な属性です。<br /><br /> プロジェクトがテンプレートから作成されるときのプロジェクト項目の名前とパスを指定します。 この属性は、テンプレート *.zip* ファイルのディレクトリ構造とは異なるディレクトリ構造を作成したり、パラメーター置換を使用して項目名を作成したりする場合に便利です。 |
| `ReplaceParameters` | 省略可能な属性です。<br /><br /> プロジェクトがテンプレートから作成されたときに置き換える必要があるパラメーター値が項目にあるかどうかを指定するブール値。 既定値は `false`にする必要があります。 |
| `OpenInEditor` | 省略可能な属性です。<br /><br /> [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]プロジェクトがテンプレートから作成されたときに、内のそれぞれのエディターで項目を開くかどうかを指定するブール値。<br /><br /> `OpenInWebBrowser`属性と `OpenInHelpBrowser` 属性は、値がの項目では無視され `OpenInEditor` `true` ます。<br /><br /> 既定値は `false` です。 |
| `OpenInWebBrowser` | 省略可能な属性です。<br /><br /> プロジェクトがテンプレートから作成されたときに、その項目を Web ブラウザーで開くかどうかを指定するブール値。<br /><br /> Web ブラウザーで開くことができるのは、プロジェクトに対してローカルな HTML ファイルとテキストファイルだけです。 この属性では外部 Url を開くことができません。<br /><br /> 既定値は `false` です。 |
| `OpenInHelpBrowser` | 省略可能な属性です。<br /><br /> プロジェクトがテンプレートから作成されたときに、その項目をヘルプビューアーで開くかどうかを指定するブール値。<br /><br /> ヘルプブラウザーで開くことができるのは、プロジェクトに対してローカルな HTML ファイルとテキストファイルだけです。 この属性では外部 Url を開くことができません。<br /><br /> 既定値は `false` です。 |
| `OpenOrder` | 省略可能な属性です。<br /><br /> 各エディターで項目が開かれる順序を表す数値を指定します。 すべての値は、10の倍数である必要があります。 `OpenOrder`値が大きい項目が最初に開かれます。 |

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[プロジェクト](../extensibility/project-element-visual-studio-templates.md)|プロジェクトに追加するファイルまたはディレクトリを指定します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 `string`テンプレート *.zip*ファイル内のファイルの名前またはパスを表す。

## <a name="remarks"></a>解説
 `ProjectItem` は、の省略可能な子です `Project` 。

 属性を使用して、 `TargetFileName` テンプレートの *.zip* ファイル内のディレクトリ構造とは異なるディレクトリ構造を作成できます。 たとえば、 *myfile.txt* ファイルがテンプレート *.zip* ファイルのルートに存在するものの、テンプレートから作成されたすべてのプロジェクトの *customfiles* という名前のディレクトリにファイルを配置する場合は、次の XML を使用します。

```xml
<ProjectItem TargetFileName="CustomFiles\MyFile.vb">MyFile.vb</ProjectItem>
```

 属性を使用して、 `TargetFileName` ファイル名に国際的な文字を含むファイルの名前を変更することもできます。 たとえば、テンプレートの *.zip* ファイルに Unicode 文字のファイル名を含めることはできません。そのため、 *.zip* ファイルに圧縮する前に、ファイルの名前を変更する必要があります。 属性を使用して、 `TargetFileName` ファイル名を元の Unicode ファイル名に戻すことができます。

 `TargetFileName`属性を使用して、パラメーターでファイルの名前を変更することもできます。 次の手順では、テンプレートの *.zip*ファイルのルートディレクトリに存在*するファイル名*を、プロジェクト名に基づいてファイル名に変更する方法について説明します。

### <a name="to-rename-files-with-parameters"></a>パラメーターを使用してファイル名を変更するには

1. *.Vstemplate*ファイルで次の XML を使用します。

   ```xml
   <ProjectItem TargetFileName="$safeprojectname$.vb">MyFile.vb</ProjectItem>
   ```

2. テキストエディターまたはでプロジェクトファイル (プロジェクトの *.vbproj* ) を開き [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

3. プロジェクトファイル内の次の XML のような行を探します。

   ```xml
   <Compile Include="MyFile.vb">
   ```

4. コード行を次の XML に置き換えます。

   ```xml
   <Compile Include="$safeprojectname$.vb">
   ```

    このテンプレートからプロジェクトを作成すると、[ **新しいプロジェクト** ] ダイアログボックスでユーザーが入力した名前に基づいて、安全でないすべての文字とスペースが削除されます。 詳細については、「 [テンプレートパラメーター](../ide/template-parameters.md)」を参照してください。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] アプリケーションでのプロジェクト テンプレートのメタデータの例を次に示します。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
            <ProjectItem ReplaceParameters="true">Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [ProjectItem 要素 (Visual Studio 項目テンプレート)](../extensibility/projectitem-element-visual-studio-item-templates.md)
