---
title: Exec タスク | Microsoft Docs
description: MSBuild Exec タスクを使用し、指定した引数を使用して指定したプログラムまたはコマンドを実行する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Exec
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Exec task [MSBuild]
- MSBuild, Exec task
ms.assetid: c9b7525a-b1c9-40fc-8bce-77a5b8f960d8
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99475ac316112f29a73a85b8ff92249a13867852
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436728"
---
# <a name="exec-task"></a>Exec タスク

指定された引数を使って、指定されたプログラムまたはコマンドを実行します。

## <a name="parameters"></a>パラメーター

`Exec` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`Command`|必須の `String` 型のパラメーターです。<br /><br /> 実行するコマンドです。 attrib などのシステム コマンド、または *program.exe* 、 *runprogram.bat* 、 *setup.msi* などの実行可能ファイルを指定できます。<br /><br /> このパラメーターで複数のコマンド行を指定できます。 または、複数のコマンドをバッチ ファイルに入れ、このパラメーターを使ってそれを実行することもできます。|
|`ConsoleOutput`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 各項目出力は、ツールによって生成される標準出力または標準エラー ストリームの行です。 これは、`ConsoleToMsBuild` が `true` に設定されている場合にのみキャプチャされます。|
|`ConsoleToMsBuild`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、タスクは、ツールの標準エラーと標準出力をキャプチャして、`ConsoleOutput` 出力パラメーターで利用できるようにします。<br /><br />既定値:`false`。|
|`CustomErrorRegularExpression`|省略可能な `String` 型のパラメーターです。<br /><br /> ツールの出力でエラー行を示すために使う正規表現を指定します。 これは、普通とは異なる書式設定の出力を生成するツールに便利です。<br /><br />既定値: `null` (カスタム処理はありません)。|
|`CustomWarningRegularExpression`|省略可能な `String` 型のパラメーターです。<br /><br /> ツールの出力で警告行を示すために使う正規表現を指定します。 これは、普通とは異なる書式設定の出力を生成するツールに便利です。<br /><br />既定値: `null` (カスタム処理はありません)。|
|`EchoOff`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、タスクは `Command` の拡張形式を MSBuild ログに出力しません。<br /><br />既定値:`false`。|
|`ExitCode`|省略可能な `Int32` 型の読み取り専用出力パラメーターです。<br /><br /> 実行したコマンドから返される終了コードを指定します。ただし、タスクによってエラーが記録され、プロセスの終了コードが 0 (成功) の場合、`ExitCode` は -1 に設定されます。|
|`IgnoreExitCode`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、タスクは実行したコマンドで提供されている終了コードを無視します。 それ以外の場合、実行されたコマンドが 0 以外の終了コードを返すときは、タスクは `false` を返します。<br /><br />既定値:`false`。|
|`IgnoreStandardErrorWarningFormat`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `false` の場合は、標準エラー/警告の形式に一致する出力行を選び、エラー/警告としてログに記録します。 `true` の場合は、この動作は無効になります。<br /><br />既定値:`false`。|
|`Outputs`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> タスクからの出力項目を含みます。 `Exec` タスク自体はこれらを設定しません。 代わりに、タスクが設定したかのようにユーザーが提供して、プロジェクトの後の処理で使うことができます。|
|`StdErrEncoding`|省略可能な `String` 型の出力パラメーターです。<br /><br /> キャプチャしたタスクの標準エラー ストリームのエンコーディングを指定します。 既定値は、現在のコンソール出力のエンコーディングです。|
|`StdOutEncoding`|省略可能な `String` 型の出力パラメーターです。<br /><br /> キャプチャしたタスクの標準出力ストリームのエンコーディングを指定します。 既定値は、現在のコンソール出力のエンコーディングです。|
|`WorkingDirectory`|省略可能な `String` 型のパラメーターです。<br /><br /> コマンドを実行するディレクトリを指定します。<br /><br />既定:プロジェクトの現在の作業ディレクトリ。|

[!INCLUDE [ToolTaskExtension arguments](includes/tooltaskextension-base-params.md)]

## <a name="remarks"></a>Remarks

このタスクは、実行したいジョブの特定の MSBuild タスクを使用できないときに便利です。 ただし、`Exec` タスクは、固有のタスクとは異なり、実行したツールまたはコマンドの結果に基づいて追加処理や条件演算を行うことはできません。

`Exec` タスクは、プロセスを直接呼び出す代わりに *cmd.exe* を呼び出します。

## <a name="example"></a>例

次の例では、`Exec` タスクを使ってコマンドを実行します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <Binaries Include="*.dll;*.exe"/>
    </ItemGroup>

    <Target Name="SetACL">
        <!-- set security on binaries-->
        <Exec Command="echo y| cacls %(Binaries.Identity) /G everyone:R"/>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
