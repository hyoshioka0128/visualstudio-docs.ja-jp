---
title: ドメイン固有言語における検証
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, constraints
- Domain-Specific Language, validation
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7a37dbb4d9754641b4bcca826ff0ec77c7298d9b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75594007"
---
# <a name="validation-in-a-domain-specific-language"></a>ドメイン固有言語における検証
ドメイン固有言語 (DSL) の作成者は、検証制約を定義して、ユーザーが作成したモデルが意味を持つことを確認できます。 たとえば、DSL でユーザーが人々とその先祖の家系図を描くことができる場合、子の誕生日が親の誕生日よりも後であることを確認する制約を作成できます。

 検証制約は、モデルが保存されているとき、開いたとき、ユーザーが明示的に [ **検証** ] メニューコマンドを実行したときに実行できます。 検証をプログラム制御の下で実行することもできます。 たとえば、プロパティ値またはリレーションシップの変更に応じて検証を実行できます。

 テキストテンプレートや、ユーザーのモデルを処理するその他のツールを作成する場合は、検証が特に重要になります。 検証により、そうしたツールが仮定する事前条件をモデルが満たすことが保証されます。

> [!WARNING]
> 検証制約は、拡張機能メニュー コマンドおよびジェスチャ ハンドラーとともに、DSL の別個の拡張機能内で定義することもできます。 ユーザーは DSL に加えて、こうした拡張機能を選択的にインストールできます。 詳細については、「 [MEF を使用した DSL の拡張](../modeling/extend-your-dsl-by-using-mef.md)」を参照してください。

## <a name="running-validation"></a>検証の実行
 ユーザーがモデル、つまりドメイン固有言語のインスタンスを編集しているとき、次の操作により検証を実行できます。

- ダイアグラムを右クリックし、[ **すべて検証**] を選択します。

- DSL のエクスプローラーで最上位のノードを右クリックし、[**すべて検証**] を選択します。

- モデルを保存します。

- モデルを開きます。

- さらに、たとえばメニュー コマンドの一部として、または変更に応じて検証を実行するプログラム コードを作成できます。

  検証エラーは、[ **エラー一覧** ] ウィンドウに表示されます。 ユーザーはエラー メッセージをダブルクリックして、エラーの原因であるモデル要素を選択できます。

## <a name="defining-validation-constraints"></a>検証制約の定義
 DSL のドメイン クラスまたはリレーションシップに検証メソッドを追加することにより、検証制約を定義します。 ユーザーまたはプログラム制御のいずれかにより検証が実行されると、検証メソッドの一部または全部が実行されます。 各メソッドはそのクラスの各インスタンスに適用され、各クラスにはいくつかの検証メソッドを含めることができます。

 各検証メソッドは発見したすべてのエラーを報告します。

