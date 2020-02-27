---
title: MSBuild プロジェクト ファイル スキーマ リファレンス | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, file schema
ms.assetid: d9a68146-1f43-4621-ac78-2c8c3f400936
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c4a0ef3fc6fe446ccda5479c95301d71efa84be4
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557805"
---
# <a name="msbuild-project-file-schema-reference"></a>MSBuild プロジェクト ファイル スキーマ リファレンス

[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] XML スキーマのすべての要素と、使用可能な属性および子要素をまとめた表を提供します。

 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] はプロジェクト ファイルを使用して、ビルド エンジンに何をどのようにビルドするかを指示します。 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロジェクト ファイルは、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] XML スキーマに準拠した XML ファイルです。 このセクションでは、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] の XML スキーマ定義 ( *.xsd*) ファイルについて説明します。

MSBuild プロジェクト ファイルのスキーマ リンクは、Visual Studio 2017 以降では必要ありません。 存在する場合は、Visual Studio のバージョンに関係なく ` http://schemas.microsoft.com/developer/msbuild/2003` である必要があります。

## <a name="msbuild-xml-schema-elements"></a>MSBuild XML スキーマの要素

 次の表に、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] XML スキーマのすべての要素、および子要素と属性を示します。

|要素|子要素|属性|
|-------------|--------------------|----------------|
|[Choose 要素 (MSBuild)](../msbuild/choose-element-msbuild.md)|Otherwise<br /><br /> When|--|
|[Import 要素 (MSBuild)](../msbuild/import-element-msbuild.md)|--|条件<br /><br /> Project|
|[ImportGroup 要素](../msbuild/importgroup-element.md)|インポート|条件|
|[Item 要素 (MSBuild)](../msbuild/item-element-msbuild.md)|*ItemMetaData*|条件<br /><br /> 除外<br /><br /> 包含<br /><br /> 削除|
|[ItemDefinitionGroup 要素 (MSBuild)](../msbuild/itemdefinitiongroup-element-msbuild.md)|*Item*|条件|
|[ItemGroup 要素 (MSBuild)](../msbuild/itemgroup-element-msbuild.md)|*Item*|条件|
|[ItemMetadata 要素 (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)|*Item*|条件|
|[OnError 要素 (MSBuild)](../msbuild/onerror-element-msbuild.md)|--|条件<br /><br /> ExecuteTargets|
|[Otherwise 要素 (MSBuild)](../msbuild/otherwise-element-msbuild.md)|Choose<br /><br /> ItemGroup<br /><br /> PropertyGroup|--|
|[Output 要素 (MSBuild)](../msbuild/output-element-msbuild.md)|--|条件<br /><br /> ItemName<br /><br /> PropertyName<br /><br /> TaskParameter|
|[Parameter 要素](../msbuild/parameter-element.md)|--|Output<br /><br /> ParameterType<br /><br /> 必須|
|[ParameterGroup 要素](../msbuild/parametergroup-element.md)|*パラメーター*|--|
|[Project 要素 (MSBuild)](../msbuild/project-element-msbuild.md)|Choose<br /><br /> インポート<br /><br /> ItemGroup<br /><br /> ProjectExtensions<br /><br /> PropertyGroup<br /><br /> ターゲット<br /><br /> UsingTask|DefaultTargets<br /><br /> InitialTargets<br /><br /> ToolsVersion<br /><br /> TreatAsLocalProperty<br /><br /> xmlns|
|[ProjectExtensions 要素 (MSBuild)](../msbuild/projectextensions-element-msbuild.md)|--|--|
|[Property 要素 (MSBuild)](../msbuild/property-element-msbuild.md)|--|条件|
|[PropertyGroup 要素 (MSBuild)](../msbuild/propertygroup-element-msbuild.md)|*Property*|条件|
|[Sdk 要素 (MSBuild)](../msbuild/sdk-element-msbuild.md)|--|名前<br /><br /> バージョン|
|[Target 要素 (MSBuild)](../msbuild/target-element-msbuild.md)|OnError<br /><br /> *タスク*|AfterTargets<br /><br /> BeforeTargets<br /><br /> 条件<br /><br /> DependsOnTargets<br /><br /> 受け取る値<br /><br /> KeepDuplicateOutputs<br /><br /> 名前<br /><br /> 出力<br /><br /> 戻り値|
|[Task 要素 (MSBuild)](../msbuild/task-element-msbuild.md)|Output|条件<br /><br /> ContinueOnError<br /><br /> *パラメーター*|
|[TaskBody 要素 (MSBuild)](../msbuild/taskbody-element-msbuild.md)|*データ*|評価|
|[UsingTask 要素 (MSBuild)](../msbuild/usingtask-element-msbuild.md)|ParameterGroup<br /><br /> TaskBody|AssemblyFile<br /><br /> AssemblyName<br /><br /> 条件<br /><br /> TaskFactory<br /><br /> TaskName|
|[When 要素 (MSBuild)](../msbuild/when-element-msbuild.md)|Choose<br /><br /> ItemGroup<br /><br /> PropertyGroup|条件|

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [条件](../msbuild/msbuild-conditions.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [MSBuild](../msbuild/msbuild.md)
