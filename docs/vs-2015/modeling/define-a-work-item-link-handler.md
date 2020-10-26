---
title: 作業項目リンクハンドラーを定義する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API
ms.assetid: d52e0bbf-0166-4bb4-a2e3-cefed6188875
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 380aaa5bed1e30c549334bc004ea38e3f0bdb762
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669937"
---
# <a name="define-a-work-item-link-handler"></a>作業項目リンク ハンドラーを定義する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユーザーが UML モデル要素と作業項目の間のリンクを作成または削除したときに応答する Visual Studio Integration Extension を作成できます。 たとえば、ユーザーが新しい作業項目をモデル要素にリンクしたときに、コードによって、その作業項目のフィールドをモデル内の値で初期化することもできます。

## <a name="set-up-a-uml-extension-solution"></a>UML 拡張機能ソリューションの設定
 これにより、ハンドラーを開発した後に他のユーザーに配布できます。 次に示す 2 つの Visual Studio プロジェクトを設定する必要があります。

- リンク ハンドラーのコードを含むクラス ライブラリ プロジェクト。

- コマンドをインストールするためのコンテナーとして動作する VSIX プロジェクト。 必要に応じて、同じ VSIX に他のコンポーネントを追加できます。

#### <a name="to-set-up-the-visual-studio-solution"></a>Visual Studio ソリューションを設定するには

