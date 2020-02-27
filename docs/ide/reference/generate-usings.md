---
title: usings の生成
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
helpviewer_keywords:
- add missing usings
ms.openlocfilehash: f3b3435e10d6bb9a71fd16b9286759b136c167f4
ms.sourcegitcommit: ea5e02720d71185f8e27fbea205024371b0c7ceb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77544544"
---
# <a name="add-missing-usings-in-visual-studio"></a>Visual Studio で不足している using を追加する

このコード生成は以下に適用されます。

- C#

**概要:** コピーして貼り付けたコードに対して、必要なインポートまたは [using ディレクティブ](/dotnet/csharp/language-reference/keywords/using-directive)をすぐに追加できます。

**条件:** プロジェクトや他のソース内のさまざまな場所からコードをコピーして、それを新しいコードに貼り付けることは、一般的な方法です。 このクイック アクションによって、コピーして貼り付けたコードで不足しているインポート ディレクティブが検索され、それらを追加するように求められます。 このコード修正では、プロジェクトからプロジェクトへの参照を追加することもできます。

**理由:** クイック アクションにより必要なインポートが自動的に追加されるため、コードに必要な `using` ディレクティブを手動でコピーする必要はありません。

## <a name="add-missing-usings-refactoring"></a>不足している using の追加リファクタリング

1. 必要な `using` ディレクティブを含めずに、ファイルからコードをコピーして新しいものに貼り付けます。 その結果として発生するエラーには、コードの修正が付随します。これにより足りない `using` ディレクティブが追加されます。

    > [!NOTE]
    > この提案は **[ツール] > [オプション] > [テキスト エディター] > [C#] > [詳細] > [ディレクティブを使用する]** で有効にする必要があります。

2. Ctrl + . キーを選択します **[クイック アクションとリファクタリング]** メニューが開きます。

    ![usings の生成](media/generate-using-codefix.png)

3. **[using \<your reference\>]\(using <参照>)** を選択し、足りない参照を追加します。

    ![usings 生成の結果](media/generate-using-result.png)

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
- [.NET 開発者向けのヒント](../csharp-developer-productivity.md)
