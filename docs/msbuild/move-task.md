---
title: Move タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Move task
- Move task [MSBuild]
ms.assetid: d1405347-1309-4f18-b565-905408093d59
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8adfa75964959e2cce61779914a52f03319ed314
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592140"
---
# <a name="move-task"></a>Move タスク
ファイルを新しい場所に移動します。

## <a name="parameters"></a>パラメーター
 `Move` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`DestinationFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ソース ファイルの移動先ファイルの一覧を指定します。 この一覧は、`SourceFiles` パラメーターに指定された一覧の内容と 1 対 1 で対応している必要があります。 つまり、`SourceFiles` に指定された最初のファイルは、`DestinationFiles` に指定された最初の場所に移動され、2 番目以降のファイルも同様に処理されます。|
|`DestinationFolder`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> ファイルの移動先ディレクトリを指定します。|
|`MovedFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 正常に移動されたアイテムが格納されます。|
|`OverwriteReadOnlyFiles`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、ファイルが読み取り専用としてマークされている場合でも、ファイルを上書きします。|
|`SourceFiles`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 移動するファイルを指定します。|

## <a name="remarks"></a>Remarks
 `DestinationFolder` パラメーターか `DestinationFiles` パラメーターのいずれかを指定する必要がありますが、両方は指定できません。 両方を指定した場合、タスクは失敗し、エラーがログに記録されます。

 `Move` タスクでは、対象ファイルに必要なフォルダーを作成します。

 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
