---
title: ZipDirectory タスク | Microsoft Docs
description: MSBuild で ZipDirectory タスクを使用して、ディレクトリのコンテンツから .zip アーカイブを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ZipDirectory
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ZipDirectory task [MSBuild]
- MSBuild, ZipDirectory task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
caps.latest.revision: 16
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d6b897a33dacdbd52beaabdd9289a010df92a85c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847883"
---
# <a name="zipdirectory-task"></a>ZipDirectory タスク

ディレクトリのコンテンツから *.zip* アーカイブを作成します。

>[!NOTE]
>`ZipDirectory` タスクは MSBuild 15.8 以降でのみ使用できます。

## <a name="parameters"></a>パラメーター

 `ZipDirectory` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`DestinationFile`|必須の <xref:Microsoft.Build.Framework.ITaskItem> パラメーター<br /><br /> 作成する *.zip* ファイルへの完全パス。|
|`Overwrite`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、対象ファイルが存在する場合は上書きされます。 既定値は `false` です。|
|`SourceDirectory`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> *.zip* アーカイブの作成元のディレクトリを指定します。|

## <a name="remarks"></a>Remarks

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

 次の例 (インポートされた *.targets* ファイルとして使用される場合) では、プロジェクトのビルド後、出力ディレクトリから *.zip* アーカイブを作成します。 `$(OutputPath)` プロパティは通常、MSBuild プロジェクト ファイルで定義されます。そのため、次のファイルをインポートするプロジェクト ファイルでは zip アーカイブ `output.zip` が生成されます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <Target Name="ZipOutputPath" AfterTargets="Build">
        <ZipDirectory
            SourceDirectory="$(OutputPath)"
            DestinationFile="$(MSBuildProjectDirectory)\output.zip" />
    </Target>

</Project>
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
