---
title: C# の Equals および GetHashCode メソッドのオーバーライドを生成する
description: '[クイックアクションとリファクタリング] メニューを使用して、Equals メソッドと GetHashCode メソッドを生成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/08/2021
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 597d17b69aa3f0feca520e6100439d934e5d9211
ms.sourcegitcommit: f9ed9c4c6c166ef9826feb21dcb9c4d47ed14e1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2021
ms.locfileid: "102607357"
---
# <a name="generate-equals-and-gethashcode-method-overrides-in-visual-studio"></a>Visual Studio で Equals および GetHashCode メソッドのオーバーライドを生成する

このコード生成は以下に適用されます。

- C#

**概要:****Equals** メソッドと **GetHashCode** メソッドを生成します。

**タイミング:** これらのオーバーライドは、メモリ内のオブジェクトの場所ではなく、1 つ以上のフィールドによって比較される型がある場合に生成されます。

**理由:**

- 値の型を実装する場合、**Equals** メソッドのオーバーライドを検討してください。 オーバーライドにした場合、ValueType では、Equals メソッドの既定の実装に比べ、パフォーマンスが上がります。

- 参照型を実装する場合、**Equals** メソッドのオーバーライドは、型がポイント、文字列、BigNumber などの基本データ型に似ている場合に検討してください。

- ハッシュ テーブルで型を正しく機能させるには、**GetHashCode** メソッドをオーバーライドします。 詳細については[等値演算子](/dotnet/standard/design-guidelines/equality-operators)のガイドラインをご覧ください。

## <a name="how-to"></a>操作方法

1. 型宣言の行のどこかにカーソルを置きます。

    ```csharp
    public class ImaginaryNumber
    {
        public double RealNumber { get; set; }
        public double ImaginaryUnit { get; set; }
    }
    ```

   コードは次のスクリーンショットのようになります。

   ![コードのスクリーンショット。強調表示されているコードに、生成されたメソッドが適用されます](media/overrides-highlight-cs.png)

   > [!TIP]
   > 型名をダブルクリックして選択しないでください。ダブルクリックすると、メニュー オプションが利用できなくなります。 行のどこかにカーソルを置くだけです。

1. 次に、次の操作のいずれかを選択します。

   - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   - 右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。

   - テキスト カーソルが既にクラスの空の行にある場合は、左余白に表示されている ![Visual Studio のスクリーンショット。ねじ回しのアイコンはクイック アクションを示します](../media/screwdriver-icon.png) アイコンをクリックします。

1. ドロップダウン メニューで **[Equals(object) を生成する]** または **[Equals および GetHashCode を生成する]** を選択します。

   ![[オーバーライドを生成する] ドロップダウン メニューのスクリーンショット](media/overrides-preview-cs.png)

1. **[メンバーの選択]** ダイアログ ボックスで、メソッドを生成するメンバーを選択します。

    ![[オーバーライドを生成する] ダイアログ](media/overrides-dialog-cs.png)

    > [!TIP]
    > ダイアログの下部の近くにあるチェックボックスを使って、このダイアログから演算子を生成することもできます。

   `Equals` メソッドと `GetHashCode` メソッドは、次のコードに示されているように、既定の実装で生成されます。

    ```csharp
   public class ImaginaryNumber : IEquatable<ImaginaryNumber>
    {
        public double RealNumber { get; set; }
        public double ImaginaryUnit { get; set; }

        public override bool Equals(object obj)
        {
            return Equals(obj as ImaginaryNumber);
        }

        public bool Equals(ImaginaryNumber other)
        {
            return other != null &&
                   RealNumber == other.RealNumber &&
                   ImaginaryUnit == other.ImaginaryUnit;
        }

        public override int GetHashCode()
        {
            return HashCode.Combine(RealNumber, ImaginaryUnit);
        }
    }
    ```

   コードは次のスクリーンショットのようになります。

   ![生成されたメソッドの結果のスクリーンショット](media/overrides-result-cs.png)

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
