---
title: FindAppConfigFile タスク | Microsoft Docs
description: MSBuild FindAppConfigFile タスクを使用して、指定されたリスト内で app.config ファイル (存在する場合) を検索する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- FindAppConfigFile task [MSBuild]
- MSBuild, FindAppConfigFile task
ms.assetid: e292de3e-7482-4426-83ce-d921061808bf
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d186a72bcc7af18671c279ff392de066b6fd9fee
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92435683"
---
# <a name="findappconfigfile-task"></a>FindAppConfigFile タスク

指定したリスト内で *app.config* ファイルを検索します。

## <a name="parameters"></a>パラメーター

 `FindAppConfigFile` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`AppConfigFile`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 存在する場合、リスト内で最初に見つかった一致する項目を指定します。|
|`PrimaryList`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 第一に検索する一覧を指定します。|
|`SecondaryList`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 第二に検索する一覧を指定します。|
|`TargetPath`|必須の `String` 型のパラメーターです。<br /><br /> メタデータとして追加する値を指定します。|

## <a name="remarks"></a>解説

 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
