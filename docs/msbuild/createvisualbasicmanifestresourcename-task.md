---
title: CreateVisualBasicManifestResourceName タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, CreateVisualBasicManifestResourceName task
- CreateVisualBasicManifestResourceName task [MSBuild]
ms.assetid: 251c47b9-de32-414b-a138-bf45290af12e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6aa419001d2e890c87873862f0575607b31d22c2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634293"
---
# <a name="createvisualbasicmanifestresourcename-task"></a>CreateVisualBasicManifestResourceName タスク

指定した *.resx* ファイル名または他のリソースから、Visual Basic スタイルのマニフェスト名を作成します。

## <a name="parameters"></a>パラメーター

 次の表では、[CreateVisualBasicManifestResourceName タスク](../msbuild/createvisualbasicmanifestresourcename-task.md) のパラメーターについて説明します。

| パラメーター | 説明 |
| - | - |
| `ManifestResourceNames` | <xref:Microsoft.Build.Framework.ITaskItem> `[]` 型の読み取り専用出力パラメーターです。<br /><br /> 生成されたマニフェスト名です。 |
| `ResourceFiles` | 必須の `String` 型のパラメーターです。<br /><br /> Visual Basic マニフェスト名の作成元のリソース ファイルの名前。 |
| `RootNamespace` | 省略可能な `String` 型のパラメーターです。<br /><br /> 通常はプロジェクト ファイルから取得される、リソース ファイルのルート名前空間。 `null` でもかまいません。 |
| `PrependCultureAsDirectory` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、カルチャの名前がマニフェスト リソース名の直前にディレクトリ名として追加されます。 既定値は `true` です。 |
| `ResourceFilesWithManifestResourceNames` | 省略可能な `String` 型の読み取り専用の出力パラメーターです。<br /><br /> マニフェスト リソース名を含むようになったリソース ファイルの名前を返します。 |

## <a name="remarks"></a>Remarks

 [CreateVisualBasicManifestResourceName タスク](../msbuild/createvisualbasicmanifestresourcename-task.md)は、特定の *.resx* または他のリソース ファイルに割り当てる適切なマニフェスト リソース名を決定します。 このタスクは、リソース ファイルに論理名を提供した後、それをメタデータとして出力パラメーターにアタッチします。

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
