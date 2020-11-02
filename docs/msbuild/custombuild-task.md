---
title: CustomBuild タスク | Microsoft Docs
description: この記事では、MSBuild で C++ ビルド プロセスのカスタマイズをサポートするために使用する、MSBuild CustomBuild タスクについて説明します。
ms.custom: SEO-VS-2020
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.custombuild
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), CustomBuild task
- CustomBuild task (MSBuild (C++))
author: ghogen
ms.author: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 640c1e6ae286b45f8700709829140093452a9491
ms.sourcegitcommit: bd9417123c6ef67aa2215307ba5eeec511e43e02
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92796551"
---
# <a name="custombuild-task"></a>CustomBuild タスク

Microsoft C++ コンパイラ ツール cmd.exe をラップします。 このクラスは [TrackedVCToolTask](../msbuild/trackedvctooltask-base-class.md) から派生しますが、ファイルの依存関係を見つける目的でファイル追跡が利用されることはありません。 インクリメント ビルドが正しく動作するには、依存関係をすべて AdditionalDependencies として明示的に指定する必要があります。

## <a name="parameters"></a>パラメーター

以下の表では、 **CustomBuild** タスクのパラメーターについて説明します。

|パラメーター|説明|
|---------------|-----------------|
|**BuildSuffix**|省略可能な **string** 型のパラメーターです。|
|**Sources**|必須の **ITaskItem[]** 型のパラメーターです。|
|**TrackerLogDirectory**|省略可能な **string** 型のパラメーターです。|

## <a name="see-also"></a>関連項目

[タスク リファレンス](../msbuild/msbuild-task-reference.md)
