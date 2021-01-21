---
title: Error タスク | Microsoft ドキュメント
description: MSBuild Error タスクを使用して、ビルドを停止し、条件付きステートメントの評価に基づいてエラーをログに記録します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Error
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Error task [MSBuild]
- MSBuild, Error task
ms.assetid: e96a90ee-a8ae-4e5b-8ef2-b5cf5fedd8b2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a2b451f9c3074af7d621576336ea3bf0e05ebea3
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436646"
---
# <a name="error-task"></a>Error タスク

ビルドを停止し、条件付きステートメントの評価に基づいてエラーをログに記録します。

## <a name="parameters"></a>パラメーター

`Error` タスクのパラメーターの説明を次の表に示します。

| パラメーター | 説明 |
|---------------| - |
| `Code` | 省略可能な `String` 型のパラメーターです。<br /><br /> エラーに関連付けるエラー コード。 |
| `File` | 省略可能な `String` 型のパラメーターです。<br /><br /> エラーが含まれているファイルの名前。 ファイル名が指定されていない場合は、Error タスクを含むファイルが使用されます。 |
| `HelpKeyword` | 省略可能な `String` 型のパラメーターです。<br /><br /> エラーに関連付けるヘルプ キーワード。 |
| `Text` | 省略可能な `String` 型のパラメーターです。<br /><br /> `Condition` パラメーターが `true` と評価された場合に MSBuild によってログに記録されるエラー テキストです。 |

## <a name="remarks"></a>解説

`Error` タスクにより、MSBuild プロジェクトはロガーに対してエラー テキストを発行し、ビルドの実行を中断することができます。

`Condition` パラメーターが `true` と評価されると、ビルドを中止し、ログにエラーを記録します。 `Condition` パラメーターが存在しない場合には、エラーがログ記録され、ビルドの実行が中止されます。 ログ処理の詳細については、[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)に関するページを参照してください。

上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

次のコード例では、すべての必須のプロパティが設定されていることを検証します。 該当するプロパティが設定されていない場合、`Error` タスクの `Text` パラメーターの値をログに記録します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="ValidateCommandLine">
        <Error
            Text=" The 0 property must be set on the command line."
            Condition="'$(0)' == ''" />
        <Error
            Text="The FREEBUILD property must be set on the command line."
            Condition="'$(FREEBUILD)' == ''" />
    </Target>
    ...
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)
