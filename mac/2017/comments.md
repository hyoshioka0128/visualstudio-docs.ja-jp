---
title: コメント アウト コード
description: この記事では、Visual Studio for Mac のソース エディターでのコメントの使用について説明します
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: 0FE5E929-1846-4F48-B5E3-70990FAF9504
ms.topic: how-to
ms.openlocfilehash: 44eee75b4803b4317bb7d3cd02cb19b55f41a067
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2020
ms.locfileid: "85949988"
---
# <a name="comments"></a>コメント

コードをデバッグしたり、コードで実験したりするとき、一時的に、あるいは長期間、コードのブロックにコメントを付けると便利です。

コード ブロック全体にコメントを付けるには:

* コードを選択し、コンテキスト メニューから **[行コメントの切り替え]** を選択します。

OR

* 選択したコードで `cmd + /` キー バインドを使用します。

いずれの方法も、コード セクションにコメントを付けるか、コメントを解除するために利用できます。 C# ファイルの場合、行コメントのレベルを追加できます。レベルを追加すると、実際のコメントを維持しながら、コード領域にコメントを付けたり、コメントを解除したりできます。

![複数レベルのコメント](media/source-editor-image8.png)

コメントは、将来、コードを利用するかもしれない開発者のためにコードを記録しておく意味でも役立ちます。 以上の作業は通常、複数行コメントという形態で行われます。これは各言語で次のように追加されます。

**C#**

```csharp
/*
 This is a multi-line
 comment in C#
*/
```

**F#**

```fsharp
(*
 This is a multi-line
  comment in F#
*)
```

## <a name="see-also"></a>関連項目

- [コメント アウト コード (Windows の Visual Studio)](/visualstudio/ide/quickstart-editor#comment-out-code)