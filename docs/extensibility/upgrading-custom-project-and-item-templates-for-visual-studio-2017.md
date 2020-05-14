---
title: Visual Studio 2017 のカスタム プロジェクトテンプレートと項目テンプレートをアップグレードする
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ad02477b-e101-4f32-aeb7-292bf95d5c2f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 5f807e142b376d05e5a44600e8f6b24ddb3593be
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698859"
---
# <a name="upgrade-custom-project-and-item-templates-for-visual-studio-2017"></a>Visual Studio 2017 のカスタム プロジェクトテンプレートと項目テンプレートをアップグレードする

Visual Studio 2017 以降では、以前のバージョンの Visual Studio とは異なる方法で .vsix または .msi によってインストールされたプロジェクトと項目のテンプレートが検出されます。 カスタム プロジェクトまたは項目テンプレートを使用する拡張機能を所有している場合は、拡張機能を更新する必要があります。 この記事では、実行する必要がある操作について説明します。

この変更は、Visual Studio 2017 にのみ影響します。 これは、以前のバージョンの Visual Studio には影響しません。

VSIX 拡張機能の一部としてプロジェクトまたは項目テンプレートを作成する場合は、「[カスタム プロジェクトテンプレートおよび項目テンプレートの作成](../extensibility/creating-custom-project-and-item-templates.md)」を参照してください。

## <a name="template-scanning"></a>テンプレートスキャン

