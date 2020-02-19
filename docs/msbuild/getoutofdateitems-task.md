---
title: GetOutOfDateItems タスク | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.getoutofdateitems
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), GetOutOfDateItems task
- GetOutOfDateItems task (MSBuild (C++))
author: corob-msft
ms.author: corob
ms.workload:
- multiple
ms.openlocfilehash: bfa60ff0f7e4060f5725fe54bd5950d858b86a22
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77272392"
---
# <a name="getoutofdateitems-task"></a>GetOutOfDateItems タスク

古い tlog を読み取り、新しい tlog 書き込んで、最新ではない項目のセットを返すヘルパー タスクです。

## <a name="parameters"></a>パラメーター

以下の表では、**GetOutOfDateItems** タスクのパラメーターについて説明します。

|パラメーター|説明|
|---------------|-----------------|
|**CheckForInterdependencies**|省略可能な **bool** 型のパラメーターです。|
|**CommandMetadataName**|省略可能な **string** 型のパラメーターです。|
|**DependenciesMetadataName**|省略可能な **string** 型のパラメーターです。|
|**HasInterdependencies**|省略可能な **bool** 型の出力パラメーターです。|
|**OutOfDateSources**|省略可能な **ITaskItem[]** 型の出力パラメーターです。|
|**OutputsMetadataName**|必須の **String** 型のパラメーターです。|
|**Sources**|省略可能な **ITaskItem[]** パラメーターです。|
|**TLogDirectory**|必須の **String** 型のパラメーターです。|
|**TLogNamePrefix**|必須の **String** 型のパラメーターです。|

## <a name="see-also"></a>関連項目

[タスク リファレンス](../msbuild/msbuild-task-reference.md)