---
title: Visual Studio 2017 のカスタムプロジェクトと項目テンプレートのアップグレード
titleSuffix: ''
description: Visual Studio 2017 以降のバージョンで使用するために、Visual Studio SDK の以前のバージョンからカスタムプロジェクトと項目テンプレートを更新する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ad02477b-e101-4f32-aeb7-292bf95d5c2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8442e24bf971b8a2a0bcf5baeeb397e4646ba766
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060277"
---
# <a name="upgrade-custom-project-and-item-templates-for-visual-studio-2017"></a>カスタム Visual Studio のプロジェクトと項目テンプレート2017のアップグレード

Visual studio 2017 以降では、visual studio は、以前のバージョンの Visual Studio とは異なる方法で、.vsix または .msi によってインストールされたプロジェクトおよび項目テンプレートを検出します。 カスタムプロジェクトまたは項目テンプレートを使用する拡張機能を所有している場合は、拡張機能を更新する必要があります。 この記事では、必要な作業について説明します。

この変更は、Visual Studio 2017 のみに影響します。 以前のバージョンの Visual Studio には影響しません。

VSIX 拡張機能の一部としてプロジェクトまたは項目テンプレートを作成する場合は、「 [カスタムプロジェクトおよび項目テンプレートの作成](../extensibility/creating-custom-project-and-item-templates.md)」を参照してください。

## <a name="template-scanning"></a>テンプレートのスキャン

以前のバージョンの Visual Studio では、 **devenv/setup** または **devenv/installvstemplates** はローカルディスクをスキャンして、プロジェクトと項目テンプレートを検索しました。 Visual Studio 2017 以降では、スキャンはユーザーレベルの場所に対してのみ実行されます。 既定のユーザーレベルの場所は、 **%USERPROFILE%\Documents \\<Visual Studio のバージョン \> \ テンプレート \\** です。 この場所は、   >  ウィザードで [**テンプレートを Visual Studio に自動的にインポート** する] オプションが選択されている場合に、[プロジェクトの **エクスポートテンプレート...** ] コマンドによって生成されるテンプレートに使用されます。

他の (ユーザー以外の) 場所については、テンプレートの場所とその他の特性を指定するマニフェスト (vstman) ファイルを含める必要があります。 Vstman ファイルは、テンプレートに使用される .vstemplate ファイルと共に生成されます。 .Vsix を使用して拡張機能をインストールした場合は、Visual Studio 2017 で拡張機能を再コンパイルすることによってこれを実現できます。 ただし、.msi を使用する場合は、変更を手動で行う必要があります。 これらの変更を行うために必要な操作の一覧については、「」を参照してください  **。** このページの後半にある MSI。

## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>プロジェクトテンプレートまたは項目テンプレートを使用して VSIX 拡張機能を更新する方法

1. Visual Studio 2017 でソリューションを開きます。 コードをアップグレードするように求められます。 **[OK]** をクリックします。

2. アップグレードが完了したら、インストール先のバージョンを変更することが必要になる場合があります。 VSIX プロジェクトで、source.extension.vsixmanifest ファイルを開き、[ **インストールするターゲット** ] タブを選択します。[ **バージョン範囲** ] フィールドが **[14.0]** の場合は、[ **編集** ] をクリックし、Visual Studio 2017 を含むように変更します。 たとえば、Visual Studio 2015 または Visual Studio 2017 に拡張機能をインストールする場合は **[14.0, 15.0]** に設定し、visual studio 2017 にインストールする場合は **[15.0]** に設定できます。

3. コードを再コンパイルします。

4. Visual Studio を閉じます。

5. VSIX をインストールします。

6. 更新プログラムをテストするには、次の手順を実行します。

    1. ファイルスキャンの変更は、次のレジストリキーによってアクティブ化されます。

         **reg add hklm\software\microsoft\visualstudio\15.0\VSTemplate/v Disabletemplates REG_DWORD Can/d 1/REG:32**

    2. キーを追加したら、 **devenv/installvstemplates** を実行します。

    3. Visual Studio を再度開きます。 予想される場所にテンプレートがあることを確認する必要があります。

    > [!NOTE]
    > Visual Studio 機能拡張プロジェクトテンプレートは、レジストリキーが存在する場合は使用できません。 レジストリキーを使用するには、レジストリキーを削除し、 **devenv/installvstemplates** を再実行する必要があります。

## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>プロジェクトテンプレートと項目テンプレートを配置するためのその他の推奨事項

- Zip 形式のテンプレートファイルは使用しないでください。 Zip 形式のテンプレートファイルは、リソースとコンテンツを取得するために圧縮解除する必要があるため、言えばに使用することができます。 代わりに、テンプレートの初期化を高速化するために、プロジェクトと項目テンプレートを個別のディレクトリに個別のファイルとして配置する必要があります。 VSIX 拡張機能の場合、VSIX ファイルの作成中に、SDK のビルドタスクによって、zip 形式のテンプレートが自動的に解凍されます。