以前のバージョンの Visual Studio では **、devenv /setup**または**devenv /installvstemplates**がローカル ディスクをスキャンしてプロジェクトテンプレートと項目テンプレートを検索しました。 Visual Studio 2017 以降では、スキャンはユーザー レベルの場所に対してのみ実行されます。 既定のユーザー レベルの場所は **、Visual Studio\\バージョン\>\テンプレート\\<ドキュメント**です。 この場所は、ウィザードで [**テンプレートを自動的に Visual Studio にインポート**する] オプションが選択されている場合に、[**プロジェクト** > エクスポート**テンプレート.**

その他の (ユーザー以外の) 場所の場合は、マニフェスト (.vstman) ファイルを含める必要があります。 .vstman ファイルは、テンプレートに使用される .vstemplate ファイルと共に生成されます。 .vsix を使用して拡張機能をインストールする場合は、Visual Studio 2017 で拡張機能を再コンパイルすることでこれを実現できます。 ただし、.msi を使用する場合は、手動で変更する必要があります。 これらの変更を行うために必要な操作の一覧については、「**と共にインストールされる拡張機能のアップグレード」を参照してください。この**ページの後半で MSI を説明します。

## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>プロジェクトまたは項目テンプレートを使用して VSIX 拡張機能を更新する方法

1. ソリューションを Visual Studio 2017 で開きます。 コードのアップグレードを求められます。 **[OK]** をクリックします。

2. アップグレードが完了した後、インストールターゲットのバージョンを変更する必要がある場合があります。 VSIX プロジェクトで、source.extension.vsixmanifest ファイルを開き、[**ターゲットのインストール**] タブを選択します。**[バージョン範囲**] フィールドが **[14.0] の**場合は、[**編集**] をクリックし、Visual Studio 2017 を含むように変更します。 たとえば **、[14.0,15.0]** に設定して拡張機能を Visual Studio 2015 または Visual Studio 2017 にインストールするか **、[15.0]** に設定して Visual Studio 2017 にインストールできます。

3. コードを再コンパイルします。

4. Visual Studio を閉じます。

5. VSIX をインストールします。

6. 次の手順を実行して、更新プログラムをテストできます。

    1. ファイル スキャンの変更は、次のレジストリ キーによってアクティブ化されます。

         **reg 追加 hklm\ソフトウェア\マイクロソフト\ビジュアルスタジオ\15.0\VSテンプレート /v テンプレートスキャンを無効にする /t REG_DWORD /d 1 /reg:32**

    2. キーを追加したら **、devenv /installvstemplates**を実行します。

    3. Visual Studio を再度開きます。 テンプレートは、期待される場所に見つかります。

    > [!NOTE]
    > Visual Studio の機能拡張プロジェクト テンプレートは、レジストリ キーが存在する場合は使用できません。 レジストリ キーを削除し、それらを使用するには **、devenv /installvstemplates**を再実行する必要があります。

## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>プロジェクト テンプレートおよび項目テンプレートを配置するためのその他の推奨事項

- 圧縮されたテンプレート ファイルは使用しないでください。 圧縮されたテンプレート ファイルは、リソースとコンテンツを取得するために圧縮を解除する必要があるため、使用コストが高くなります。 代わりに、プロジェクトテンプレートと項目テンプレートを個別のファイルとして独自のディレクトリに配置して、テンプレートの初期化を高速化する必要があります。 VSIX 拡張機能の場合、SDK ビルド タスクは、VSIX ファイルの作成中に、zip 形式のテンプレートを自動的に解凍します。

- テンプレートの検出中に不要なリソース アセンブリの読み込みを回避するために、テンプレート名、説明、アイコン、またはプレビューにパッケージ/リソース ID エントリを使用しないようにします。 代わりに、ローカライズされたマニフェストを使用して、ローカライズされた名前またはプロパティを使用する各ロケールのテンプレート エントリを作成できます。

- テンプレートをファイル項目として含める場合、マニフェストの生成によって期待どおりの結果が得られるとは限りません。 その場合は、VSIX プロジェクトに手動で生成されたマニフェストを追加する必要があります。

## <a name="file-changes-in-project-and-item-templates"></a>プロジェクトテンプレートおよび項目テンプレートのファイルの変更
Visual Studio 2015 と Visual Studio 2017 のバージョンのテンプレート ファイルの違いのポイントを示して、新しいファイルを正しく作成できるようにします。

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

 VSIX プロジェクトの再構築に起因する .vstman ファイル (VSIX プロジェクトのマニフェスト ディレクトリにあります) は次のとおりです。

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

 [要素](../extensibility/templatedata-element-visual-studio-templates.md)によって提供される情報は変わりません。 ** \<VSTemplateContainer 要素>** 関連付けられたテンプレートの .vstemplate ファイルを指します。

 Visual Studio 2015 によって作成された既定の項目 .vstemplate ファイルを次に示します。

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

 VSIX プロジェクトの再構築に起因する .vstman ファイル (VSIX プロジェクトのマニフェスト ディレクトリにあります) は次のとおりです。

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

 ** \<TemplateData>** 要素によって提供される情報は変わりません。 **\<要素が**関連付けられたテンプレートの .vstemplate ファイルを指す VSTemplateContainer>

 .vstman ファイルのさまざまな要素の詳細については、「 Visual Studio テンプレート マニフェスト スキーマ リファレンス 」を[参照してください](../extensibility/visual-studio-template-manifest-schema-reference.md)。

## <a name="upgrades-for-extensions-installed-with-an-msi"></a>拡張のアップグレードがインストールされている.Msi

一部の MSI ベースの拡張機能では、テンプレートを次のディレクトリなどの一般的なテンプレートの場所に配置します。

- **\<Visual Studio のインストール ディレクトリ>\Common7\IDE\\<プロジェクト テンプレート/項目テンプレート\>**

- **\<Visual Studio のインストール ディレクトリ>\Common7\IDE\拡張機能\\<プロジェクト/アイテム テンプレート<名前\>\\\>**

拡張機能が MSI ベースの配置を実行する場合は、テンプレート マニフェストを手動で生成し、拡張セットアップに含まれていることを確認する必要があります。 上記の .vstman の例と[Visual Studio テンプレート マニフェスト スキーマ リファレンス](../extensibility/visual-studio-template-manifest-schema-reference.md)を比較します。

プロジェクトテンプレートと項目テンプレート用に個別のマニフェストを作成し、上で指定したルートテンプレートディレクトリを指定する必要があります。 拡張およびロケールごとに 1 つのマニフェストを作成します。

## <a name="see-also"></a>関連項目

- [テンプレート検出のトラブルシューティング](troubleshooting-template-discovery.md)
- [カスタム プロジェクトテンプレートと項目テンプレートの作成](creating-custom-project-and-item-templates.md)
