---
title: Windows フォームに基づくドメイン固有言語の作成
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c52b3bd352c2ecb2272ad8e229a0fe52a9ee5b41
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "88238362"
---
# <a name="create-a-windows-forms-based-domain-specific-language"></a>Windows フォームベースのドメイン固有言語を作成する

Windows フォームを使用すると、DSL 図を使用する代わりに、ドメイン固有言語 (DSL) モデルの状態を表示できます。 このトピックでは、Visual Studio の視覚化およびモデリング SDK を使用して Windows フォームを DSL にバインドする手順について説明します。

次の図は、Windows フォームの UI と、DSL インスタンスのモデルエクスプローラーを示しています。

![Visual Studio での DSL インスタンス](../modeling/media/dsl-wpf-2.png)

## <a name="create-a-windows-forms-dsl"></a>Windows フォーム DSL を作成する

**最小限の WinForm デザイナー** DSL テンプレートでは、独自の要件に合わせて変更できる最小限の dsl が作成されます。

1. **最小の WinForm デザイナー**テンプレートから DSL を作成します。

    このチュートリアルでは、次の名前を前提としています。

    - ソリューションと DSL の名前: `FarmApp`
    - 名前空間: `Company.FarmApp`

2. テンプレートに用意されている最初の例を試してみてください。

   1. すべてのテンプレートを変換します。

   2. サンプルをビルドして実行します (**Ctrl F5 キーを押し** + **F5**ます)。

   3. Visual Studio の実験用インスタンスで、 `Sample` デバッグプロジェクトでファイルを開きます。

        Windows フォームコントロールに表示されることに注意してください。

        また、モデルの要素がエクスプローラーに表示されていることも確認できます。

        フォームまたはエクスプローラーでいくつかの要素を追加し、他の表示に表示されていることを確認します。

   Visual Studio のメインインスタンスでは、DSL ソリューションに関する次の点に注意してください。

- `DslDefinition.dsl` には、図の要素が含まれていません。 これは、dsl の図を使用して DSL のインスタンスモデルを表示しないためです。 代わりに、Windows フォームをモデルにバインドすると、フォーム上の要素にモデルが表示されます。

- およびプロジェクトに加えて、 `Dsl` `DslPackage` ソリューションには、UI プロジェクトという名前の3番目のプロジェクトが含まれています。このプロジェクトには、 `UI.` **UI** Windows フォームコントロールの定義が含まれています。 `DslPackage` はに依存 `UI` し、 `UI` に依存し `Dsl` ます。

- プロジェクトには `DslPackage` 、 `UI\DocView.cs` プロジェクトで定義されている Windows フォームコントロールを表示するコードが含まれてい `UI` ます。

- このプロジェクトには、 `UI` DSL にバインドされたフォームコントロールの実際のサンプルが含まれています。 ただし、DSL 定義を変更した場合は機能しません。 プロジェクトには `UI` 次のものが含まれます。

  - という名前の Windows フォームクラス `ModelViewControl` 。

  - `DataBinding.cs`の追加の部分定義を含むという名前のファイル `ModelViewControl` 。 コンテンツを表示するには、 **ソリューションエクスプローラー**で、ファイルのショートカットメニューを開き、[ **コードの表示**] をクリックします。

### <a name="about-the-ui-project"></a>UI プロジェクトについて

Dsl 定義ファイルを更新して独自の DSL を定義する場合は、DSL を表示するようにプロジェクトのコントロールを更新する必要があり `UI` ます。 `Dsl`プロジェクトとは異なり `DslPackage` 、サンプル `UI` プロジェクトはから生成されません `DslDefinitionl.dsl` 。 必要に応じて、.tt ファイルを追加してコードを生成できます。ただし、このチュートリアルでは説明しません。

## <a name="update-the-dsl-definition"></a>DSL 定義を更新する

このチュートリアルでは、次の DSL 定義を使用します。

