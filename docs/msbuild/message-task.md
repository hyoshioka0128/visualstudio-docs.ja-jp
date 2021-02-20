---
title: Message タスク | Microsoft Docs
description: ビルドの間にメッセージをログに記録する MSBuild の Message タスクのパラメーターと設定について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Message
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Message task
- Message task [MSBuild]
ms.assetid: 2293309d-42b6-46dc-9684-8c146f66bc28
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: eb2a1837210a5f36577d3bf677a4152033914f49
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99918250"
---
# <a name="message-task"></a>Message タスク

ビルド中のメッセージをログに記録します。

## <a name="parameters"></a>パラメーター

 `Message` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`Importance`|省略可能な `String` 型のパラメーターです。<br /><br /> メッセージの重要度を指定します。 このパラメーターの値には、`high`、`normal`、または `low` を指定できます。 既定値は `normal` です。|
|`Text`|省略可能な `String` 型のパラメーターです。<br /><br /> ログに記録するエラー テキスト。|

## <a name="remarks"></a>注釈

 `Message` タスクを使用すると、MSBuild プロジェクトで、ビルド処理のさまざまな段階でロガーにメッセージを発行できます。

 `Condition` パラメーターが `true` と評価されると、`Text` パラメーターの値がログに記録され、ビルド処理が継続されます。 `Condition` パラメーターが存在しない場合は、メッセージ テキストがログに記録されます。 ログ処理の詳細については、[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)に関するページを参照してください。

 既定では、登録されているすべてのロガーにメッセージが送信されます。 ロガーによって `Importance` パラメーターが解釈されます。 通常、`high` に設定されたメッセージは、ロガーの詳細度が <xref:Microsoft.Build.Framework.LoggerVerbosity> に設定されている場合に送信されます。`Minimal` 必要です。 ロガーの詳細度が <xref:Microsoft.Build.Framework.LoggerVerbosity> に設定されている場合、`low` に設定されたメッセージが送信されます。`Detailed`

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

 次のコード例は、登録されているすべてのロガーにメッセージをログ記録します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="DisplayMessages">
        <Message Text="Project File Name = $(MSBuildProjectFile)" />
        <Message Text="Project Extension = $(MSBuildProjectExtension)" />
    </Target>
    ...
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)
