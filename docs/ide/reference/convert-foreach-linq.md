---
title: foreach ループを LINQ に変換する
descritpion: Convert any foreach loop that uses an IEnumerable to a LINQ query or a LINQ call form (also known as a LINQ method).
ms.date: 07/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 390e66fa01d49f217140c3c030bcc54fd349e402
ms.sourcegitcommit: 8b1314ceab58e0d562cdbb1367fa738fdca7bf1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2020
ms.locfileid: "86285395"
---
# <a name="convert-a-foreach-loop-to-linq"></a>foreach ループを LINQ に変換する

このリファクタリングは以下に適用されます。

- C#

**概要:** IEnumerables を使用する *foreach* ループを LINQ クエリまたは LINQ 呼び出し形式 (別名 LINQ メソッド) に簡単に変換できます。

**条件:** IEnumerable を使用する foreach ループがあり、そのループで LINQ クエリとして読み取る。

**理由:** foreach ループよりも LINQ 構文を使用したい。 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq) により、クエリは C# での高度な言語構成要素になります。 LINQ では、ファイルのコードの量が減り、コードが読みやすくなります。また、さまざまなデータ ソースで同様のクエリ式パターンを指定できます。

> [!NOTE]
> 一般的に、LINQ 構文は foreach ループに比べて効率的ではありません。 LINQ を使用してコードの読みやすさを改善するときは、発生する可能性があるパフォーマンスのトレードオフを認識しておくことをお勧めします。

## <a name="convert-a-foreach-loop-to-linq-refactoring"></a>foreach ループを LINQ リファクタリングに変換する

1. `foreach` キーワードにカーソルを置きます。

    ![IEnumerable サンプルを使用する foreach](media/convert-foreach-to-LINQ.png)

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   ![LINQ に変換メニューのサンプル](media/convert-foreach-to-LINQ-codefix.png)

3. **[Convert to LINQ]\(LINQ に変換\)** または **[Convert to LINQ (call form)]\(LINQ に変換 (呼び出し形式)\)** を選択する

   ![LINQ クエリの結果のサンプル](media/convert-foreach-to-LINQ-result.png)

   ![LINQ 呼び出し形式の結果のサンプル](media/convert-foreach-to-LINQ-callform-result.png)

### <a name="sample-code"></a>サンプル コード

```csharp
using System.Collections.Generic;

public class Class1
{
    public void MyMethod()
    {
        var greetings = new List<string>()
            { "hi", "yo", "hello", "howdy" };

        IEnumerable<string> enumerable()
        {
            foreach (var greet in greetings)
            {
                if (greet.Length < 3)
                {
                    yield return greet;
                }
            }

            yield break;
        }
    }
}
```

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [[変更のプレビュー] ウィンドウ](../../ide/preview-changes.md)
- [.NET 開発者向けのヒント](../csharp-developer-productivity.md)