- テンプレートの検出中に不要なリソースアセンブリが読み込まれないようにするために、テンプレート名、説明、アイコン、またはプレビューにはパッケージ/リソース ID のエントリを使用しないでください。 代わりに、ローカライズされたマニフェストを使用して、ローカライズされた名前またはプロパティを使用するロケールごとにテンプレートエントリを作成できます。

- テンプレートをファイル項目として含める場合は、マニフェストの生成によって期待どおりの結果が得られないことがあります。 その場合は、手動で生成されたマニフェストを VSIX プロジェクトに追加する必要があります。

## <a name="file-changes-in-project-and-item-templates"></a>プロジェクトテンプレートと項目テンプレートでのファイルの変更
新しいファイルを正しく作成できるように、Visual Studio 2015 と Visual Studio 2017 バージョンのテンプレートファイルの相違点を示します。

 Visual Studio 2015 で作成された既定のプロジェクト .vstemplate ファイルを次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ProjectTemplate1</Name>
    <Description>ProjectTemplate1</Description>
    <Icon>ProjectTemplate1.ico</Icon>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <SortOrder>1000</SortOrder>
    <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
    <CreateNewFolder>true</CreateNewFolder>
    <DefaultName>ProjectTemplate1</DefaultName>
    <ProvideDefaultName>true</ProvideDefaultName>
  </TemplateData>
  <TemplateContent>
    <Project File="ProjectTemplate.csproj" ReplaceParameters="true">
      <ProjectItem ReplaceParameters="true" TargetFileName="Properties\AssemblyInfo.cs">AssemblyInfo.cs</ProjectItem>
      <ProjectItem ReplaceParameters="true" OpenInEditor="true">Class1.cs</ProjectItem>
    </Project>
  </TemplateContent>
</VSTemplate>

```

 次に示すのは、VSIX プロジェクトの再構築に起因する vstman ファイル (VSIX プロジェクトのマニフェストディレクトリにあります) です。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\ProjectTemplate1</RelativePathOnDisk>
    <TemplateFileName>ProjectTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ProjectTemplate1</Name>
        <Description>ProjectTemplate1</Description>
        <Icon>ProjectTemplate1.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>ProjectTemplate1</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 [Templatedata](../extensibility/templatedata-element-visual-studio-templates.md)要素によって提供される情報は変わりません。 要素は、 **\<VSTemplateContainer>** 関連付けられているテンプレートの .vstemplate ファイルをポイントします。

 Visual Studio 2015 によって作成される既定の .vstemplate ファイルを次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ItemTemplate1</Name>
    <Description>ItemTemplate1</Description>
    <Icon>ItemTemplate1.ico</Icon>
    <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    <DefaultName>Class.cs</DefaultName>
  </TemplateData>
  <TemplateContent>
    <References>
      <Reference>
        <Assembly>System</Assembly>
      </Reference>
    </References>
    <ProjectItem ReplaceParameters="true">Class.cs</ProjectItem>
  </TemplateContent>
</VSTemplate>

```

 次に示すのは、VSIX プロジェクトの再構築に起因する vstman ファイル (VSIX プロジェクトのマニフェストディレクトリにあります) です。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Item">
    <RelativePathOnDisk>CSharp\1033\ItemTemplate1</RelativePathOnDisk>
    <TemplateFileName>ItemTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ItemTemplate1</Name>
        <Description>ItemTemplate1</Description>
        <Icon>ItemTemplate1.ico</Icon>
        <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
        <DefaultName>Class.cs</DefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>
```

 要素によって提供される情報は **\<TemplateData>** 変わりません。 要素は、 **\<VSTemplateContainer>** 関連付けられているテンプレートの .vstemplate ファイルをポイントします。

 Vstman ファイルのさまざまな要素の詳細については、「 [Visual Studio テンプレートマニフェストスキーマリファレンス](../extensibility/visual-studio-template-manifest-schema-reference.md)」を参照してください。

## <a name="upgrades-for-extensions-installed-with-an-msi"></a>と共にインストールされる拡張機能のアップグレード。MSI

MSI ベースの拡張機能によっては、次のディレクトリのような一般的なテンプレートの場所にテンプレートが展開されます。

- **\<Visual Studio installation directory>\Common7\IDE \\<projecttemplates/ItemTemplates\>**

- **\<Visual Studio installation directory>\Common7\IDE\Extensions \\<ExtensionName \> \\<プロジェクト/itemtemplates\>**

拡張機能で MSI ベースの展開を実行する場合は、手動でテンプレートマニフェストを生成し、拡張機能のセットアップに含まれていることを確認する必要があります。 上に示した vstman の例と、 [Visual Studio のテンプレートマニフェストスキーマのリファレンス](../extensibility/visual-studio-template-manifest-schema-reference.md)を比較します。

プロジェクトテンプレートと項目テンプレートに個別のマニフェストを作成し、上記のようにルートテンプレートディレクトリをポイントする必要があります。 拡張機能とロケールごとに1つのマニフェストを作成します。

## <a name="see-also"></a>こちらもご覧ください

- [テンプレート検出のトラブルシューティング](troubleshooting-template-discovery.md)
- [カスタムプロジェクトテンプレートと項目テンプレートの作成](creating-custom-project-and-item-templates.md)
