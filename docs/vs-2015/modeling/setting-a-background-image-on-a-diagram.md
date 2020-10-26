---
title: 図の背景画像の設定 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: e334a24c-8521-4072-b50f-e59158dde145
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2b7d206852101a1d99a08eac710d88e93afe4a04
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671206"
---
# <a name="setting-a-background-image-on-a-diagram"></a>ダイアグラムへの背景イメージの設定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Visualization and Modeling SDK では、カスタム コードを使用して生成されるデザイナーの背景イメージを設定できます。

## <a name="setting-the-background-image"></a>背景画像を設定する

#### <a name="to-set-a-background-image-for-a-generated-designer"></a>生成されるデザイナーの背景イメージを設定するには

1. 図の背景として使用するイメージ ファイルを、現在のプロジェクトの Dsl\Resources ディレクトリにコピーします。

2. **ソリューションエクスプローラー**で、[Dsl\ Resources] フォルダーを右クリックし、[**追加**] をポイントして、[**既存の項目**] をクリックします。

3. [ **既存項目の追加** ] ダイアログボックスで、dsl¥ Resources フォルダーを参照します。

4. [ **ファイルの種類** ] ボックスの一覧の [ **イメージファイル**] をクリックします。

5. ディレクトリにコピーしたイメージファイルをクリックし、[ **追加**] をクリックします。

6. [Dsl] を右クリックし、[ **プロパティ** ] をクリックして dsl プロジェクトのプロパティを開きます。

7. [ **リソース** ] タブで、[ **このプロジェクトには既定のリソースファイルが含まれていません] をクリックします。ここをクリックして作成します。**

8. **ソリューションエクスプローラー**から [リソース] ウィンドウに画像をドラッグして、リソースファイルにイメージファイルを追加します。

9. ［ファイル］ メニューを開き、プロジェクトのプロパティを保存するオプションをクリックします。

10. ファイル Dsl\Properties\Resources.resx が存在しており、その下に Resources.Designer.cs ファイルがあることを確認します。

11. Resources.Designer.cs がない場合は、 **ソリューションエクスプローラー**でファイルリソース .resx をクリックします。

12. **[プロパティ]** ウィンドウで、 `Custom Tool` プロパティを `ResXFileCodeGenerator`に設定します。

13. **ソリューションエクスプローラー**で、Dsl プロジェクトを右クリックし、[**追加**] をポイントして、[**新しいフォルダー**] をクリックします。

14. フォルダーに「 **Custom**」という名前を指定します。

15. カスタムフォルダーを右クリックして [ **追加**] をポイントし、[ **新しい項目**] をクリックします。

16. [ **新しい項目の追加** ] ダイアログボックスの [ **テンプレート** ] ボックスの一覧で、[ **コードファイル**] をクリックします。

17. [ **名前** ] ボックスに「 `BackgroundImage.cs` 」と入力し、[ **追加**] をクリックします。

18. 次のコードを BackgroundImage.cs ファイルにコピーし、名前空間、図クラス名、およびイメージ ファイル リソース名を調整します。

     "MyDiagramClass" を、Dsl\GeneratedCode\Diagrams.cs で定義されている図の部分クラスの名前に置き換えます。 Dsl\GeneratedCode\Diagrams.cs ファイルから正しい名前空間を取得することもできます。

    ```
    using System;
    using Microsoft.VisualStudio.Modeling.Diagrams;

    // Fix the namespace:
    namespace Fabrikam.MyLanguage
    {
      // Fix the Diagram Class name - get it from GeneratedCode\Diagram.cs

      public partial class Language29Diagram
      {
        protected override void InitializeInstanceResources()
        {
          // Fix the Resources namespace and the Image resource name:
          ImageField backgroundField = new ImageField("background",
              Fabrikam.MyLanguage.Properties.Resources.MyPicture);

          backgroundField.DefaultFocusable = false;
          backgroundField.DefaultSelectable = false;
          backgroundField.DefaultVisibility = true;
          backgroundField.DefaultUnscaled = false;

          shapeFields.Add(backgroundField);

          backgroundField.AnchoringBehavior
            .SetTopAnchor(AnchoringBehavior.Edge.Top, 0.01);
          backgroundField.AnchoringBehavior
            .SetLeftAnchor(AnchoringBehavior.Edge.Left, 0.01);
          backgroundField.AnchoringBehavior
            .SetRightAnchor(AnchoringBehavior.Edge.Right, 0.01);
          backgroundField.AnchoringBehavior
            .SetBottomAnchor(AnchoringBehavior.Edge.Bottom, 0.01);

          base.InitializeInstanceResources();
        }
      }
    }
    ```

     プログラムコードを使用したモデルのカスタマイズの詳細については、「 [プログラムコードでのモデルのナビゲーションと更新](../modeling/navigating-and-updating-a-model-in-program-code.md)」を参照してください。

## <a name="see-also"></a>参照
 [図形とコネクタの定義](../modeling/defining-shapes-and-connectors.md)[テキストとイメージのフィールドのカスタマイズ](../modeling/customizing-text-and-image-fields.md)[プログラムコードでのモデルの移動と更新コードの](../modeling/navigating-and-updating-a-model-in-program-code.md)[記述ドメイン固有言語の](../modeling/writing-code-to-customise-a-domain-specific-language.md)カスタマイズ
