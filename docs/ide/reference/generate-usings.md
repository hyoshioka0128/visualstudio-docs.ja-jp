---
title: usings の生成
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
helpviewer_keywords:
- add missing usings
ms.openlocfilehash: 903b160bac0e8096062e09fd78ff4c92c46cf8ee
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094315"
---
# <a name="add-missing-usings-in-visual-studio"></a>Visual Studio で不足している using を追加する

このコード生成は以下に適用されます。

- C#

- Visual Basic

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
