---
title: GetOutputFileName タスク | Microsoft Docs
description: cl.exe や他のツールの出力ファイル名オプションを指定するには、MSBuild GetOutputFileName ヘルパー タスクを使用します。
ms.custom: SEO-VS-2020
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.getoutputfilename
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), GetOutputFileName task
- GetOutputFileName task (MSBuild (C++))
author: ghogen
ms.author: ghogen
ms.workload:
- multiple
ms.openlocfilehash: cb4670bb84b151332951608f7b20ef5ea44e59a3
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436783"
---
# <a name="getoutputfilename-task"></a>GetOutputFileName タスク

cl や他のツールの出力ファイル名を取得するヘルパー タスクです。これにより、出力ディレクトリのみを指定する、完全なファイル名を指定する、または何も指定しないことが可能になります。

## <a name="parameters"></a>パラメーター

以下の表では、 **GetOutputFileName** タスクのパラメーターについて説明します。

|パラメーター|説明|
|---------------|-----------------|
|**OutputExtension**|必須の **String** 型のパラメーターです。|
|**OutputFile**|省略可能な **string** 型の出力パラメーターです。|
|**[OutputPath]**|省略可能な **string** 型のパラメーターです。|
|**SourceFile**|必須の **String** 型のパラメーターです。|

## <a name="see-also"></a>関連項目

[タスク リファレンス](../msbuild/msbuild-task-reference.md)
