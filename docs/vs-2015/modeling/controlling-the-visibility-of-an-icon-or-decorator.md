---
title: アイコンまたはデコレータの可視性の制御 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 2697fd5d-b936-4b6b-b87b-be64825dc7a4
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 49cecff999e0155209ba58c20c0d623b15d63698
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667830"
---
# <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>アイコンまたはデコレーターの可視性の制御
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*デコレータ*は、ドメイン固有言語 (DSL) の図形に表示されるアイコンまたはテキストの行です。 モデルのプロパティの状態に応じて、デコレータを表示したり、非表示にしたりすることができます。 たとえば、人物を表す図形では、ユーザーの性別、子の数などに応じて異なるアイコンが表示される場合があります。

## <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>アイコンまたはデコレータの可視性の制御
 次の手順では、ドメインクラスへの図形とそのマッピングが既に定義されていることを前提としています。 詳細については、「 [ドメイン固有言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。

#### <a name="to-control-the-visibility-of-an-icon-or-text-decorator"></a>アイコンまたはテキストデコレータの表示を制御するには

1. DSL 定義図で、表示するアイコンまたはテキストデコレーターを図形クラスに追加します。

   1. Shape クラスを右クリックし、[ **追加**] をポイントして、必要なデコレータの種類をクリックします。

   2. デコレータの **Position** プロパティを設定します。 複数のデコレータが同じ位置を持つことができます。 たとえば、男性と女性のアイコンを同じ位置に共有することができます。

   3. アイコンデコレータの **既定のアイコン** プロパティを設定します。

2. 図の要素マップを選択します。これは、DSL 定義図の図形クラスとドメインクラスの間の灰色の線です。

3. DSL の詳細ウィンドウの [ **デコレータマップ** ] タブで、デコレータを選択します。 たとえば、MaleDecorator のようになります。

4. [ **表示フィルター** ] ボックスをオンにします。

5. 可視性を制御する必要があるドメインプロパティがイミディエイトドメインクラスにある場合は、[ **Path To Filter] プロパティを** 空白のままにします。

    それ以外の場合は、ドロップダウンメニューをクリックし、プロパティが配置されているリレーションシップまたはクラスに移動します。

   - エラーレポートが表示されないようにするには、ナビゲーションツールで "*" とマークされているリレーションシップを移動しないでください。

6. **フィルタープロパティ**をドメインプロパティに設定します。 たとえば、性別です。

7. [ **可視性エントリ** ] の一覧で、デコレータが表示されるこのドメインプロパティの値を追加します。 たとえば、「男性」とします。

8. 各アイコンに対して手順を繰り返します。

9. **すべてのテンプレートを変換**し、ビルドして実行し、テスト図を開きます。

10. 制御プロパティの値を変更すると、デコレーターが表示され、非表示になります。

    多くの場合、単純な値のセットよりも複雑な数式によって、表示を制御する必要があります。 たとえば、特定の種類のリンクの数に応じてアイコンを使用する場合や、数値が特定の範囲内にあるかどうかに依存させる場合などです。 その場合は、次の手順を使用します。

#### <a name="to-control-the-visibility-of-a-decorator-based-on-a-formula"></a>数式に基づいてデコレータの表示を制御するには

1. ドメインクラスに計算されたドメインプロパティを追加します。 [ **プロパティ** ] ウィンドウで、次の値を設定します。

     **Isbrowsable 可能 =** `False`**-これにより、ユーザーのプロパティが非表示**になります。    

     **Kind =** `Calculated`**-これは、値を計算するコードを提供することを意味します**。    

     **DecoratorControl**などの**名前**

     **各種** = `Boolean`

     詳細については、「 [計算済みおよびカスタムストレージのプロパティ](../modeling/calculated-and-custom-storage-properties.md)」を参照してください。

2. 新しいプロパティがデコレータの可視性を制御するようにします。

    1. [ダイアグラム要素マップ] を選択します。これは、ドメインクラスから図形までの灰色の線です。 DSL の **詳細** ウィンドウで、[ **ある decoratormap** ] タブを開きます。

    2. [ **表示フィルター** ] ボックスをオンにします。

    3. [ **フィルター] プロパティ**で、コントロールプロパティ **DecoratorControl**を選択します。

    4. [ **可視性エントリ**] に「」と入力 `True` します。

3. ソリューションエクスプローラーツールバーの [ **すべてのテンプレートの変換** ] をクリックします。

4. [**ビルド**] メニューの [**ソリューションのビルド**] をクリックします。

5. 表示されたエラーレポートをダブルクリックします。 "*クラス* には GetDecoratorControlValue の定義が含まれていません"。

     [テキストエディター] が表示され、[] が表示されます。 強調表示されたエラーは、メソッドの追加を要求するコメントです。

6. 名前空間、クラス、およびメソッドが見つからないことに注意してください。  たとえば、FamilyTree GetDecoratorControlValue () のようになります。

7. 別のコードファイルで、不足しているメソッドを含む部分クラス定義を記述します。 次に例を示します。

    ```
    namespace Company.FamilyTree
    { partial class Person
      { bool GetDecoratorControlValue()
        {
          return this.Children.Count > 0;
    } } }
    ```

     プログラムコードを使用したモデルのカスタマイズの詳細については、「 [プログラムコードでのモデルのナビゲーションと更新](../modeling/navigating-and-updating-a-model-in-program-code.md)」を参照してください。

8. ソリューションをリビルドして実行します。

## <a name="see-also"></a>参照
 [図形とコネクタの定義](../modeling/defining-shapes-and-connectors.md)[図の背景画像の設定](../modeling/setting-a-background-image-on-a-diagram.md)[プログラムコードでのモデルの移動および更新コードの](../modeling/navigating-and-updating-a-model-in-program-code.md)[記述ドメイン固有言語のカスタマイズ](../modeling/writing-code-to-customise-a-domain-specific-language.md)
