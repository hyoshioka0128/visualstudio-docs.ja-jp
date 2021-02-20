---
title: GetReferenceAssemblyPaths タスク | Microsoft Docs
description: MSBuild GetReferenceAssemblyPaths タスクを使用して、さまざまなフレームワークの参照アセンブリのパスを返します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 178ef49c-5dee-405b-a14b-a37f41dc0609
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d3e0afdc7486e4337a92e3639c23c404050a84c4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99914615"
---
# <a name="getreferenceassemblypaths-task"></a>GetReferenceAssemblyPaths タスク

各種フレームワークの参照アセンブリのパスを返します。

## <a name="parameters"></a>パラメーター

 `GetReferenceAssemblyPaths` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`ReferenceAssemblyPaths`|省略可能な `String[]` 型の出力パラメーターです。<br /><br /> `TargetFrameworkMoniker` パラメーターに基づいて、パスを返します。 `TargetFrameworkMoniker` が null または空の場合、このパスは `String.Empty` になります。|
|`FullFrameworkReferenceAssemblyPaths`|省略可能な `String[]` 型の出力パラメーターです。<br /><br /> モニカーのプロファイル部分を考慮せず、`TargetFrameworkMoniker` パラメーターに基づいて、パスを返します。 `TargetFrameworkMoniker` が null または空の場合、このパスは `String.Empty` になります。|
|`TargetFrameworkMoniker`|省略可能な `String` 型のパラメーターです。<br /><br /> 参照アセンブリ パスに関連付けられているターゲット フレームワーク モニカーを指定します。|
|`RootPath`|省略可能な `String` 型のパラメーターです。<br /><br /> 参照アセンブリ パスの生成に使用するルート パスを指定します。|
|`BypassFrameworkInstallChecks`|省略可能な <xref:System.Boolean> 型のパラメーターです。<br /><br /> `true` の場合、ターゲット フレームワークに応じて、特定のランタイム フレームワークがインストールされるように既定で `GetReferenceAssemblyPaths` が実行する基本的なチェックを省略します。|
|`TargetFrameworkMonikerDisplayName`|省略可能な `String` 型の出力パラメーターです。<br /><br /> ターゲット フレームワーク モニカーの表示名を指定します。|

## <a name="remarks"></a>解説

 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)