---
title: プロジェクトアイテム要素 (Visual Studio プロジェクト テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: conceptual
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
ms.openlocfilehash: 11052d8e585f1d06f6d787402001cfbbe2b6810f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701850"
---
# <a name="projectitem-element-visual-studio-project-templates"></a>プロジェクト項目要素
プロジェクト テンプレートに含まれるファイルを指定します。

> [!NOTE]
> 要素`ProjectItem`は、テンプレートがプロジェクトまたは項目のどちらに対して使用されているかに応じて、異なる属性を受け入れます。 このトピックでは、`ProjectItem`プロジェクト テンプレートの要素について説明します。 項目テンプレートの要素の`ProjectItem`説明については、「[プロジェクトアイテム要素 (Visual Studio 項目テンプレート)」](../extensibility/projectitem-element-visual-studio-item-templates.md)を参照してください。

 \<VSTemplate \<> テンプレート\<プロジェクト>\<プロジェクト>>>コンテンツ

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
| `TargetFileName` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトを作成するときのプロジェクト項目の名前とパスを指定します。 この属性は、テンプレート *.zip*ファイル内のディレクトリ構造とは異なるディレクトリ構造を作成する場合や、パラメーター置換を使用して項目名を作成する場合に便利です。 |
| `ReplaceParameters` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトを作成するときに置き換える必要があるパラメーター値を項目に含めるかどうかを指定するブール値。 既定値は `false` です。 |
| `OpenInEditor` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトを作成するときに、項目をそれぞれのエディターで[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]開くかどうかを指定するブール値。<br /><br /> と`OpenInWebBrowser``OpenInHelpBrowser`属性は、`OpenInEditor`の値を持つ項目では`true`無視されます。<br /><br /> 既定値は `false` です。 |
| `OpenInWebBrowser` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトを作成するときに、アイテムを Web ブラウザーで開くかどうかを指定するブール値。<br /><br /> Web ブラウザで開くことができるのは、プロジェクトにローカルな HTML ファイルとテキスト ファイルだけです。 この属性を使用して外部 URL を開くことはできません。<br /><br /> 既定値は `false` です。 |
| `OpenInHelpBrowser` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトを作成するときに、ヘルプ ビューアーでアイテムを開くかどうかを指定するブール値。<br /><br /> ヘルプ ブラウザで開くことができるのは、プロジェクトにローカルな HTML ファイルとテキスト ファイルだけです。 この属性を使用して外部 URL を開くことはできません。<br /><br /> 既定値は `false` です。 |
| `OpenOrder` | 省略可能な属性です。<br /><br /> 各エディターでアイテムを開く順序を表す数値を指定します。 すべての値は 10 の倍数である必要があります。 より大きい`OpenOrder`値を持つアイテムが最初に開かれます。 |

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[プロジェクト](../extensibility/project-element-visual-studio-templates.md)|プロジェクトに追加するファイルまたはディレクトリを指定します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テンプレート`string` *.zip*ファイル内のファイルの名前またはパスを表す A。

## <a name="remarks"></a>Remarks
 `ProjectItem`は オプションの子`Project`です。

 この`TargetFileName`属性を使用して、テンプレート *.zip*ファイル内のディレクトリ構造とは異なるディレクトリ構造を作成できます。 たとえば *、MyFile.vb*ファイルがテンプレート *.zip*ファイルのルートに存在し、テンプレートから作成されたすべてのプロジェクトの*CustomFiles*というディレクトリにファイルを配置する場合は、次の XML を使用します。

```xml
<ProjectItem TargetFileName="CustomFiles\MyFile.vb">MyFile.vb</ProjectItem>
```

 この`TargetFileName`属性は、ファイル名に国際文字が含まれているファイルの名前を変更するためにも使用できます。 たとえば、テンプレートの *.zip*ファイルには Unicode 文字を含むファイル名を含めることができないため *、.zip*ファイルに圧縮する前にファイル名を変更する必要があります。 この`TargetFileName`属性を使用して、元の Unicode ファイル名に戻すファイル名を設定できます。

 この`TargetFileName`属性は、パラメーターを使用してファイルの名前を変更するためにも使用できます。 次の手順では、テンプレート *.zip*ファイルのルート ディレクトリにある*MyFile.vb*ファイルの名前をプロジェクト名に基づいてファイル名に変更する方法について説明します。

### <a name="to-rename-files-with-parameters"></a>パラメータを使用してファイルの名前を変更するには

1. *.vstemplate*ファイルで次の XML を使用します。

   ```xml
   <ProjectItem TargetFileName="$safeprojectname$.vb">MyFile.vb</ProjectItem>
   ```

2. テキスト エディタまたは[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]でプロジェクト ファイル ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]プロジェクトの *.vbproj)* を開きます。

3. 次の XML に似たプロジェクト ファイルの行を見つけます。

   ```xml
   <Compile Include="MyFile.vb">
   ```

4. コード行を次の XML に置き換えます。

   ```xml
   <Compile Include="$safeprojectname$.vb">
   ```

    このテンプレートからプロジェクトを作成すると、ファイル名はユーザーが [**新しいプロジェクト**] ダイアログ ボックスに入力した名前に基づいて作成され、安全でない文字とスペースがすべて削除されます。 詳細については、「テンプレート[パラメーター](../ide/template-parameters.md)」を参照してください。

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
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [ProjectItem 要素 (Visual Studio 項目テンプレート)](../extensibility/projectitem-element-visual-studio-item-templates.md)