![DSL&#45;Wpf&#45;1](../modeling/media/dsl-wpf-1.png)

1. DSL デザイナーで DslDefinition. dsl を開きます。

2. **要素**の削除

3. **Examplemodel.store**ドメインクラスの名前をに変更 `Farm` します。

     `Size` **Int32**型で、Boolean 型の追加のドメインプロパティを指定し `IsOrganic` ます。 **Boolean**

    > [!NOTE]
    > ルートドメインクラスを削除してから新しいルートを作成する場合は、エディターのルートクラスのプロパティをリセットする必要があります。 **DSL エクスプローラー**で、[**エディター**] を選択します。 次に、[プロパティウィンドウで、[ **ルートクラス** ] をに設定し `Farm` ます。

4. **名前付きドメインクラス**ツールを使用して、次のドメインクラスを作成します。

    - `Field` -これにという名前の追加のドメインプロパティを指定 `Size` します。

    - `Animal` -プロパティウィンドウで、 **継承修飾子** を **Abstract**に設定します。

5. **ドメインクラス**ツールを使用して、次のクラスを作成します。

    - `Sheep`

    - `Goat`

6. **継承**ツールを使用して、を作成 `Goat` して `Sheep` から継承し `Animal` ます。

7. **埋め込みツールを**使用し `Field` て、との下に埋め込み `Animal` `Farm` ます。

8. 図を整理することもできます。 重複する要素の数を減らすには、リーフ要素のショートカットメニューの [ **サブツリーをここに移動** ] を使用します。

9. ソリューションエクスプローラーのツールバーにある**すべてのテンプレートを変換**します。

10. **Dsl**プロジェクトをビルドします。

    > [!NOTE]
    > この段階では、他のプロジェクトはエラーなしでビルドされません。 ただし、データソースウィザードでそのアセンブリを使用できるように、Dsl プロジェクトをビルドする必要があります。

## <a name="update-the-ui-project"></a>UI プロジェクトを更新する

DSL モデルに格納されている情報を表示する新しいユーザーコントロールを作成できるようになりました。 ユーザーコントロールをモデルに接続する最も簡単な方法は、データバインディングを使用することです。 **Modevdc bindingsource**という名前のデータバインディングアダプターの種類は、dsl を非 VMSDK インターフェイスに接続するように設計されています。

### <a name="define-your-dsl-model-as-a-data-source"></a>DSL モデルをデータソースとして定義する

1. [ **データ** ] メニューの [ **データソースの表示**] をクリックします。

     **[データ ソース]** ウィンドウが開きます。

     [ **新しいデータソースの追加**] を選択します。 **データソース構成ウィザード**が開きます。

2. [ **オブジェクト**]、[ **次へ**] の順に選択します。

     [ **Dsl**]、[ **FarmApp**] の順に展開し、モデルのルートクラスである [ **ファーム**] を選択します。 **[完了]** を選択します。

     ソリューションエクスプローラーでは、 **UI**プロジェクトに**Properties\DataSources\Farm.datasource**が含まれるようになりました。

     [データソース] ウィンドウに、モデルクラスのプロパティとリレーションシップが表示されます。

     ![DslWpf&#45;3](../modeling/media/dslwpf-3.png)

### <a name="connect-your-model-to-a-form"></a>モデルをフォームに接続する

1. **UI**プロジェクトで、既存の .cs ファイルをすべて削除します。

2. という名前の新しい **ユーザーコントロール** ファイルを `FarmControl` **UI** プロジェクトに追加します。

3. [ **データソース** ] ウィンドウの [ **ファーム**] のドロップダウンメニューで、[ **詳細**] を選択します。

    他のプロパティの既定の設定はそのままにします。

4. デザインビューで FarmControl.cs を開きます。

    [データソース] ウィンドウから FarmControl に **ファーム** をドラッグします。

    各プロパティに1つずつ、一連のコントロールが表示されます。 リレーションシップのプロパティでは、コントロールは生成されません。

5. **FarmBindingNavigator**を削除します。 これはデザイナーでも自動的に生成され `FarmControl` ますが、このアプリケーションには役立ちません。

6. ツールボックスを使用して、 **DataGridView**の2つのインスタンスを作成し、とという名前を指定し `AnimalGridView` `FieldGridView` ます。

   > [!NOTE]
   > 別の手順として、[データソース] ウィンドウからコントロールに [動物とフィールド] の項目をドラッグします。 この操作により、グリッドビューとデータソースの間にデータグリッドとバインドが自動的に作成されます。 ただし、このバインドは Dsl では正しく機能しません。 そのため、データグリッドとバインドを手動で作成することをお勧めします。

7. ツールボックスに **Modeの bindingsource** ツールが含まれていない場合は、ツールボックスを追加します。 [ **データ** ] タブのショートカットメニューで、[ **項目の選択**] を選択します。 [**ツールボックスアイテムの選択**] ダイアログで、[ **.NET Framework** ] タブの [ **modeて bindingsource** ] を選択します。

8. ツールボックスを使用して、 **modeの**2 つのインスタンスを作成し、とという名前を指定し `AnimalBinding` `FieldBinding` ます。

9. 各**Modeの** **DataSource**プロパティを**farmBindingSource**に設定します。

     **DataMember**プロパティを [**動物**または**フィールド**に設定します。

10. の **DataSource** プロパティをに `AnimalGridView` 、のをに設定し `AnimalBinding`  `FieldGridView` `FieldBinding` ます。

11. ファームコントロールのレイアウトを好みに合わせて調整します。

    **Modeare bindingsource**は、dsl に固有のいくつかの機能を実行するアダプターです。

- VMSDK ストアトランザクションで更新をラップします。

   たとえば、ユーザーがデータビューグリッドから行を削除すると、通常のバインドではトランザクションの例外が発生します。

- これにより、ユーザーが行を選択したときに、データグリッド行ではなく、対応するモデル要素のプロパティがプロパティウィンドウ表示されるようになります。

  ![DslWpf4 ](../modeling/media/dslwpf4.png) データソースとビュー間のリンクのスキーマ。

### <a name="complete-the-bindings-to-the-dsl"></a>DSL へのバインドを完了します。

1. **UI**プロジェクトの別のコードファイルに次のコードを追加します。

    ```csharp
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace Company.FarmApp
    {
      partial class FarmControl
      {
        public IContainer Components { get { return components; } }

        /// <summary>Binds the WinForms data source to the DSL model.
        /// </summary>
        /// <param name="nodelRoot">The root element of the model.</param>
        public void DataBind(ModelElement modelRoot)
        {
          WinFormsDataBindingHelper.PreInitializeDataSources(this);
          this.farmBindingSource.DataSource = modelRoot;
          WinFormsDataBindingHelper.InitializeDataSources(this);
        }
      }
    }
    ```

2. **Dslpackage**プロジェクトで、次の変数定義を更新して、 **Dslpackage\ docview.tt**を編集します。

    ```csharp
    string viewControlTypeName = "FarmControl";
    ```

## <a name="test-the-dsl"></a>DSL をテストする

DSL ソリューションを構築して実行できるようになりました。ただし、後でさらに改良を加えることもできます。

1. ソリューションをビルドして実行します。

2. Visual Studio の実験用インスタンスで、 **サンプル** ファイルを開きます。

3. **FarmApp エクスプローラー**で、**ファーム**のルートノードのショートカットメニューを開き、[**新しい Goat の追加**] を選択します。

     `Goat1` [ **動物** ] ビューに表示されます。

    > [!WARNING]
    > [**動物**] ノードではなく、[**ファーム**] ノードのショートカットメニューを使用する必要があります。

4. **ファーム**のルートノードを選択し、そのプロパティを表示します。

     フォームビューで、ファームの **名前** または **サイズ** を変更します。

     フォームの各フィールドから移動すると、プロパティウィンドウの対応するプロパティが変更されます。

## <a name="enhance-the-dsl"></a>DSL を強化する

### <a name="make-the-properties-update-immediately"></a>プロパティを直ちに更新する

1. FarmControl.cs のデザインビューで、名前、サイズ、IsOrganic などの単純なフィールドを選択します。

2. [プロパティウィンドウで、[ **連結** ] を展開して [ **(詳細)**] を開きます。

     [ **書式設定と詳細バインド** ] ダイアログボックスの [ **データソース更新モード**] で、[ **OnPropertyChanged**] を選択します。

3. ソリューションをビルドして実行します。

     フィールドの内容を変更すると、ファームモデルの対応するプロパティがすぐに変更されることを確認します。

### <a name="provide-add-buttons"></a>[追加] ボタンを指定する

1. FarmControl.cs のデザインビューで、ツールボックスを使用してフォーム上にボタンを作成します。

    たとえば、ボタンの名前とテキストを編集 `New Sheep` します。

2. (たとえば、ダブルクリックして) ボタンの背後にあるコードを開きます。

    次のように編集します。

   ```csharp
   private void NewSheepButton_Click(object sender, EventArgs e)
   {
     using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
     {
       elementOperations.MergeElementGroup(farm,
         new ElementGroup(new Sheep(farm.Partition)));
       t.Commit();
     }
   }

   // The following code is shared with other add buttons:
   private ElementOperations operationsCache = null;
   private ElementOperations elementOperations
   {
     get
     {
       if (operationsCache == null)
       {
         operationsCache = new ElementOperations(farm.Store, farm.Partition);
       }
       return operationsCache;
     }
   }
   private Farm farm
   {
     get { return this.farmBindingSource.DataSource as Farm; }
   }
   ```

    また、次のディレクティブも挿入する必要があります。

   ```csharp

   using Microsoft.VisualStudio.Modeling;
   ```

3. Goats と Fields に似たボタンを追加します。

4. ソリューションをビルドして実行します。

5. [新規作成] ボタンによって項目が追加されていることを確認します。 FarmApp Explorer と適切なデータグリッドビューの両方に新しい項目が表示されます。

    データグリッドビューで要素の名前を編集できるようになります。 そこから削除することもできます。

   ![DSL&#45;Wpf&#45;2](../modeling/media/dsl-wpf-2.png)

### <a name="about-the-code-to-add-an-element"></a>要素を追加するコードについて

新しい要素のボタンについては、次の代替コードが少し単純になります。

```csharp
private void NewSheepButton_Click(object sender, EventArgs e)
{
  using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
  {
    farm.Animals.Add(new Sheep(farm.Partition)); ;
    t.Commit();
  }
}
```

ただし、このコードでは、新しい項目の既定の名前は設定されません。 DSL の **要素マージディレクティブ** で定義したカスタマイズされたマージは実行されません。定義されている可能性があるカスタムマージコードは実行されません。

したがって、を使用して新しい要素を作成することをお勧め <xref:Microsoft.VisualStudio.Modeling.ElementOperations> します。 詳細については、「 [要素の作成および移動をカスタマイズ](../modeling/customizing-element-creation-and-movement.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [ドメイン固有言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)
- [ドメイン固有言語をカスタマイズするコードを記述する](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)
