---
title: UpdateManifest タスク| Microsoft Docs
description: MSBuild で UpdateManifest タスクを使用して、マニフェスト内の選択したプロパティを更新して再署名する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, UpdateManifest task
- UpdateManifest task [MSBuild]
ms.assetid: 1291fd33-b89e-4e15-8fb1-69f9625cf2d2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4fab3844b21e12edceb83da310e9069199578ef6
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93046852"
---
# <a name="updatemanifest-task"></a>UpdateManifest タスク

マニフェスト内の選択したプロパティを更新し、再署名します。

## <a name="parameters"></a>パラメーター

 `UpdateManifest` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`ApplicationManifest`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> アプリケーション マニフェストを指定します。|
|`ApplicationPath`|必須の `String` 型のパラメーターです。<br /><br /> アプリケーション マニフェストのパスを指定します。|
|`InputManifest`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> 更新するマニフェストを指定します。|
|`OutputManifest`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型の出力パラメーターです。<br /><br /> 更新されたプロパティを含むマニフェストを指定します。|

## <a name="remarks"></a>注釈

 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Utilities.Task> クラスからパラメーターを継承します。 これらの追加パラメーターのリストとその説明については、「[Task 基底クラス](../msbuild/task-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)