> [!NOTE]
> 検証メソッドはエラーを報告しますが、モデルを変更しません。 特定の変更を調整または防止する場合は、「 [検証の代替手段](#alternatives)」を参照してください。

#### <a name="to-define-a-validation-constraint"></a>検証制約を定義するには

1. [ **Editor\ 検証** ] ノードで検証を有効にします。

   1. [ **Ds**] を開きます。

   2. DSL エクスプローラーで、[ **エディター** ] ノードを展開し、[ **検証**] を選択します。

   3. プロパティウィンドウで、[ **使用**  ] プロパティをに設定し `true` ます。 これらのプロパティをすべて設定すると利便性が最高になります。

   4. **ソリューションエクスプローラー**ツールバーの [**すべてのテンプレートの変換**] をクリックします。

2. 1 つ以上のドメイン クラスまたはドメイン リレーションシップに対して部分クラス定義を作成します。 これらの定義は、 **Dsl** プロジェクトの新しいコードファイルに記述します。

3. 各クラスのプレフィックスとして次の属性を使用します。

   ```csharp
   [ValidationState(ValidationState.Enabled)]
   ```

   - 既定では、この属性により、派生したクラスの検証も有効になります。 特定の派生クラスについて検証を無効にする場合は、`ValidationState.Disabled` を使用できます。

4. 検証メソッドをクラスに追加します。 各検証メソッドには任意の名前を付けられますが、型 <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationContext> のパラメーターは 1 つです。

    プレフィックスとして 1 つ以上の `ValidationMethod` 属性を使用する必要があります。

   ```csharp
   [ValidationMethod (ValidationCategories.Open | ValidationCategories.Save | ValidationCategories.Menu ) ]
   ```

    ValidationCategories はメソッドが実行されるタイミングを指定します。

   次に例を示します。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;

// Allow validation methods in this class:
[ValidationState(ValidationState.Enabled)]
// In this DSL, ParentsHaveChildren is a domain relationship
// from Person to Person:
public partial class ParentsHaveChildren
{
  // Identify the method as a validation method:
  [ValidationMethod
  ( // Specify which events cause the method to be invoked:
    ValidationCategories.Open // On file load.
  | ValidationCategories.Save // On save to file.
  | ValidationCategories.Menu // On user menu command.
  )]
  // This method is applied to each instance of the
  // type (and its subtypes) in a model:
  private void ValidateParentBirth(ValidationContext context)
  {
    // In this DSL, the role names of this relationship
    // are "Child" and "Parent":
     if (this.Child.BirthYear < this.Parent.BirthYear
        // Allow user to leave the year unset:
        && this.Child.BirthYear != 0)
      {
        context.LogError(
             // Description:
                       "Child must be born after Parent",
             // Unique code for this error:
                       "FAB001ParentBirthError",
              // Objects to select when user double-clicks error:
                       this.Child,
                       this.Parent);
    }
  }
```

 このコードについては次の点に注意してください。

- 検証メソッドをドメイン クラスまたはドメイン リレーションシップに追加できます。 これらの型のコードは、 **Code\Domain に生成 \* さ**れます。

- 各検証メソッドはそのクラスおよびサブクラスのすべてのインスタンスに適用されます。 ドメイン リレーションシップの場合、各インスタンスは 2 つのモデル要素間のリンクです。

- 検証メソッドは指定された順序で適用されず、各メソッドは予測可能な順序でそのクラスのインスタンスに適用されません。

- 通常、検証メソッドでストア コンテンツを更新するのは、一貫性のない結果を生じる可能性があるため、不適切な処理です。 代わりに、`context.LogError`、`LogWarning`、または `LogInfo` を呼び出すことにより、メソッドはすべてのエラーを報告する必要があります。

- LogError 呼び出しでは、ユーザーがエラー メッセージをダブルクリックしたときに選択される、モデル要素またはリレーションシップ リンクの一覧を指定できます。

- プログラムコードでモデルを読み取る方法の詳細については、「 [プログラムコードでのモデルのナビゲーションと更新](../modeling/navigating-and-updating-a-model-in-program-code.md)」を参照してください。

  例は次のドメイン モデルに適用されます。 ParentsHaveChildren リレーションシップは Child および Parent という名前のロールを含みます。

  ![DSL 定義図 &#45; ファミリツリーモデル](../modeling/media/familyt_person.png)

## <a name="validation-categories"></a>検証カテゴリ
 <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute> 属性で、検証メソッドをいつ実行するかを指定します。

|カテゴリ|実行|
|-|-|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|ユーザーが検証メニュー コマンドを呼び出すとき。|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|モデル ファイルが開くとき。|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|ファイルが保存されるとき。 検証エラーがある場合、ユーザーは保存操作を取り消すことができます。|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|ファイルが保存されるとき。 このカテゴリでメソッドからのエラーがある場合、ユーザーはファイルを再度開くことができない可能性があることを警告されます。<br /><br /> このカテゴリは、読み込みエラーを引き起こす可能性がある、複製された名前または ID、またはその他の条件をテストする検証メソッドに使用します。|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|ValidateCustom メソッドが呼び出されるとき。 このカテゴリの検証はプログラム コードからのみ呼び出すことができます。<br /><br /> 詳細については、「 [カスタム検証カテゴリ](#custom)」を参照してください。|

## <a name="where-to-place-validation-methods"></a>検証メソッドを配置する場所
 多くの場合、異なる型に 1 つの検証メソッドを配置することで、同じ効果を得ることができます。 たとえば、次のように、ParentsHaveChildren リレーションシップの代わりに Person クラスにメソッドを追加し、リンクを通して反復することができます。

```
[ValidationState(ValidationState.Enabled)]
public partial class Person
{[ValidationMethod
 ( ValidationCategories.Open
 | ValidationCategories.Save
 | ValidationCategories.Menu
 )
]
  private void ValidateParentBirth(ValidationContext context)
  {
    // Iterate through ParentHasChildren links:
    foreach (Person parent in this.Parents)
    {
        if (this.BirthYear <= parent.BirthYear)
        { ...
```

 **検証制約の集約。** 予測可能な順序で検証を適用するには、モデルのルート要素など、オーナー クラスで単一の検証メソッドを定義します。 この手法により、複数のエラー報告を単一のメッセージに集約することもできます。

 欠点は組み合わされたメソッドが管理しにくいことと、すべての制約が同じ `ValidationCategories` を含む必要があることです。 したがって、可能であれば、各制約を別々のメソッドに維持することをお勧めします。

 **コンテキスト キャッシュ内の値の受け渡し。** コンテキスト パラメーターは任意の値を配置可能なディクショナリを持っています。 このディクショナリは検証が実行中保持されます。 たとえば、特定の検証メソッドはコンテキスト内でエラー カウントを維持し、繰り返しのメッセージでエラー ウィンドウがあふれることを防ぐために使用できます。 次に例を示します。

```csharp
List<ParentsHaveChildren> erroneousLinks;
if (!context.TryGetCacheValue("erroneousLinks", out erroneousLinks))
erroneousLinks = new List<ParentsHaveChildren>();
erroneousLinks.Add(this);
context.SetCacheValue("erroneousLinks", erroneousLinks);
if (erroneousLinks.Count < 5) { context.LogError( ... ); }
```

## <a name="validation-of-multiplicities"></a>多重度の検証
 最小多重度をチェックするための検証メソッドは DSL 用に自動生成されます。 このコードは、 **生成された Code\MultiplicityValidation.cs**に書き込まれます。 これらのメソッドは、DSL エクスプローラーの [ **Editor\ 検証** ] ノードで検証を有効にしたときに有効になります。

 ドメイン リレーションシップのロールの多重度を 1..* または 1..1 に設定し、ユーザーがこのリレーションシップのリンクを作成しない場合、検証エラー メッセージが表示されます。

 たとえば、DSL にクラス Person と町村があり、リレーションシップが PersonLivesInTown で** \\ **あるとします。* 町の役割では、町を持たない人物ごとにエラーメッセージが表示されます。

## <a name="running-validation-from-program-code"></a>プログラム コードからの検証の実行
 ValidationController をアクセスまたは作成することにより検証を実行できます。 エラーウィンドウでユーザーにエラーを表示する場合は、ダイアグラムの DocData にアタッチされている ValidationController を使用します。 たとえば、メニュー コマンドを作成する場合、コマンド セット クラスで `CurrentDocData.ValidationController` を使用できます。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;
using Microsoft.VisualStudio.Modeling.Shell;
...
partial class MyLanguageCommandSet
{
  private void OnMenuMyContextMenuCommand(object sender, EventArgs e)
  {
   ValidationController controller = this.CurrentDocData.ValidationController;
...
```

 詳細については、「 [方法: ショートカットメニューにコマンドを追加](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)する」を参照してください。

 別個の検証コントローラーを作成して、独自にエラーを管理することもできます。 次に例を示します。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;
using Microsoft.VisualStudio.Modeling.Shell;
...
Store store = ...;
VsValidationController validator = new VsValidationController(s);
// Validate all elements in the Store:
if (!validator.Validate(store, ValidationCategories.Save))
{
  // Deal with errors:
  foreach (ValidationMessage message in validator.ValidationMessages) { ... }
}
```

## <a name="running-validation-when-a-change-occurs"></a>変更発生時の検証実行
 モデルが無効になった直後にユーザーへの警告を表示する場合、検証を実行するストア イベントを定義できます。 ストアイベントの詳細については、「 [イベントハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

 検証コードに加えて、次の例のようなコンテンツを含むカスタムコードファイルを **Dslpackage** プロジェクトに追加します。 このコードはドキュメントにアタッチされる `ValidationController` を使用します。 このコントローラーでは、Visual Studio の [エラー一覧] に検証エラーが表示されます。

```csharp
using System;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;
namespace Company.FamilyTree
{
  partial class FamilyTreeDocData // Change name to your DocData.
  {
    // Register the store event handler:
    protected override void OnDocumentLoaded()
    {
      base.OnDocumentLoaded();
      DomainClassInfo observedLinkInfo = this.Store.DomainDataDirectory
         .FindDomainClass(typeof(ParentsHaveChildren));
      DomainClassInfo observedClassInfo = this.Store.DomainDataDirectory
         .FindDomainClass(typeof(Person));
      EventManagerDirectory events = this.Store.EventManagerDirectory;
      events.ElementAdded
         .Add(observedLinkInfo, new EventHandler<ElementAddedEventArgs>(ParentLinkAddedHandler));
      events.ElementDeleted.Add(observedLinkInfo, new EventHandler<ElementDeletedEventArgs>(ParentLinkDeletedHandler));
      events.ElementPropertyChanged.Add(observedClassInfo, new EventHandler<ElementPropertyChangedEventArgs>(BirthDateChangedHandler));
    }
    // Handler will be called after transaction that creates a link:
    private void ParentLinkAddedHandler(object sender,
                                ElementAddedEventArgs e)
    {
      this.ValidationController.Validate(e.ModelElement,
           ValidationCategories.Save);
    }
    // Called when a link is deleted:
    private void ParentLinkDeletedHandler(object sender,
                                ElementDeletedEventArgs e)
    {
      // Don't apply validation to a deleted item!
      // - Validate store to refresh the error list.
      this.ValidationController.Validate(this.Store,
           ValidationCategories.Save);
    }
    // Called when any property of a Person element changes:
    private void BirthDateChangedHandler(object sender,
                      ElementPropertyChangedEventArgs e)
    {
      Person person = e.ModelElement as Person;
      // Not interested in changes in other properties:
      if (e.DomainProperty.Id != Person.BirthYearDomainPropertyId)
          return;

      // Validate all parent links to and from the person:
      this.ValidationController.Validate(
        ParentsHaveChildren.GetLinksToParents(person)
        .Concat(ParentsHaveChildren.GetLinksToChildren(person))
        , ValidationCategories.Save);
    }
  }
}
```

 ハンドラーはリンクまたは要素に影響する、元に戻す操作またはやり直し操作の後でも呼び出されます。

## <a name="custom-validation-categories"></a><a name="custom"></a> カスタム検証カテゴリ
 「メニュー」や「開く」といった標準の検証カテゴリに加えて、独自のカテゴリを定義できます。 これらのカテゴリをプログラム コードから呼び出すことができます。 ユーザーはそれらを直接呼び出すことができません。

 カスタム カテゴリの一般的な使用法は、モデルが特定のツールの事前条件を満たすかどうかをテストするカテゴリを定義することです。

 特定のカテゴリに検証メソッドを追加するには、プレフィックスとして次のような属性を使用します。

```csharp
[ValidationMethod(CustomCategory = "PreconditionsForGeneratePartsList")]
[ValidationMethod(ValidationCategory.Menu)]
private void TestForCircularLinks(ValidationContext context)
{...}
```

> [!NOTE]
> メソッドのプレフィックスには任意の数の `[ValidationMethod()]` 属性を使用できます。 メソッドをカスタム カテゴリと標準カテゴリの両方に追加できます。

 カスタム検証を呼び出すには次のようにします。

```csharp

// Invoke all validation methods in a custom category:
validationController.ValidateCustom
  (store, // or a list of model elements
   "PreconditionsForGeneratePartsList");
```

## <a name="alternatives-to-validation"></a><a name="alternatives"></a> 検証の代替手段
 検証制約はエラーを報告しますが、モデルを変更しません。 代わりに、モデルが無効になることを防ぐ場合、他の手法を使用できます。

 ただし、これらの手法は推奨されません。 通常、無効なモデルの修正方法をユーザーに決めてもらう方が適切です。

 **変更を調整して、モデルの有効性を復元します。** たとえば、ユーザーが許容される最大値を超えてプロパティを設定した場合、プロパティを最大値にリセットできます。 そのためには、規則を定義します。 詳細については、「 [ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

 **無効な変更が試みられた場合、トランザクションをロールバックします。** この目的のために規則を定義することもできますが、場合によっては、プロパティハンドラー **OnValueChanging ()** をオーバーライドしたり、トランザクションをロールバックするためのなどのメソッドをオーバーライドしたりすることができ `OnDeleted().` `this.Store.TransactionManager.CurrentTransaction.Rollback().` ます。詳細については、「 [ドメインプロパティ値の変更ハンドラー](../modeling/domain-property-value-change-handlers.md)」を参照してください。

> [!WARNING]
> 変更が調整またはロールバックされたことをユーザーが認識できるようにします。 たとえば、`System.Windows.Forms.MessageBox.Show("message").` を使用します

## <a name="see-also"></a>こちらもご覧ください

- [プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [イベント ハンドラーによって変更内容がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)
