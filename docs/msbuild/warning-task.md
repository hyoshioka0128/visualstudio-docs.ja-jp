---
title: Warning タスク | Microsoft Docs
description: MSBuild で Warning タスクを使用して、条件付きステートメントの評価に基づいてビルド中の警告をログに記録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Warning
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Warning task [MSBuild]
- MSBuild, Warning task
ms.assetid: 96ba5507-8b43-4f54-a1d7-9b15644dd56c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ce7104c08ce8f18672bf4d2df93debc3c1d19983
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93047810"
---
# <a name="warning-task"></a>Warning タスク

条件付きステートメントの評価に基づいてビルド中の警告をログに記録します。

## <a name="parameters"></a>パラメーター

 `Warning` タスクのパラメーターの説明を次の表に示します。

| パラメーター | 説明 |
|---------------| - |
| `Code` | 省略可能な `String` 型のパラメーターです。<br /><br /> 警告に関連付ける警告コード。 |
| `File` | 省略可能な `String` 型のパラメーターです。<br /><br /> 関連ファイルが存在する場合、それを指定します。 ファイルが指定されない場合、Warning タスクを含むファイルが使用されます。 |
| `HelpKeyword` | 省略可能な `String` 型のパラメーターです。<br /><br /> 警告に関連付けるヘルプ キーワード。 |
| `Text` | 省略可能な `String` 型のパラメーターです。<br /><br /> `Condition` パラメーターが `true` と評価された場合に MSBuild によってログに記録される警告テキストです。 |

## <a name="remarks"></a>注釈

 `Warning` タスクを使用すると、MSBuild プロジェクトにおいて、必要な構成やプロパティが存在していることを確認してから次のビルド手順に進むことができます。

 `Warning` タスクの `Condition` パラメーターが `true` と評価される場合、`Text` パラメーターの値がログに記録され、ビルドが引き続き実行されます。 `Condition` パラメーターが存在しない場合は、警告テキストがログに記録されます。 ログ処理の詳細については、[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)に関するページを参照してください。

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

 次のコード例では、コマンド ラインに設定されているプロパティが確認されます。 プロパティが設定されていない場合、警告イベントが生成され、`Warning` タスクの `Text` パラメーターの値がログに記録されます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="ValidateCommandLine">
        <Warning
            Text=" The 0 property was not set on the command line."
            Condition="'$(0)' == ''" />
        <Warning
            Text=" The FREEBUILD property was not set on the command line."
            Condition="'$(FREEBUILD)' == ''" />
    </Target>
    ...
</Project>
```

## <a name="see-also"></a>関連項目

- [ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
