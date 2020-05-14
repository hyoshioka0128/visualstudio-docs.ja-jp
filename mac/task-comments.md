---
title: タスク コメント
description: コードにタスク コメントを追加する
author: cobey
ms.author: cobey
ms.date: 05/06/2018
ms.assetid: 562DCB46-D8FA-4DC4-AAEA-F274448C4CD2
ms.openlocfilehash: d88b74ab953f97e061f4be3befc227646006f38b
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "67692325"
---
# <a name="task-comments"></a>タスク コメント

コードを記述する場合、完了していないコード、問題があるコード、警告の簡単な回避策などをコメントで明示的に示すのは標準的な方法です。 Visual Studio for Mac に用意されている既定の指示トークンは、TODO、HACK、FIXME、および UNDONE です。 カスタマイズしたトークンは、次の図のように、 **[Visual Studio]、[ユーザー設定]、[環境]、[タスク]** の順に選択して定義できます。

![タスク一覧のユーザー設定](media/source-editor-image10.png)

新しいタスク コメントを追加するには、タスク キーワードを含むコメントを追加します。 次に例を示します。

```csharp
//TODO: Finish this for all properties.
```

Visual Studio for Mac では、これらのマーカーに注意を引くために、**タスク一覧**パッドでマーカーが強調表示されます。これは、 **[表示] > [パッド] > [タスク]** に移動することで表示できます。

![タスク一覧パッド](media/source-editor-image11.png)

## <a name="see-also"></a>参照

- [タスク一覧の使用 (Windows の Visual Studio)](/visualstudio/ide/using-the-task-list)