---
title: SetEnv タスク | Microsoft Docs
ms.date: 11/05/2018
ms.topic: reference
f1_keywords:
- vc.task.setenv
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), tasks
- SetEnv task (MSBuild (C++))
ms.assetid: fd9e4225-68cb-4608-8b27-468b0218c936
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c5df538e7eb86a20dfc06e6e6558bded577ba3d2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77632382"
---
# <a name="setenv-task"></a>SetEnv タスク

指定された環境変数の値を設定または削除します。

## <a name="parameters"></a>パラメーター

 **SetEnv** タスクのパラメーターの説明を次の表に示します。

|パラメーター|[説明]|
|---------------|-----------------|
|**Name**|必須の **String** 型のパラメーターです。<br /><br /> 環境変数の名前。|
|**OutputEnvironmentVariable**|省略可能な **String** 型の出力パラメーターです。<br /><br /> **Name** パラメーターによって指定される環境変数に割り当てられる値が含まれます。|
|**プレフィックス**|必須の `Boolean` パラメーターです。<br /><br /> `true` の場合、**Name** パラメーターによって指定される環境変数値の前に **Value** パラメーターの値を連結し、結果を環境変数に割り当てます。 `false` の場合、**Value** パラメーターの値のみを環境変数に割り当てます。|
|**Target**|省略可能な **String** 型のパラメーターです。<br /><br /> 環境変数が保存される場所を指定します。 "User" または "Machine" を指定します。<br /><br /> 詳細については、「[EnvironmentVariableTarget 列挙型](xref:System.EnvironmentVariableTarget)」をご覧ください。|
|**値**|省略可能な **String** 型のパラメーターです。<br /><br /> **Name** パラメーターによって指定される環境変数に割り当てられる値。 **Value** が空で変数が存在する場合、変数が削除されます。 変数が存在しない場合、操作が実行できなくてもエラーは発生しません。<br /><br /> 詳細については、「[Environment::SetEnvironmentVariable メソッド](xref:System.Environment.SetEnvironmentVariable%2A)」を参照してください。|

## <a name="see-also"></a>参照

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
