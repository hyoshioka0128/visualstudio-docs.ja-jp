---
title: FormatUrl タスク | Microsoft Docs
description: MSBuild FormatUrl タスクを使用して、入力 URL を正しい出力 URL 形式に変換する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, FormatUrl task
- FormatUrl task [MSBuild]
ms.assetid: 81114b67-520f-43b5-8891-224f68a78516
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a9a05ce16289c012b067faa5bc302a3921cbe1c7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888096"
---
# <a name="formaturl-task"></a>FormatUrl タスク

URL を正しい URL 書式に変換します。

## <a name="parameters"></a>パラメーター

 `FormatUrl` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`InputUrl`|省略可能な `String` 型のパラメーターです。<br /><br /> 書式設定する URL を指定します。|
|`OutputUrl`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 書式設定された URL を指定します。|

## <a name="remarks"></a>解説

 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)