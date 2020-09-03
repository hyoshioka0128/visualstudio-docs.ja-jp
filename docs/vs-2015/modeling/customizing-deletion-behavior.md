---
title: 削除動作のカスタマイズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.deletebehavior
helpviewer_keywords:
- Domain-Specific Language, deletion
ms.assetid: c6bf088d-52c6-4817-af45-ddae745bb5a9
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9d0dcfc5724e87d57d2803b9b64a6eb121314b99
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655041"
---
# <a name="customizing-deletion-behavior"></a>削除動作のカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通常、要素を削除すると、関連する要素も削除されます。 接続されたすべてのリレーションシップと子要素が削除されます。 この動作は、 *削除の伝達*という名前です。 削除の伝達をカスタマイズできます。たとえば、追加の関連要素を削除することを準備できます。 プログラム コードを作成して、モデルの状態に応じた削除の伝達を実現できます。 削除に応じて他の変更を発生させることもできます。

 このトピックのセクションは次のとおりです。

- [既定の削除動作](#default)

- [ロールの削除伝達の設定オプション](#property)

- [削除クロージャのオーバーライド](#closure) –この手法は、削除によって隣接する要素が削除される可能性がある場合に使用します。

- [Ondeleting と ondeleting の使用](#ondeleting) –これらのメソッドを使用して、応答にストアの内部または外部の値の更新などの他のアクションを含めることができます。

- [削除ルール](#rules) –ルールを使用して、ストア内の任意の種類の更新プログラムを伝達します。変更すると、他の変更が生じる可能性があります。

- [削除イベント](#rules) –ストアイベントを使用して、ストアの外部に更新を伝達します (他のドキュメントなど) [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

- [結合](#unmerge) 解除–結合操作を使用して、子要素を親にアタッチしたマージ操作を元に戻します。

## <a name="default-deletion-behavior"></a><a name="default"></a> 既定の削除動作
 既定では、次の規則が削除の伝達を制御します。

- 要素が削除された場合、埋め込まれたすべての要素も削除されます。 埋め込まれた要素は、この要素がソースである埋め込みリレーションシップのターゲットです。 たとえば、 **アルバム** から **楽曲**への埋め込みリレーションシップがある場合、特定のアルバムが削除されると、そのすべての曲も削除されます。

     対照的に、ソングを削除してもアルバムは削除されません。

- 既定では、削除は参照リレーションシップに沿って伝達されません。 参照リレーションシップが**アルバム**から**アーティスト**に関連付けられている場合、**アルバムを削除**しても関連するアーティストは削除されず、アーティストを削除してもアルバムは削除されません。

     ただし、削除は一部の組み込みリレーションシップに沿って伝達されます。 たとえば、モデル要素が削除されると、その図形も図から削除されます。 要素を図形は `PresentationViewsSubject` 参照リレーションシップによって関連付けられています。

- ソース ロールまたはターゲット ロールのいずれかで要素に接続されたすべてのリレーションシップは削除されます。 反対のロールの要素のロール プロパティには削除された要素が含まれなくなります。

## <a name="setting-the-propagate-delete-option-of-a-role"></a><a name="property"></a> ロールの [削除の反映] オプションの設定
 削除によって参照リレーションシップに沿った伝達または埋め込まれた子から親への伝達を発生させることができます。

#### <a name="to-set-delete-propagation"></a>削除の伝達を設定するには

1. DSL 定義図で、削除する *ロール* を選択します。 ロールはドメイン リレーションシップ ボックスの左側または右側の線で表されます。

    たとえば、アルバムが削除された場合は常に関連するアーチストも削除されるように指定する場合、ドメイン クラス Artist に接続されたロールを選択します。

2. プロパティウィンドウで、[削除の **伝達** ] プロパティを設定します。

3. F5 キーを押して、次のことを検証します。

   - このリレーションシップのインスタンスが削除されると、選択したロールの要素も削除されます。

   - 反対のロールの要素が削除されると、このリレーションシップのインスタンスは削除され、このロールの関連要素は削除されます。

   [ **DSL の詳細**] ウィンドウで [**削除の伝達**] オプションを表示することもできます。 ドメインクラスを選択し、[DSL の詳細] ウィンドウで、ウィンドウの横にあるボタンをクリックして [ **削除の動作** ] ページを開きます。 各リレーションシップの逆の役割については、[ **反映** ] オプションが表示されます。 [ **スタイルの削除** ] 列は、[ **反映** ] オプションが既定の設定であるかどうかを示しますが、別の効果はありません。

## <a name="delete-propagation-by-using-program-code"></a>プログラム コードを使用する削除の伝達
 DSL 定義ファイル内のオプションにより選択できるのは、削除がすぐ隣に伝達するかどうかのみです。 より複雑な削除の伝達のしくみを実装するために、プログラム コードを作成できます。

> [!NOTE]
> DSL 定義にプログラムコードを追加するには、 **dsl** プロジェクトで別のコードファイルを作成し、部分定義を記述して、生成されたコードフォルダー内のクラスを拡張します。 詳細については、「 [ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)」を参照してください。

## <a name="defining-a-delete-closure"></a><a name="closure"></a> 削除クロージャの定義
 削除操作では、 _モデル_**DeleteClosure** のクラスを使用して、最初の選択によって、削除する要素を決定します。 これは `ShouldVisitRelationship()` および `ShouldVisitRolePlayer()` を繰り返し呼び出し、リレーションシップのグラフを検索します。 これらのメソッドをオーバーライドできます。 ShouldVisitRolePlayer はリンクの ID およびリンクのロールの一方における要素とともに提供されます。 次のいずれかの値を返す必要があります。

- **VisitorFilterResult**–要素を削除する必要があり、ウォーカーは要素の他のリンクを試すために処理を続行する必要があります。

- **VisitorFilterResult** –別のクエリが削除する必要があるという応答がない場合は、要素を削除しないでください。

- VisitorFilterResult –別のクエリが**Yes**に応答する場合でも、要素を削除しないようにする必要があり**ます。** また、ウォーカーは要素の他のリンクを試すことができません。

```
// When a musician is deleted, delete their albums with a low rating.
// Override methods in <YourDsl>DeleteClosure in DomainModel.cs
partial class MusicLibDeleteClosure
{
  public override VisitorFilterResult ShouldVisitRolePlayer
    (ElementWalker walker, ModelElement sourceElement, ElementLink elementLink,
    DomainRoleInfo targetDomainRole, ModelElement targetRolePlayer)
  {
    ArtistAppearsInAlbum link = elementLink as ArtistAppearsInAlbum;
    if (link != null
       && targetDomainRole.RolePlayer.Id == Album.DomainClassId)
    {
      // Count other unvisited links to the Album of this link.
      if (ArtistAppearsInAlbum.GetLinksToArtists(link.Album)
              .Where(linkAlbumArtist =>
                     linkAlbumArtist != link &&
                     !walker.Visited(linkAlbumArtist))
              .Count() == 0)
      {
        // Should delete this role player:
        return VisitorFilterResult.Yes;
      }
      else
        // Don’t delete unless another relationship deletes it:
        return VisitorFilterResult.DoNotCare;
    }
    else
    {
      // Test for and respond to other relationships and roles here.

      // Not the relationship or role we’re interested in.
      return base.ShouldVisitRolePlayer(walker, sourceElement,
             elementLink, targetDomainRole, targetRolePlayer);
    }
  }
}

```

 このクロージャ手法により、削除する要素をリンクのセットが削除が始まる前に決定されることを確実にします。 また、ウォーカーはクロージャの結果をモデルの他の部分からの結果と結合します。

 ただし、この手法は削除がリレーションシップのグラフ内の隣にあるものにのみ影響することを仮定しています。この方法を使用してモデルの別の部分にある要素を削除することはできません。 削除に応じて要素を追加したり他の変更を実行したりする場合には使用できません。

## <a name="using-ondeleting-and-ondeleted"></a><a name="ondeleting"></a> Ondeleting と Ondeleting の使用
 ドメイン クラスまたはドメイン リレーションシップのいずれかで、`OnDeleting()` または `OnDeleted()` をオーバーライドできます。

1. <xref:Microsoft.VisualStudio.Modeling.ModelElement.OnDeleting%2A> は、要素が削除されようとしているときに、そのリレーションシップが切断される前に呼び出されます。 まだ他の要素に対して移動可能で、`store.ElementDirectory` の中にあります。

    同時にいくつかの要素が削除される場合、削除の実行前にそれらすべてに対して OnDeleting が呼び出されます。

    `IsDeleting` が true です。

2. <xref:Microsoft.VisualStudio.Modeling.ModelElement.OnDeleted%2A> は、要素が削除されたときに呼び出されます。 CLR ヒープ内に留まるので、必要があれば Undo を実行できますが、他の要素からのリンクは解除され、`store.ElementDirectory` から削除されます。 リレーションシップの場合、ロールは引き続き古いロールプレーヤーを参照します。`IsDeleted` が true です。

3. OnDeleting および OnDeleted は要素の作成後にユーザーが Undo を起動するとき、および以前の削除が Redo で繰り返されるときに呼び出されます。 これらの場合にストア要素の更新を回避するには `this.Store.InUndoRedoOrRollback` を使用します。 詳細については、「 [方法: トランザクションを使用](../modeling/how-to-use-transactions-to-update-the-model.md)してモデルを更新する」を参照してください。

   たとえば、次のコードでは、最後の子 Song が削除されると Album が削除されます。

```

// Delete the parent Album when the last Song is deleted.
// Override methods in the embedding relationship between Album and Song:
partial class AlbumHasSongs
{
  protected override void OnDeleted()
  {
    base.OnDeleted();
    // Don't perform in-store actions in undo:
    if (this.Store.InUndoRedoOrRollback) return;
    // Relationship source and target still work:
    // Don't bother if source is already on its way out:
    if (!this.Album.IsDeleting && !this.Album.IsDeleted)
    {
      if (this.Album.Songs.Count == 0)
      {
        this.Album.Delete();
} } } }

```

 多くの場合、ロール要素よりもリレーションシップの削除からトリガーする方が有用です。なぜなら、要素の削除時とリレーションシップ自体の削除時の両方で機能するからです。 ただし、参照リレーションシップの場合、関連要素が削除された場合に削除が伝達され、リレーションシップ自体が削除された場合は伝達されないようにすることをお勧めします。 次の例では、最後の貢献 Artist が削除されると Album が削除されますが、リレーションシップが削除されても応答しません。

```
using System.Linq; ...
// Assumes a many-many reference relationship
// between Artist and Album.
partial class Artist
{
  protected override void OnDeleting()
  {
    base.OnDeleting();
    if (this.Store.InUndoRedoOrRollback) return;
    List<Album> toDelete = new List<Album>();
    foreach (Album album in this.Albums)
    {
      if (album.Artists.Where(artist => !artist.IsDeleting)
                        .Count() == 0)
      {
        toDelete.Add(album);
      }
    }
    foreach (Album album in toDelete)
    {
      album.Delete();
} } }

```

 要素で <xref:Microsoft.VisualStudio.Modeling.ModelElement.Delete%2A> を実行すると、OnDeleting および OnDeleted が呼び出されます。 これらのメソッドは常にインラインで実行されます。つまり、実際の削除の直前および直後に実行されます。 作成するコードが複数の要素を削除する場合、それらのすべてで OnDeleting と OnDeleted が交互に呼び出されることになります。

## <a name="deletion-rules-and-events"></a><a name="rules"></a> 削除ルールとイベント
 OnDelete ハンドラーの代わりに、削除規則と削除イベントを定義できます。

1. **削除** および **削除** ルールは、Undo または Redo ではなく、トランザクションでのみトリガーされます。 それらを設定して、削除が実行されるトランザクションの最後に実行されるようにキューに配置できます。 Deleting 規則は常に、キューに配置されているすべての Deleted 規則の前に実行されます。

     規則を使用し、リレーションシップ、図要素、およびそれらのプロパティなど、ストア内の要素にのみ影響する変更を伝達します。 通常、Deleting 規則は削除を伝達するために使用され、Delete 規則は置換要素およびリレーションシップを作成するために使用されます。

     詳細については、「 [ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

2. **削除さ** れたストアイベントは、トランザクションの終了時に呼び出され、元に戻すまたはやり直した後に呼び出されます。 したがって、ファイル、データベース エントリ、または [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 内の他のオブジェクトなど、ストア外のオブジェクトに削除を伝達するために使用されます。

     詳細については、「 [イベントハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

    > [!WARNING]
    > 要素が削除された場合、そのドメイン プロパティ値にアクセスできますが、リレーションシップ リンクに移動できません。 ただし、リレーションシップに deleted イベントを設定した場合、ロール プレーヤーだった 2 つの要素にもアクセスできます。 したがって、モデル要素の削除に応答し、リンクされた要素にアクセスする場合、モデル要素のドメイン クラスの代わりにリレーションシップで delete イベントを設定します。

### <a name="example-deletion-rules"></a>削除規則の例

```
[RuleOn(typeof(Album), FireTime = TimeToFire.TopLevelCommit)]
internal class AlbumDeletingRule : DeletingRule
{
  public override void ElementDeleting(ElementDeletingEventArgs e)
  {
    base.ElementDeleting(e);
    // ...perform tasks to propagate imminent deletion
  }
}
[RuleOn(typeof(Album), FireTime = TimeToFire.TopLevelCommit)]
internal class AlbumDeletedRule : DeleteRule
{
  public override void ElementDeleted(ElementDeletedEventArgs e)
  {
    base.ElementDeleted(e);
    // ...perform tasks such as creating new elements
  }
}

// The rule must be registered:
public partial class MusicLibDomainModel
{
  protected override Type[] GetCustomDomainModelTypes()
  {
    List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
    types.Add(typeof(AlbumDeletingRule));
    types.Add(typeof(AlbumDeletedRule));
    // If you add more rules, list them here.
    return types.ToArray();
  }
}

```

### <a name="example-deleted-event"></a>Deleted イベントの例

```
partial class NestedShapesSampleDocData
{
  protected override void OnDocumentLoaded(EventArgs e)
  {
    base.OnDocumentLoaded(e);
    DomainRelationshipInfo commentRelationship =
          this.Store.DomainDataDirectory
          .FindDomainRelationship(typeof(CommentsReferenceComponents));

    this.Store.EventManagerDirectory.ElementDeleted.Add(commentRelationship,
      new EventHandler<ElementDeletedEventArgs>(CommentLinkDeleted));
  }

  private void CommentLinkDeleted (object sender, ElementDeletedEventArgs e)
  {
    CommentsReferenceComponents link = e.ModelElement as CommentsReferenceComponents;
    Comment comment = link.Comment;
    Component component = link.Subject;
    if (comment.IsDeleted)
    {
      // The link was deleted because the comment was deleted.
      System.Windows.Forms.MessageBox.Show("Removed comment on " + component.Name);
    }
    else
    {
      // It was just the link that was deleted - the comment itself remains.
      System.Windows.Forms.MessageBox.Show("Removed comment link to "
           + component.Name);
    }
  }
}

```

## <a name="unmerge"></a><a name="unmerge"></a> 分割
 子要素をその親にアタッチする操作を *merge*と呼びます。 マージは、新しい要素または要素のグループがツールボックスから作成されたとき、またはモデルの別の部分から移動されたとき、またはクリップボードからコピーされたときに発生します。 マージ操作は親とその新しい子の間に埋め込みリレーションシップを作成するほか、追加のリレーションシップのセットアップ、補助的な要素の作成、および要素内のプロパティ値の設定も可能です。 マージ操作は要素マージ ディレクティブ (EMD) にカプセル化されています。

 EMD は、補完的な *結合* または操作もカプセル化 `MergeDisconnect` します。 マージにより構築された要素のクラスターがある場合、残りの要素を一貫した状態のままにするには、関連する unmerge を使用して、そこから要素を削除することをお勧めします。 通常、unmerge 操作は前のセクションで説明している手法を使用します。

 詳細については、「 [要素の作成および移動をカスタマイズ](../modeling/customizing-element-creation-and-movement.md)する」を参照してください。

## <a name="see-also"></a>参照
 [コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)[要素の作成と移動](../modeling/customizing-element-creation-and-movement.md)[コードを記述してドメイン固有言語をカスタマイズする](../modeling/writing-code-to-customise-a-domain-specific-language.md)
