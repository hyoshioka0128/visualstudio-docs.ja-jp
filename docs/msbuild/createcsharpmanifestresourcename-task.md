---
title: CreateCSharpManifestResourceName タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, CreateCSharpManifestResourceName task
- CreateCSharpManifestResourceName task [MSBuild]
ms.assetid: 2ace88c1-d757-40a7-8158-c1d3f5ff0511
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1b3c4b49e6e3df2ef0fcac978566e8656ab78ab
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596061"
---
# <a name="createcsharpmanifestresourcename-task"></a>CreateCSharpManifestResourceName タスク
指定した *.resx* ファイル名または他のリソースから [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] スタイルのマニフェスト名を作成します。

## <a name="parameters"></a>パラメーター
 次の表では、[CreateCSharpManifestResourceName タスク](../msbuild/createcsharpmanifestresourcename-task.md)のパラメーターについて説明します。

| パラメーター | 説明 |
| - | - |
| `ManifestResourceNames` | <xref:Microsoft.Build.Framework.ITaskItem> `[]` 型の読み取り専用出力パラメーターです。<br /><br /> 生成されたマニフェスト名です。 |
| `ResourceFiles` | 必須の `String` 型のパラメーターです。<br /><br /> [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] マニフェスト名の作成元のリソース ファイルの名前。 |
| `RootNamespace` | 省略可能な `String` 型のパラメーターです。<br /><br /> 通常はプロジェクト ファイルから取得される、リソース ファイルのルート名前空間。 `null` でもかまいません。 |
| `PrependCultureAsDirectory` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、カルチャの名前がマニフェスト リソース名の直前にディレクトリ名として追加されます。 既定値は `true` です。 |
| `ResourceFilesWithManifestResourceNames` | 省略可能な `String` 型の読み取り専用の出力パラメーターです。<br /><br /> マニフェスト リソース名を含むようになったリソース ファイルの名前を返します。 |

## <a name="remarks"></a>Remarks
 [CreateVisualBasicManifestResourceName タスク](../msbuild/createvisualbasicmanifestresourcename-task.md)は、特定の *.resx* または他のリソース ファイルに割り当てる適切なマニフェスト リソース名を決定します。 このタスクは、リソース ファイルに論理名を提供した後、それをメタデータとして出力パラメーターにアタッチします。

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
