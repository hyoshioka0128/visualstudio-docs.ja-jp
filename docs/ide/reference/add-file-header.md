---
title: ファイル ヘッダーを追加する
ms.date: 07/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 2c69f73989e898c44bdef6cf008d48f6c918652a
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801322"
---
# <a name="add-file-header"></a>ファイル ヘッダーを追加する

このコード生成は以下に適用されます。

- C#

- Visual Basic

**概要:** [EditorConfig](https://docs.microsoft.com/visualstudio/ide/create-portable-custom-editor-options#add-an-editorconfig-file-to-a-project) を使用して、既存のファイル、プロジェクト、およびソリューションにファイル ヘッダーを追加します。

**条件:** ファイル、プロジェクト、およびソリューションにファイル ヘッダーを簡単に追加したいとき。

**理由:** チームにより、著作権のためにファイル ヘッダーを含めることが要求されています。 

## <a name="how-to"></a>方法

1. プロジェクトまたはソリューションに [EditorConfig](https://docs.microsoft.com/visualstudio/ide/create-portable-custom-editor-options#add-an-editorconfig-file-to-a-project) を追加します (まだ作成していない場合)。

2. お使いの EditorConfig ファイルに次の規則を追加します: *file_header_template*。

3. 適用するヘッダー テキストと同じ規則の値を設定します。 ファイル名のプレースホルダーとして `{fileName}` を使用できます。

    ![EditorConfig ファイル ヘッダー規則](media/add-file-header-rule.png)

    > [!NOTE]
    > EditorConfig に複数行を明示的に含めることはできません。新しい行を挿入するには、Unix の改行文字を使用する必要があります。

4. C# または Visual Basic ファイルの最初の行にキャレットを置きます。

5. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

6. **[ファイル ヘッダーを追加する]** を選択します。 

    ![EditorConfig ファイル ヘッダー規則](media/add-file-header.png)

7. ファイル ヘッダーをプロジェクトまたはソリューション全体に適用する場合は、 **[次の場所のすべての出現箇所を修正します]** オプションで **[プロジェクト]** または **[ソリューション]** を選択します。

8. **[すべての出現箇所を修正します]** ダイアログが開き、変更をプレビューできます。

    ![[すべての出現箇所を修正します] ダイアログ](media/file-header-preview-changes.png)

8. **[適用]** を選択して変更を適用します。

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