1. クラス ライブラリ プロジェクトを作成し、それを既存の VSIX ソリューションに追加するか、または新規のソリューションを作成します。

    1. **[ファイル]** メニューで、**[新規作成]**、**[プロジェクト]** の順に選択します。

    2. [ **インストールされたテンプレート**] の [ **Visual C#** ] または [ **Visual Basic**] を展開し、中央の列で [ **クラスライブラリ**] をクリックします。

    3. 新しいソリューションを作成するか、既に開いている VSIX ソリューションにコンポーネントを追加するかを **[ソリューション]** に指定します。

    4. プロジェクトの名前と場所を設定し、[OK] をクリックします。

2. ソリューションに既存の VSIX プロジェクトが存在しない場合は、新しく作成します。

    1. **ソリューションエクスプローラー**で、ソリューションのショートカットメニューの [**追加**]、[**新しいプロジェクト**] の順に選択します。

    2. **[インストールされたテンプレート]** の **[Visual C#]** または **[Visual Basic]** を展開し、 **[機能拡張]** をクリックします。 中央の列で、 **[VSIX プロジェクト]** をクリックします。

3. VSIX プロジェクトをソリューションのスタートアップ プロジェクトとして設定します。

    - ソリューションエクスプローラーで、VSIX プロジェクトのショートカットメニューの [ **スタートアッププロジェクトに設定**] を選択します。

4. **Source.extension.vsixmanifest**の [**コンテンツ**] で、クラスライブラリプロジェクトを MEF コンポーネントとして追加します。

    1. **[メタデータ]** タブで、VSIX の名前を設定します。

    2. **[インストールの対象]** タブで、Visual Studio のバージョンを対象として設定します。

    3. **[アセット]** タブで、 **[新規作成]** をクリックし、ダイアログ ボックスで次のように設定します。

         **型**  = **MEF コンポーネント**

         **ソース**  = **現在のソリューション内のプロジェクト**

         **プロジェクト**  = *クラスライブラリプロジェクト*

## <a name="defining-the-work-item-link-handler"></a>作業項目リンク ハンドラーの定義
 次に挙げるタスクはすべてクラス ライブラリ プロジェクトで行います。

### <a name="project-references"></a>プロジェクト参照
 次の [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] アセンブリをプロジェクト参照に追加します。

 `Microsoft.TeamFoundation.WorkItemTracking.Client.dll`

 `Microsoft.VisualStudio.TeamFoundation.WorkItemTracking.dll Microsoft.VisualStudio.Modeling.Sdk.[version]`

 `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml`

 `Microsoft.VisualStudio.Uml.Interfaces`

 `System.ComponentModel.Composition`

 `System.Drawing` -サンプルコードによって使用されます。

 [**参照の追加**] ダイアログの [ **.net** ] タブでこれらの参照のいずれかが見つからない場合は、[参照] タブを使用して、"\Common7\IDE\PrivateAssemblies" という形式で検索し \\ ます。

### <a name="import-the-work-item-namespace"></a>作業項目の名前空間をインポートする
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]プロジェクト**参照**で、次のアセンブリへの参照を追加します。

- Microsoft.TeamFoundation.WorkItemTracking.Client.dll

- Microsoft.VisualStudio.TeamFoundation.WorkItemTracking.dll

  プログラム コードで、次の名前空間をインポートします。

```
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.Uml.Classes;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.TeamFoundation.WorkItemTracking;
using System.Linq;
```

### <a name="define-the-linked-work-item-event-handler"></a>リンクされた作業項目イベント ハンドラーを定義する
 クラス ライブラリ プロジェクトにクラス ファイルを追加し、その内容を次のように設定します。 名前空間およびクラスの名前は必要に応じて変更してください。

```
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.Uml.Classes;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.TeamFoundation.WorkItemTracking;
using System.Linq;

namespace WorkItems
{
  [Export(typeof(ILinkedWorkItemExtension))]
  public class MyWorkItemExtension : ILinkedWorkItemExtension
  {
    // Called before a new work item is edited by the user.
    // Use this to initialize work item fields from the model element.
    public void OnWorkItemCreated(System.Collections.Generic.IEnumerable<IElement> elementsToBeLinked, IWorkItemDocument workItemDocument)
    {
      INamedElement namedElement =
            elementsToBeLinked.First() as INamedElement;
      if (namedElement != null)
        workItemDocument.Item.Title = namedElement.Name;

    }

    // Called when any work item is linked to a model element.
    public void OnWorkItemLinked(System.Collections.Generic.IEnumerable<IElement> elements, string serverUri, int workItemId)
    {
      foreach (IElement element in elements)
        foreach (IShape shape in element.Shapes())
          shape.Color = System.Drawing.Color.Red;
    }

    // Called when a work item is unlinked from a model element.
    public void OnWorkItemRemoved(IElement element, string serverUri, int workItemId)
    {
      foreach (IShape shape in element.Shapes())
        shape.Color = System.Drawing.Color.White;
    }
  }
}
```

## <a name="testing-the-link-handler"></a>リンク ハンドラーのテスト
 テストを行う場合は、リンク ハンドラーをデバッグ モードで実行します。

> [!WARNING]
> 作業項目を作成またはそれにリンクするには、既に TFS ソース コード管理 (SCC) に接続されている必要があります。 別の TFS SCC への接続を開こうとすると、Visual Studio が現在のソリューションを自動的に閉じます。 作業項目を作成またはそれにリンクしようとする前に、適切な SCC に接続されていることを確認してください。 Visual Studio の今後のリリースでは、SCC に接続されていないとメニュー コマンドを使用できません。

#### <a name="to-test-the-link-handler"></a>リンク ハンドラーをテストするには

1. **F5**キーを押すか、 **[デバッグ]** メニューの **[デバッグ開始]** をクリックします。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用のインスタンスが開始します。

     **トラブルシューティング**: 新しいが [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 開始されない場合は、VSIX プロジェクトがソリューションのスタートアッププロジェクトとして設定されていることを確認します。

2. 実験用の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で、モデリング プロジェクトを開くか、または生成し、モデリング図を開くか、または生成します。

3. モデル要素 (UML クラスなど) を生成し、その名前を設定します。

4. 要素を右クリックし、[ **作業項目の作成**] をクリックします。

    - サブメニューに **[Open Team Foundation Server Connection**] が表示されている場合は、プロジェクトを閉じ、適切な TFS に接続して、この手順を再起動する必要があります。

    - サブメニューに作業項目の種類の一覧が表示される場合は、いずれか 1 つをクリックします。

         新しい作業項目フォームが開きます。

5. 前のセクションのサンプル コードを使用した場合は、作業項目のタイトルがモデル要素と同じであることを確認します。 これで、`OnWorkItemCreated()` が動作したことを確認できます。

6. フォームを完成させてから、作業項目を保存して閉じます。

7. 作業項目の色が赤になっていることを確認します。 これで、サンプル コードの `OnWorkItemLinked()` が動作したことを確認できます。

     **トラブルシューティング**: ハンドラーメソッドが実行されていない場合は、次のことを確認します。

    - クラスライブラリプロジェクトは、VSIX プロジェクトの**ソース. extensions. マニフェスト**の**コンテンツ**リストに MEF コンポーネントとして表示されます。

    - 適切な `Export` 属性がハンドラー クラスに追加されており、そのクラスが `ILinkedWorkItemExtension` を実装する。

    - すべての `Import` 属性と `Export` 属性のパラメーターが有効である。

## <a name="about-the-work-item-handler-code"></a>作業項目ハンドラーのコードについて

### <a name="listening-for-new-work-items"></a>新しい作業項目の待機
 `OnWorkItemCreated` は、モデル要素にリンクされる新しい作業項目の作成をユーザーが選択したときに呼び出されます。 コードによって作業項目のフィールドを初期化できます。 初期化された作業項目がユーザーに提示され、ユーザーはフィールドを更新して作業項目を保存できます。 モデル要素へのリンクは、作業項目が正常に保存されるまで作成されません。

```
public void OnWorkItemCreated(
    IEnumerable<IElement> elementsToBeLinked,
    IWorkItemDocument workItem)
{
  INamedElement namedElement =
         elementsToBeLinked.First() as INamedElement;
  if (namedElement != null)
      workItem.Item.Title = namedElement.Name;
}
```

### <a name="listening-for-link-creation"></a>リンクの作成の待機
 `OnWorkItemLinked` は、リンクが作成された直後に呼び出されます。 これは、そのリンクが新しい作業項目へのリンクであるか既存の項目へのリンクであるかにかかわらず呼び出されます。 個々の作業項目ごとに呼び出されます。

```
public void OnWorkItemLinked
        (IEnumerable<IElement> elements,
         string serverUri, // TFS server
         int workItemId)
{
  foreach (IElement element in elements)
    foreach (IShape shape in element.Shapes())
         shape.Color = System.Drawing.Color.Red;
}
```

> [!NOTE]
> この例を動作させるには、`System.Drawing.dll` へのプロジェクト参照を追加し、名前空間 `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation` をインポートする必要があります。 ただし、この追加作業は、`OnWorkItemLinked` のその他の実装には必要ありません。

### <a name="listening-for-link-removal"></a>リンクの削除の待機
 `OnWorkItemRemoved` は、削除された各作業項目リンクの直前に呼び出されます。 モデル要素が削除されると、そのすべてのリンクが削除されます。

```
public void OnWorkItemRemoved
         (IElement element, string serverUri, int workItemId)
{...}
```

## <a name="updating-a-work-item"></a>作業項目の更新
 Team Foundation 名前空間を使用して、作業項目を操作できます。

 次の例を使用するには、プロジェクトの参照設定に次の .NET アセンブリを追加します。

- Microsoft.TeamFoundation.Client.dll

- Microsoft.TeamFoundation.WorkItemTracking.Client.dll

```

using Microsoft.TeamFoundation.Client;
using Microsoft.TeamFoundation.WorkItemTracking.Client;
...
public void OnWorkItemLinked
        (IEnumerable<IElement> elements,
         string serverUri, // TFS server
         int workItemId)
{
  TfsTeamProjectCollection tfs =
        TfsTeamProjectCollectionFactory
            .GetTeamProjectCollection(new Uri(serverUri));
  WorkItemStore workItemStore = new WorkItemStore(tfs);
  WorkItem item = workItemStore.GetWorkItem(workItemId);
  item.Open();
  item.Title = "something";
  item.Save();
} 
```

## <a name="accessing-the-work-item-reference-links"></a>作業項目参照のリンクへのアクセス
 リンクには次のようにアクセスできます。

```
//Get:
string linkString = element.GetReference(ReferenceConstants.WorkItem);
// Set:
element.AddReference(ReferenceConstants.WorkItem, linkString, true);

```

 `linkString` の形式は次のとおりです。

 `string.Format(@"%{0}\{1}#{1}${2}", tfServer, projectCollection, RepositoryGuid, workItem.Id);`

 ここで、

- サーバーの URI は次のとおりです。

   `http://tfServer:8080/tfs/projectCollection`

   `projectCollection` では、大文字と小文字の区別が重要です。

- `RepositoryGuid` は、TFS 接続から取得できます。

  ```csharp
  TfsTeamProjectCollection tpc = TfsTeamProjectCollectionFactory...;
  RepositoryGuid= tpc.InstanceId;

  ```

  参照の詳細については、「 [UML モデル要素への参照文字列のアタッチ](../modeling/attach-reference-strings-to-uml-model-elements.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [TeamFoundation. WorkItemStore. Client.](/previous-versions/visualstudio/visual-studio-2013/bb179850(v=vs.120))
- [モデル要素と作業項目とのリンク](../modeling/link-model-elements-and-work-items.md)
- [UML モデル要素に参照文字列をアタッチする](../modeling/attach-reference-strings-to-uml-model-elements.md)
- [モデリング拡張機能を定義およびインストールする](../modeling/define-and-install-a-modeling-extension.md)
- [UML API を使用したプログラミング](../modeling/programming-with-the-uml-api.md)
