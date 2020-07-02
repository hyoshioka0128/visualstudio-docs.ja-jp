---
title: ロック ポリシーの定義と読み取り専用セグメントの作成
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0778df98ff5f9665da7220fe40972c9a8f8d8e1d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536085"
---
# <a name="defining-a-locking-policy-to-create-read-only-segments"></a>ロック ポリシーの定義と読み取り専用セグメントの作成
Visual Studio の視覚化およびモデリング SDK の不変 API を使用すると、プログラムはドメイン固有言語 (DSL) モデルの一部またはすべてをロックすることができます。これにより、プログラムはそのモデルを読み取ることができますが、変更することはできません。 たとえば、この読み取り専用オプションを使用すると、ユーザーは DSL モデルに注釈を付けて確認することができますが、元のを変更できないようにすることができます。

 さらに、DSL の作成者は、ロックポリシーを定義でき*ます。* ロックポリシーでは、許可されているロック、許可されていないロック、必須のロックを定義します。 たとえば、DSL を発行するときに、サードパーティの開発者が新しいコマンドで拡張できるようにすることができます。 ただし、ロックポリシーを使用して、モデルの指定した部分の読み取り専用の状態を変更できないようにすることもできます。

> [!NOTE]
> ロックポリシーは、リフレクションを使用することによって回避できます。 サードパーティの開発者には明確な境界が用意されていますが、強力なセキュリティは提供されていません。

 詳細とサンプルについては、Visual Studio の[視覚化およびモデリング SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)の web サイトを参照してください。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="setting-and-getting-locks"></a>設定と取得 (ロックを)
 ストア、パーティション、または個々の要素に対してロックを設定できます。 たとえば、次のステートメントを実行すると、モデル要素が削除されるのを防ぐことができます。また、プロパティが変更されるのを防ぐことができます。

```csharp
using Microsoft.VisualStudio.Modeling.Immutability; ...
element.SetLocks(Locks.Delete | Locks.Property);
```

 他のロック値を使用して、リレーションシップ、要素の作成、パーティション間の移動、およびロール内のリンクの順序変更を防止できます。

 ロックは、ユーザー操作とプログラムコードの両方に適用されます。 プログラムコードによって変更が試行されると、が `InvalidOperationException` スローされます。 元に戻す操作またはやり直し操作では、ロックは無視されます。

 を使用して、指定されたセット内の任意のロックが要素にあるかどうかを検出でき `IsLocked(Locks)` ます。また、を使用して、要素の現在のロックセットを取得でき `GetLocks()` ます。

 トランザクションを使用せずにロックを設定できます。 ロックデータベースはストアに含まれていません。 OnValueChanged など、ストアの値の変更に応じてロックを設定した場合は、元に戻す操作の一部である変更を許可する必要があります。

 これらのメソッドは、名前空間で定義されている拡張メソッドです <xref:Microsoft.VisualStudio.Modeling.Immutability> 。

### <a name="locks-on-partitions-and-stores"></a>パーティションおよびストアに対するロック
 ロックは、パーティションとストアにも適用できます。 パーティションに設定されているロックは、パーティション内のすべての要素に適用されます。 したがって、たとえば、次のステートメントを使用すると、独自のロックの状態に関係なく、パーティション内のすべての要素が削除されるのを防ぐことができます。 それでも、などの他のロック `Locks.Property` は、個々の要素に対して設定できます。

```csharp
partition.SetLocks(Locks.Delete);
```

 ストアに設定されているロックは、パーティションおよび要素のロックの設定に関係なく、すべての要素に適用されます。

### <a name="using-locks"></a>ロックの使用
 ロックを使用して、次の例のようなスキームを実装できます。

- コメントを表すものを除き、すべての要素とリレーションシップへの変更を禁止します。 これにより、ユーザーは変更せずにモデルに注釈を付けることができます。

- 既定のパーティションの変更を禁止しますが、ダイアグラムパーティションの変更を許可します。 ユーザーはダイアグラムを再配置できますが、基になるモデルを変更することはできません。

- 別のデータベースに登録されているユーザーのグループを除き、ストアへの変更を禁止します。 他のユーザーの場合、ダイアグラムとモデルは読み取り専用です。

- ダイアグラムのブール型プロパティが true に設定されている場合は、モデルへの変更を許可しません。 そのプロパティを変更するメニューコマンドを提供します。 これにより、ユーザーが誤って変更しないようにすることができます。

- 特定のクラスの要素およびリレーションシップの追加と削除を禁止しますが、プロパティの変更を許可します。 これにより、ユーザーがプロパティを入力できる固定フォームが提供されます。

## <a name="lock-values"></a>値のロック
 ロックは、ストア、パーティション、または個々の ModelElement に設定できます。 Locks は `Flags` 列挙体です。 ' &#124; ' を使用して値を組み合わせることができます。

- ModelElement のロックには、常にそのパーティションのロックが含まれます。

- パーティションのロックには、常にストアのロックが含まれます。

  パーティションまたはストアにロックを設定することはできません。また、同時に個々の要素のロックを無効にすることもできません。

