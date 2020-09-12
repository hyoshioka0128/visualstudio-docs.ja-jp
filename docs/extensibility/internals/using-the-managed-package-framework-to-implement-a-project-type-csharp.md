---
title: プロジェクトの種類に対してマネージパッケージフレームワークを使用する (C#)
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating with MPF
- MPF projects
- managed package framework, creating projects
ms.assetid: 926de536-eead-415b-9451-f1ddc8c44630
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fca3f95780d548b4482c502f5b3eaa44005fd2e2
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90038648"
---
# <a name="using-the-managed-package-framework-to-implement-a-project-type-c"></a>マネージド パッケージ フレームワークを使用したプロジェクト タイプの実装 (C#)
Managed Package Framework (MPF) には、独自のプロジェクトの種類を実装するために使用または継承できる C# クラスが用意されています。 MPF は、Visual Studio が提供するプロジェクトの種類を想定している多くのインターフェイスを実装しているため、プロジェクトの種類の詳しい実装に専念することができます。

## <a name="using-the-mpf-project-source-code"></a>MPF プロジェクトのソースコードを使用する
 プロジェクト用の Managed Package Framework (MPFProj) には、新しいプロジェクトシステムを作成および管理するためのヘルパークラスが用意されています。 MPF の他のクラスとは異なり、プロジェクトクラスは、Visual Studio に付属しているアセンブリには含まれていません。 代わりに、プロジェクトのクラスは、 [MPF でプロジェクト2013の](https://github.com/tunnelvisionlabs/MPFProj10)ソースコードとして提供されています。

 このプロジェクトを VSPackage ソリューションに追加するには、次の手順を実行します。

1. MPFProj ファイルを *Mpfprojectdir*にダウンロードします。

2. *Mpfprojectdir*\Dev10\Src\CSharp\ProjectBase.file で、次のブロックを変更します。

```
<!-- Provide a default value for $(ProjectBasePath) -->
  <PropertyGroup>
    <ProjectBasePath >MPFProjDir\Dev10\Src\CSharp</ProjectBasePath>
  </PropertyGroup>
```

1. VSPackage プロジェクトを作成します。

2. VSPackage プロジェクトをアンロードします。

3. 他のブロックの前に次のブロックを追加して、VSPackage ファイルを編集し `<Import>` ます。

```
<Import Project="MPFProjectDir\Dev10\Src\CSharp\ProjectBase.files" />
  <PropertyGroup>
    <!--To specify a different registry root to register your package, uncomment the TargetRegistryRoot tag and specify a registry root in it.
    <TargetRegistryRoot></TargetRegistryRoot>-->
    <RegisterOutputPackage>true</RegisterOutputPackage>
    <RegisterWithCodebase>true</RegisterWithCodebase>
  </PropertyGroup>
```

1. プロジェクトを保存します。

2. VSPackage ソリューションを閉じて再度開きます。

3. VSPackage プロジェクトを再度開きます。 ProjectBase という名前の新しいディレクトリが表示できます。

4. VSPackage プロジェクトに次の参照を追加します。

     Microsoft. Build. Tasks. 4.0

5. プロジェクトをビルドします。

## <a name="hierarchy-classes"></a>階層クラス
 次の表は、プロジェクト階層をサポートする MPFProj のクラスをまとめたものです。 詳細については、「 [階層と選択](../../extensibility/internals/hierarchies-and-selection.md)」を参照してください。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.HierarchyNode`|
|`Microsoft.VisualStudio.Package.ProjectNode`|
|`Microsoft.VisualStudio.Package.ProjectContainerNode`|
|`Microsoft.VisualStudio.Package.FileNode`|
|`Microsoft.VisualStudio.Package.FolderNode`|
|`Microsoft.VisualStudio.Package.ReferenceContainerNode`|
|`Microsoft.VisualStudio.Package.ReferenceNode`|
|`Microsoft.VisualStudio.Package.ProjectReferenceNode`|
|`Microsoft.VisualStudio.Package.ComReferenceNode`|
|`Microsoft.VisualStudio.Package.AssemblyReferenceNode`|
|`Microsoft.VisualStudio.Package.BuildDependency`|

## <a name="document-handling-classes"></a>ドキュメント処理クラス
 次の表は、ドキュメントの処理をサポートする MPF のクラスを示しています。 詳細については、「 [プロジェクト項目を開いて保存](../../extensibility/internals/opening-and-saving-project-items.md)する」を参照してください。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.DocumentManager`|
|`Microsoft.VisualStudio.Package.FileDocumentManager`|

## <a name="configuration-and-output-classes"></a>構成クラスと出力クラス
 次の表に、プロジェクトの種類がデバッグとリリース、プロジェクト出力のコレクションなどの複数の構成をサポートする MPF のクラスを示します。 詳細については、「 [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.ConfigProvider`|
|`Microsoft.VisualStudio.Package.ProjectConfig`|
|`Microsoft.VisualStudio.Package.BuildableProjectConfig`|
|`Microsoft.VisualStudio.Package.OutputGroup`|
|`Microsoft.VisualStudio.Package.ProjectElement`|

## <a name="automation-support-classes"></a>オートメーション-サポートクラス
 次の表に、プロジェクトの種類のユーザーがアドインを記述できるように、自動化をサポートする MPF のクラスを示します。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.Automation.OAProject`|
|`Microsoft.VisualStudio.Package.Automation.OANavigableProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItem`|
|`Microsoft.VisualStudio.Package.Automation.OANestedProjectItem`|

## <a name="properties-classes"></a>Properties クラス
 次の表に、ユーザーがプロパティブラウザーで参照および変更できるプロパティをプロジェクトの種類で追加できるようにする、MPF 内のクラスの一覧を示します。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.LocalizableProperties`|
|`Microsoft.VisualStudio.Package.NodeProperties`|
|`Microsoft.VisualStudio.Package.FileNodeProperties`|
|`Microsoft.VisualStudio.Package.ProjectNodeProperties`|
|`Microsoft.VisualStudio.Package.FolderNodeProperties`|
|`Microsoft.VisualStudio.Package.ReferenceNodeProperties`|
