---
title: イベント ハンドラーによって変更内容がモデル外に反映される
description: 視覚化およびモデリング SDK では、ストアのイベントハンドラーを定義して、ストアの外部のリソースに変更を反映させることができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, events
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9b0780007361115aa485b91db70cc413029a6f8f
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97361678"
---
# <a name="event-handlers-propagate-changes-outside-the-model"></a>イベント ハンドラーによって変更内容がモデル外に反映される

視覚化およびモデリング SDK では、ストアのイベントハンドラーを定義して、ストアの外部にあるリソースに変更を反映することができます。たとえば、ストア以外の変数、ファイル、他のストア内のモデル、その他の Visual Studio 拡張機能などです。 ストアイベントハンドラーは、トリガーイベントが発生したトランザクションの終了後に実行されます。 これらは、元に戻す操作またはやり直し操作でも実行されます。 そのため、ストアのルールとは異なり、ストアのイベントは、ストアの外部にある値を更新する場合に最も役立ちます。 .NET イベントとは異なり、ストアイベントハンドラーはクラスをリッスンするように登録されます。インスタンスごとに個別のハンドラーを登録する必要はありません。 変更を処理するさまざまな方法を選択する方法の詳細については、「 [変更に対する応答と反映](../modeling/responding-to-and-propagating-changes.md)」を参照してください。

グラフィック画面やその他のユーザーインターフェイスコントロールは、ストアイベントによって処理できる外部リソースの例です。

### <a name="to-define-a-store-event"></a>ストアイベントを定義するには

1. 監視するイベントの種類を選択します。 完全な一覧については、のプロパティを参照 <xref:Microsoft.VisualStudio.Modeling.EventManagerDirectory> してください。 各プロパティは、イベントの種類に対応します。 最も頻繁に使用されるイベントの種類は次のとおりです。

    - `ElementAdded` -モデル要素、リレーションシップリンク、シェイプ、またはコネクタが作成されたときにトリガーされます。

    - ElementPropertyChanged-ドメインプロパティの値が変更されたときにトリガーされ `Normal` ます。 イベントは、新しい値と古い値が等しくない場合にのみトリガーされます。 イベントは、計算されたストレージプロパティとカスタムストレージプロパティには適用できません。

         リレーションシップリンクに対応するロールプロパティには適用できません。 代わりに、を使用し `ElementAdded` てドメインリレーションシップを監視します。

    - `ElementDeleted` -モデル要素、リレーションシップ、図形、またはコネクタが削除された後にトリガーされます。 要素のプロパティ値には引き続きアクセスできますが、他の要素との関係はありません。

2. **Dslpackage** プロジェクト内の別のコードファイルに _dsl_**docdata** の部分クラス定義を追加します。

3. 次の例に示すように、イベントのコードをメソッドとして記述します。 にアクセスする `static` 場合を除き、にすることができ `DocData` ます。

4. `OnDocumentLoaded()`ハンドラーを登録するには、をオーバーライドします。 複数のハンドラーがある場合は、それらすべてを同じ場所に登録できます。

登録コードの場所は重要ではありません。 `DocView.LoadView()` は、別の場所です。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualStudio.Modeling;

namespace Company.MusicLib
{
  partial class MusicLibDocData
  {
    // Register store events here or in DocView.LoadView().
    protected override void OnDocumentLoaded()
    {
      base.OnDocumentLoaded(); // Don't forget this.

      #region Store event handler registration.
      Store store = this.Store;
      EventManagerDirectory emd = store.EventManagerDirectory;
      DomainRelationshipInfo linkInfo = store.DomainDataDirectory
          .FindDomainRelationship(typeof(ArtistAppearsInAlbum));
      emd.ElementAdded.Add(linkInfo,
          new EventHandler<ElementAddedEventArgs>(AddLink));
      emd.ElementDeleted.Add(linkInfo,
          new EventHandler<ElementDeletedEventArgs>(RemoveLink));

      #endregion Store event handlers.
    }

