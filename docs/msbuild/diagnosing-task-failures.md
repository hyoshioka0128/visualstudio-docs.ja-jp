---
title: タスク エラーの診断 | Microsoft Docs
description: 失敗したタスク、ツール名、およびその他の情報を特定して、MSBuild タスクの失敗を診断する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 09/25/2019
ms.topic: troubleshooting
f1_keywords:
- MSBuild.ToolTask.ToolCommandFailed
dev_langs:
- VB
- CSharp
- C++
- jsharp
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eaf55cc529be8fc61e05d1a76096e26d965aa136
ms.sourcegitcommit: bd9417123c6ef67aa2215307ba5eeec511e43e02
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92796473"
---
# <a name="diagnosing-task-failures"></a>タスク エラーの診断

`MSB6006` は、タスクによって具体的なエラーがログに記録されなかった場合に、0 以外の終了コードを返すツール プロセスを <xref:Microsoft.Build.Utilities.ToolTask> 派生クラスが実行するときに生成されます。

## <a name="identifying-the-failing-task"></a>失敗したタスクの特定

タスク エラーが発生した場合は、最初の手順として、失敗しているタスクを特定します。

エラーのテキストには、ツール名 (タスクの <xref:Microsoft.Build.Utilities.ToolTask.ToolName> の実装で指定されたフレンドリ名、または実行可能ファイルの名前) と、数値の終了コードが記載されています。 たとえば、次のようになります。

```text
error MSB6006: "custom tool" exited with code 1.
```

ツール名は `custom tool`、終了コードは `1` です。

### <a name="command-line-builds"></a>コマンドライン ビルド

概要を含めるようにビルドが構成されている場合 (既定値)、その概要は次のようになります。

```text
Build FAILED.

"S:\MSB6006_demo\MSB6006_demo.csproj" (default target) (1) ->
(InvokeToolTask target) ->
  S:\MSB6006_demo\MSB6006_demo.csproj(19,5): error MSB6006: "custom tool" exited with code 1.
```

この結果は、ファイル `S:\MSB6006_demo\MSB6006_demo.csproj` の 19 行目に定義されているタスクで、プロジェクト `S:\MSB6006_demo\MSB6006_demo.csproj` の `InvokeToolTask` というターゲットで、エラーが発生したことを示しています。

### <a name="in-visual-studio"></a>Visual Studio 内

Visual Studio のエラー一覧の列 `Project`、`File`、`Line` にも同じ情報が表示されます。

## <a name="finding-more-failure-information"></a>その他のエラー情報の検索

このエラーは、タスクによって特定のエラーがログに記録されなかった場合に生成されます。 エラーをログに記録できない問題は、多くの場合、呼び出したツールから出力されたエラー形式を理解するようにタスクが構成されていないために起こります。

通常、正常に動作するツールからは、標準出力またはエラー ストリームに何らかのコンテキスト情報またはエラー情報が出力され、タスクでは既定でこの情報がキャプチャされ、ログに記録されます。 詳細については、エラーが発生する前のログ エントリを確認してください。 この情報を保持するには、場合によっては、より高いログ レベルでビルドを再実行する必要があります。

## <a name="next-steps"></a>次のステップ

うまく行けば、ログで特定された追加のコンテキストまたはエラーから、問題の根本原因が明らかになります。

そうでない場合は、必要に応じて、失敗したタスクに入力されたプロパティと項目を調べて考えられる原因を絞り込みます。
