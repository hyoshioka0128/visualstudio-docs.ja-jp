---
title: プロジェクトの種類に対するマネージ パッケージ フレームワークの使用 (C#) |マイクロソフトドキュメント
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
ms.openlocfilehash: 7ca9dda0b699e0f70b0c945ab9ecfe9f9f4dcda6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704119"
---
# <a name="using-the-managed-package-framework-to-implement-a-project-type-c"></a>マネージド パッケージ フレームワークを使用したプロジェクト タイプの実装 (C#)
マネージ パッケージ フレームワーク (MPF) には、独自のプロジェクトの種類を実装するために使用または継承できる C# クラスが用意されています。 MPF は、Visual Studio が提供するプロジェクトの種類を期待するインターフェイスの多くを実装し、プロジェクトの種類の詳細を実装することに集中できます。

## <a name="using-the-mpf-project-source-code"></a>MPF プロジェクトソースコードの使用
 プロジェクト用管理パッケージ フレームワーク (MPFProj) には、新しいプロジェクト システムを作成および管理するためのヘルパー クラスが用意されています。 MPF の他のクラスとは異なり、プロジェクト クラスは Visual Studio に付属するアセンブリには含まれません。 代わりに、プロジェクト クラスは[、プロジェクト 2013 の MPF](https://github.com/tunnelvisionlabs/MPFProj10)でソース コードとして提供されます。

 VSPackage ソリューションにこのプロジェクトを追加するには、次の操作を行います。

1. MPFProj ファイルを*MPF プロジェクトディレクトリ*にダウンロードします。

2. *次*のブロックを変更します。

```
<!-- Provide a default value for $(ProjectBasePath) -->
  <PropertyGroup>
    <ProjectBasePath >MPFProjDir\Dev10\Src\CSharp</ProjectBasePath>
  </PropertyGroup>
```

1. VSPackage プロジェクトを作成します。

2. VSPackage プロジェクトをアンロードします。

3. 他`<Import>`のブロックの前に次のブロックを追加して VSPackage .csproj ファイルを編集します。

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

2. VSPackage ソリューションを閉じてから再度開きます。

3. VSPackage プロジェクトを再度開きます。 プロジェクトベースという名前の新しいディレクトリが表示されます。

4. VSPackage プロジェクトに次の参照を追加します。

     タスク.4.0

5. プロジェクトをビルドします。

## <a name="hierarchy-classes"></a>階層クラス
 次の表は、プロジェクト階層をサポートする MPFProj のクラスをまとめたものです。 詳細については、「[階層と選択](../../extensibility/internals/hierarchies-and-selection.md)」を参照してください。

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
 次の表は、ドキュメントの処理をサポートする MPF のクラスを示しています。 詳細については、「[プロジェクト項目を開くおよび保存](../../extensibility/internals/opening-and-saving-project-items.md)する 」を参照してください。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.DocumentManager`|
|`Microsoft.VisualStudio.Package.FileDocumentManager`|

## <a name="configuration-and-output-classes"></a>構成クラスと出力クラス
 次の表は、デバッグやリリースなどの複数の構成、およびプロジェクト出力のコレクションをプロジェクトの種類でサポートできるようにする MPF のクラスを示しています。 詳細については、「[構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.ConfigProvider`|
|`Microsoft.VisualStudio.Package.ProjectConfig`|
|`Microsoft.VisualStudio.Package.BuildableProjectConfig`|
|`Microsoft.VisualStudio.Package.OutputGroup`|
|`Microsoft.VisualStudio.Package.ProjectElement`|

## <a name="automation-support-classes"></a>オートメーションサポートクラス
 次の表は、オートメーションをサポートする MPF のクラスの一覧です。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.Automation.OAProject`|
|`Microsoft.VisualStudio.Package.Automation.OANavigableProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItem`|
|`Microsoft.VisualStudio.Package.Automation.OANestedProjectItem`|

## <a name="properties-classes"></a>プロパティ クラス
 次の表は、ユーザーがプロパティ ブラウザーで参照および変更できるプロパティをプロジェクトの種類に追加できるようにする、MPF のクラスを示しています。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.LocalizableProperties`|
|`Microsoft.VisualStudio.Package.NodeProperties`|
|`Microsoft.VisualStudio.Package.FileNodeProperties`|
|`Microsoft.VisualStudio.Package.ProjectNodeProperties`|
|`Microsoft.VisualStudio.Package.FolderNodeProperties`|
|`Microsoft.VisualStudio.Package.ReferenceNodeProperties`|