|値|が true であることを意味します。 `IsLocked(Value)`|
|-|-|
|なし|制限はありません。|
|プロパティ|要素のドメインプロパティは変更できません。 これは、リレーションシップのドメインクラスの役割によって生成されるプロパティには適用されません。|
|追加|パーティションまたはストアに新しい要素とリンクを作成することはできません。<br /><br /> には適用されません `ModelElement` 。|
|移動|`element.IsLocked(Move)`が true の場合、またはが true の場合、パーティション間で要素を移動することはできません `targetPartition.IsLocked(Move)` 。|
|削除|要素自体、または削除が反映される要素 (埋め込み要素や図形など) に対してこのロックが設定されている場合、要素を削除することはできません。<br /><br /> を使用すると、 `element.CanDelete()` 要素を削除できるかどうかを検出できます。|
|並び|Roleplayer でのリンクの順序を変更することはできません。|
|RolePlayer|この要素をソースとするリンクのセットは変更できません。 たとえば、新しい要素をこの要素の下に埋め込むことはできません。 これは、この要素がターゲットであるリンクには影響しません。<br /><br /> この要素がリンクの場合、ソースとターゲットは影響を受けません。|
|All|他の値のビットごとの OR。|

## <a name="locking-policies"></a>ロックポリシー
 DSL の作成者は、*ロックポリシー*を定義できます。 ロックポリシーは、特定のロックが設定されないようにするか、特定のロックを設定する必要があるように、SetLocks () の操作を軽減します。 通常、ロックポリシーを使用して、ユーザーまたは開発者が誤って DSL の使用を contravening ことを防ぐことができます。これは、変数を宣言する場合と同じ `private` です。

 また、ロックポリシーを使用して、要素の型に依存するすべての要素にロックを設定することもできます。 これは、 `SetLocks(Locks.None)` 要素が最初に作成されたとき、またはファイルから逆シリアル化されたときにが常に呼び出されるためです。

 ただし、ポリシーを使用して、要素の有効期間中のロックを変更することはできません。 この効果を実現するには、の呼び出しを使用する必要があり `SetLocks()` ます。

 ロックポリシーを定義するには、次のことを行う必要があります。

- <xref:Microsoft.VisualStudio.Modeling.Immutability.ILockingPolicy> を実装するクラスを作成します。

- このクラスを、DSL の DocData で利用できるサービスに追加します。

### <a name="to-define-a-locking-policy"></a>ロックポリシーを定義するには
 <xref:Microsoft.VisualStudio.Modeling.Immutability.ILockingPolicy>には次の定義があります。

```csharp
public interface ILockingPolicy
{
  Locks RefineLocks(ModelElement element, Locks proposedLocks);
  Locks RefineLocks(Partition partition, Locks proposedLocks);
  Locks RefineLocks(Store store, Locks proposedLocks);
}
```

 これらのメソッドは、 `SetLocks()` Store、Partition、または ModelElement の呼び出しが行われたときに呼び出されます。 各メソッドには、推奨されるロックのセットが用意されています。 提案されたセットを返すことも、ロックを追加および削除することもできます。

 次に例を示します。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Immutability;
namespace Company.YourDsl.DslPackage // Change
{
  public class MyLockingPolicy : ILockingPolicy
  {
    /// <summary>
    /// Moderate SetLocks(this ModelElement target, Locks locks)
    /// </summary>
    /// <param name="element">target</param>
    /// <param name="proposedLocks">locks</param>
    /// <returns></returns>
    public Locks RefineLocks(ModelElement element, Locks proposedLocks)
    {
      // In my policy, users can never delete an element,
      // and other developers cannot easily change that:
      return proposedLocks | Locks.Delete);
    }
    public Locks RefineLocks(Store store, Locks proposedLocks)
    {
      // Only one user can change this model:
      return Environment.UserName == "aUser"
           ? proposedLocks : Locks.All;
    }
```

 他のコードがを呼び出す場合でも、ユーザーが常に要素を削除できるようにするには`SetLocks(Lock.Delete):`

 `return proposedLocks & (Locks.All ^ Locks.Delete);`

 MyClass のすべての要素のすべてのプロパティの変更を禁止するには、次のようにします。

 `return element is MyClass ? (proposedLocks | Locks.Property) : proposedLocks;`

### <a name="to-make-your-policy-available-as-a-service"></a>ポリシーをサービスとして使用できるようにするには
 プロジェクトで `DslPackage` 、次の例のようなコードを含む新しいファイルを追加します。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Immutability;
namespace Company.YourDsl.DslPackage // Change
{
  // Override the DocData GetService() for this DSL.
  internal partial class YourDslDocData // Change
  {
    /// <summary>
    /// Custom locking policy cache.
    /// </summary>
    private ILockingPolicy myLockingPolicy = null;

    /// <summary>
    /// Called when a service is requested.
    /// </summary>
    /// <param name="serviceType">Service requested</param>
    /// <returns>Service implementation</returns>
    public override object GetService(System.Type serviceType)
    {
      if (serviceType == typeof(SLockingPolicy)
       || serviceType == typeof(ILockingPolicy))
      {
        if (myLockingPolicy == null)
        {
          myLockingPolicy = new MyLockingPolicy();
        }
        return myLockingPolicy;
      }
      // Request is for some other service.
      return base.GetService(serviceType);
    }
}
```