    private void AddLink(object sender, ElementAddedEventArgs e)
    {
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;
      if (link != null)
            ExternalDatabase.Add(link.Artist.Name, link.Album.Title);
    }
    private void RemoveLink(object sender, ElementDeletedEventArgs e)
    {
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;
      if (link != null)
            ExternalDatabase.Delete(link.Artist.Name, link.Album.Title);
    }
  }
}
```

## <a name="use-events-to-make-undoable-adjustments-in-the-store"></a>イベントを使用して、ストアで取り消し可能な調整を行う

ストアイベントは、トランザクションがコミットされた後にイベントハンドラーが実行されるため、通常、ストア内の変更を反映するためには使用されません。 代わりに、ストアルールを使用します。 詳細については、「 [ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

ただし、ユーザーが元のイベントとは別に追加の更新を元に戻すことができるようにする場合は、イベントハンドラーを使用してストアに追加の更新を行うことができます。 たとえば、小文字がアルバムタイトルの通常の規則であるとします。 ユーザーが大文字で入力した後、タイトルを小文字に修正するストアイベントハンドラーを作成できます。 ただし、ユーザーは、[元に戻す] コマンドを使用して修正をキャンセルし、大文字を復元できます。 2番目の元に戻すと、ユーザーの変更が削除されます。

これに対し、同じことを行うためにストアの規則を記述した場合、ユーザーの変更と修正は同じトランザクション内で行われるため、ユーザーは元の変更を失うことなく調整を元に戻すことができません。

```csharp
partial class MusicLibDocView
{
    // Register store events here or in DocData.OnDocumentLoaded().
    protected override void LoadView()
    {
      /* Register store event handler for Album Title property. */
      // Get reflection data for property:
      DomainPropertyInfo propertyInfo =
        this.DocData.Store.DomainDataDirectory
        .FindDomainProperty(Album.TitleDomainPropertyId);
      // Add to property handler list:
      this.DocData.Store.EventManagerDirectory
        .ElementPropertyChanged.Add(propertyInfo,
        new EventHandler<ElementPropertyChangedEventArgs>
             (AlbumTitleAdjuster));

      /*
      // Alternatively, you can set one handler for
      // all properties of a class.
      // Your handler has to determine which property changed.
      DomainClassInfo classInfo = this.Store.DomainDataDirectory
           .FindDomainClass(typeof(Album));
      this.Store.EventManagerDirectory
          .ElementPropertyChanged.Add(classInfo,
        new EventHandler<ElementPropertyChangedEventArgs>
             (AlbumTitleAdjuster));
       */
      return base.LoadView();
    }

// Undoable adjustment after a property is changed.
// Method can be static since no local access.
private static void AlbumTitleAdjuster(object sender,
         ElementPropertyChangedEventArgs e)
{
  Album album = e.ModelElement as Album;
  Store store = album.Store;

  // We mustn't update the store in an Undo:
  if (store.InUndoRedoOrRollback
      || store.InSerializationTransaction)
      return;

  if (e.DomainProperty.Id == Album.TitleDomainPropertyId)
  {
    string newValue = (string)e.NewValue;
    string lowerCase = newValue.ToLowerInvariant();
    if (!newValue.Equals(lowerCase))
    {
      using (Transaction t = store.TransactionManager
            .BeginTransaction("adjust album title"))
      {
        album.Title = lowerCase;
        t.Commit();
      } // Beware! This could trigger the event again.
    }
  }
  // else other properties of this class.
}
```

ストアを更新するイベントを記述する場合は、次のようにします。

- `store.InUndoRedoOrRollback`元に戻すでモデル要素を変更しないようにするには、を使用します。 トランザクションマネージャーは、ストア内のすべてのものを元の状態に戻します。

- `store.InSerializationTransaction`モデルがファイルから読み込まれている間に変更を行わないようにするには、を使用します。

- 変更を加えると、さらにイベントがトリガーされます。 無限ループを避けるようにしてください。

## <a name="store-event-types"></a>イベントの種類を格納する

各イベントの種類は、Store. EventManagerDirectory のコレクションに対応しています。 イベントハンドラーはいつでも追加または削除できますが、通常はドキュメントの読み込み時に追加します。

|`EventManagerDirectory` プロパティ名|実行するタイミング|
|-|-|
|追加される element|ドメインクラス、ドメインリレーションシップ、図形、コネクタ、または図のインスタンスが作成されます。|
|ElementDeleted|モデル要素がストアの要素ディレクトリから削除されており、リレーションシップのソースまたはターゲットではなくなっています。 要素は実際にはメモリから削除されませんが、将来の元に戻す場合に保持されます。|
|Elementを開始しました|外側のトランザクションの終了時に呼び出されます。|
|Elementの終了|他のすべてのイベントが処理されたときに呼び出されます。|
|ElementMoved|モデル要素が1つのストアパーティションから別のストアパーティションに移動されました。<br /><br /> これは、図の図形の位置とは関係ありません。|
|ElementPropertyChanged|ドメインプロパティの値が変更されました。 これは、古い値と新しい値が等しくない場合にのみ実行されます。|
|RolePlayerChanged|リレーションシップの2つのロール (両端) のいずれかが、新しい要素を参照しています。|
|RolePlayerOrderChanged|複数要素の接続性が1より大きいロールでは、リンクの順序が変更されています。|
|トランザクションの開始||
|トランザクションコミット済み||
|トランザクションロールバック||

## <a name="see-also"></a>関連項目

- [変更内容への対応および変更内容の反映](../modeling/responding-to-and-propagating-changes.md)
- [サンプルコード: サーキットダイアグラム](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
