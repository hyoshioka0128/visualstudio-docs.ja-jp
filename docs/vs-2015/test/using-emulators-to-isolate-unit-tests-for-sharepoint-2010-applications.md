---
title: SharePoint 2010 アプリケーションの単体テストを分離するためのエミュレーターの使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: b681164c-c87a-4bd7-be48-ed77e1578471
caps.latest.revision: 17
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cc3560c1cbcebea9f61465240cd4e2c7a0f811f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667464"
---
# <a name="using-emulators-to-isolate-unit-tests-for-sharepoint-2010-applications"></a>Sharepoint 2010 アプリケーションの単体テストを分離するためのエミュレーターの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft.SharePoint.Emulators パッケージには、Microsoft SharePoint 2010 アプリケーションの分離単体テストの作成に役立つ一連のライブラリが用意されています。 エミュレーターは、[Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md) 分離フレームワークで [shim](../test/using-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing.md) を使用して、SharePoint API の最も一般的なオブジェクトおよびメソッドを模倣する、軽量なメモリ内オブジェクトを作成します。 SharePoint メソッドがエミュレートされていない場合、またはエミュレーターの既定の動作を変更する場合は、Fakes shim を作成して必要な結果を提供できます。

 既存のテスト メソッドとクラスは、エミュレーターのコンテキストで実行されるように容易に変換できます。 この機能を使用すると、二重用途のテストを作成できます。 二重用途のテストは、実際の SharePoint API に対する統合テストと、エミュレーターを使用する分離単体テストを切り替えることができます。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容
 [必要条件](#BKMK_Requirements)

 [AppointmentsWebPart の例](#BKMK_The_AppointmentsWebPart_example)

 [既存のテストを変換する](#BKMK_Converting_an_existing_test)

- [テストプロジェクトへのエミュレーターパッケージの追加](#BKMK_Adding_the_Emulators_package_to_a_test_project)

- [エミュレーションを使用したテストメソッドの実行](#BKMK__Running_a_test_method_in_the_emulation_context)

  [二重用途のクラスとメソッドの作成](#BKMK_Creating_dual_use_classes_and_methods)

  [TestInitialize 属性と Testinitialize 属性を使用して二重用途のテストクラスを作成する](#BKMK_Using_TestInitialize_and_TestCleanup_attributes_to_create_a_dual_use_test_class)

  [エミュレートされていない SharePoint メソッドを処理する](#BKMK_Handling_non_emulated_SharePoint_methods)

  [新しいエミュレーション テストの作成と概要](#BKMK_Writing_emulation_tests_from_scratch__and_a_summary)

  [例](#BKMK_Example)

  [エミュレートされた SharePoint の型](#BKMK_Emulated_SharePoint_types)

## <a name="requirements"></a><a name="BKMK_Requirements"></a> 必要条件

- Microsoft SharePoint 2010 (SharePoint 2010 Server または SharePoint 2010 Foundation)

- Microsoft Visual Studio Enterprise

- Microsoft SharePoint Emulators NuGet パッケージ

  また、[Visual Studio での単体テストの基本](../test/unit-test-basics.md)をよく理解しておく必要があるほか、[Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md) に関する知識も必要です。

## <a name="the-appointmentswebpart-example"></a><a name="BKMK_The_AppointmentsWebPart_example"></a> AppointmentsWebPart の例
 AppointmentsWebPart を使用すると、予定の SharePoint リストを表示および管理できます。

 ![予定 Web パーツ](../test/media/ut-emulators-appointmentswebpart.png "UT_EMULATORS_AppointmentsWebPart")

 この例では、Web パーツの 2 つのメソッドをテストします。

- `ScheduleAppointment` メソッドは、自身に渡されたリスト項目の値を検証し、指定された SharePoint Web にある一覧に新しいエントリを作成します。

- `GetAppointmentsForToday` メソッドは、今日の予定の詳細を返します。

  [このトピックの内容](#BKMK_In_this_topic)

## <a name="converting-an-existing-test"></a><a name="BKMK_Converting_an_existing_test"></a> 既存のテストの変換
 SharePoint コンポーネントの一般的なメソッド テストでは、テスト メソッドにより、一時的なサイトが SharePoint Foundation に作成され、テスト対象のコードが必要とする SharePoint コンポーネントが追加されます。 その後、コンポーネントのインスタンスが作成および実行されます。 このサイトは、テストの終了時に破棄されます。

 テスト対象のコードの `ScheduleAppointment` メソッドは、ほとんどの場合、そのコンポーネントに対して記述された最初のメソッドの 1 つです。

```
// method under test
public bool ScheduleAppointment(SPWeb web, string listName, string name,
    string phone, string email, string age, DateTime date, out string errorMsg)
{
    errorMsg = string.Empty;
    var badFormat = this.checkInput(name, phone, email, age);
    if (badFormat)
    {
        errorMsg = "Bad Format";
        return false;
    }
    var exists = this.CheckDuplicate(listName, web, name, phone, email, age, date);
    if (exists)
    {
        errorMsg = "Item already exists";
        return false;
    }
    SPListItemCollection items = web.Lists[listName].Items;
    // create item and populate fields
    SPListItem item = items.Add();
    item["Name"] = name;
    item["Phone"] = phone;
    item["Email"] = email;
    item["Age"] = age;
    item["Date"] = date.ToString("D");
    item.Update();
    return true;
}

```

 `ScheduleAppointment` メソッドの機能の最初のテストは次のようになります。

```csharp

[TestMethod]
public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
{
    using( var site = new SPSite("http://localhost"))
    using (var webPart = new BookAnAppointmentWebPart())
    {
        // Arrange
        string errorMsg = string.Empty;
        DateTime date = DateTime.Now;
        SPList list = AddListToSiteHelper(site);

        // Act
        bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
            "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
            out errorMsg);
        list.Delete();

        // Assert
        Assert.IsTrue(success);
    }
}
```

 このテスト メソッドは、`ScheduleAppointment` メソッドによって新しいエントリが一覧に適切に追加されたかどうかを検証しますが、コードの特定の動作のテストというよりも、どちらかというと Web パーツの統合テストです。 このテストは、SharePoint および SharePoint API に対する外部依存関係によって、`ScheduleAppointment` メソッドのユーザー コード以外の理由で失敗することがあります。 また、SharePoint サイトの作成および破棄のオーバーヘッドによりテストが遅くなりすぎて、コード プロセスの一部として実行できなくなることもあります。 すべてのテスト メソッドに対してサイトの設定と破棄を実行しても、効率的な開発者単体テストの作成に関する問題を悪化させるだけです。

 Microsoft SharePoint エミュレーターは、よく使用する SharePoint API の動作を模倣する一連のオブジェクトとメソッド "doubles" を提供します。 エミュレートされたメソッドは SharePoint API の軽量な実装で、SharePoint を実行する必要がありません。 Microsoft Fakes を使用して、SharePoint API への呼び出しを、SharePoint エミュレーターのメソッド doubles に迂回させることで、テストを分離して、必要なコードをテストしているかどうかを確認します。 エミュレートされていない SharePoint のメソッドを呼び出すと、Fake を使用して必要な動作を直接作成できます。

 [このトピックの内容](#BKMK_In_this_topic)

### <a name="adding-the-emulators-package-to-a-test-project"></a><a name="BKMK_Adding_the_Emulators_package_to_a_test_project"></a> テスト プロジェクトに Emulators パッケージを追加する
 SharePoint エミュレーターをテスト プロジェクトに追加するには:

1. ソリューション エクスプローラーでテスト プロジェクトを選択します。

2. ショートカット メニューの **[NuGet パッケージの管理...]** を選択します。

3. `Microsoft.SharePoint.Emulators` の **[オンライン]** カテゴリを検索し、**[インストール]** を選択します。

   ![SharePoint エミュレーター NuGet パッケージ](../test/media/ut-emulators-nuget.png "UT_EMULATORS_Nuget")

   [このトピックの内容](#BKMK_In_this_topic)

### <a name="running-a-test-method-with-emulation"></a><a name="BKMK__Running_a_test_method_in_the_emulation_context"></a> エミュレーションを使用してテスト メソッドを実行する
 パッケージをインストールすると、必要なライブラリへの参照がプロジェクトに追加されます。 既存のテスト クラスでエミュレーターを使いやすくするには、名前空間 `Microsoft.SharePoint.Emulators` と `Microsoft.QualityTools.Testing.Emulators` を追加します。

 テスト メソッドでエミュレーションを有効にするには、`using` オブジェクトを作成する `SharePointEmulationScope` ステートメントでメソッド本体をラップします。 次に例を示します。

```csharp

[TestMethod]
public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
{
    // create the emulation scope with a using statement
    using (new SharePointEmulationScope())
    using( var site = new SPSite("http://localhost"))
    using (var webPart = new BookAnAppointmentWebPart())
    {
        // Arrange
        string errorMsg = string.Empty;
        DateTime date = DateTime.Now;
        SPList list = AddListToSiteHelper(site);

        // Act
        bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
            "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
            out errorMsg);
        list.Delete();

        // Assert
        Assert.IsTrue(success);
    }
}

```

 テスト メソッドが実行されると、エミュレーター ランタイムは、Microsoft Fake を呼び出してコードを SharePoint メソッドに動的に挿入し、これらのメソッドへの呼び出しを、Microsoft.SharePoint.Fakes.dll で宣言されているデリゲートに迂回させます。 Microsoft.SharePoint.Emulators.dll は、エミュレートされたメソッドのデリゲートを実装し、SharePoint の実際の動作を正確に模倣します。 テスト メソッドまたはテスト対象のコンポーネントが SharePoint メソッドを呼び出した結果として生じる動作は、エミュレーションの動作です。

 ![エミュレーターの実行フロー](../test/media/ut-emulators-flowchart.png "UT_EMULATORS_FlowChart")

 [このトピックの内容](#BKMK_In_this_topic)

## <a name="creating-dual-use-classes-and-methods"></a><a name="BKMK_Creating_dual_use_classes_and_methods"></a> 二重用途のクラスおよびメソッドを作成する
 実際の SharePoint API に対する統合テストと、エミュレーターを使用する分離単体テストの両方に使用できるメソッドを作成するには、オーバーロードされたコンストラクター `SharePointEmulationScope(EmulationMode)` を使用して、テスト メソッド コードをラップします。 `EmulationMode` 列挙型の 2 つの値は、スコープがエミュレーターを使用するかどうか  (`EmulationMode.Enabled`)、またはスコープが SharePoint API を使用するかどうか (`EmulationMode.Passthrough`) を指定します。

 たとえば、次のコードは、前回のテストを二重用途に変更する方法を示しています。

```csharp

// class level field specifies emulation mode
private const EmulationMode emulatorMode = EmulationMode.Enabled;

[TestMethod]
public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
{
    // emulation scope determined by emulatorMode
    using( SharePointEmulationScope(emulatorMode))
    using( var site = new SPSite("http://localhost"))
    using (var webPart = new BookAnAppointmentWebPart())
    {
        // Arrange
        string errorMsg = string.Empty;
        DateTime date = DateTime.Now;
        SPList list = AddListToSiteHelper(site);

        // Act
        bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
            "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
            out errorMsg);
        list.Delete();

        // Assert
        Assert.IsTrue(success);
    }
}
```

 [このトピックの内容](#BKMK_In_this_topic)

## <a name="using-testinitialize-and-testcleanup-attributes-to-create-a-dual-use-test-class"></a><a name="BKMK_Using_TestInitialize_and_TestCleanup_attributes_to_create_a_dual_use_test_class"></a> TestInitialize 属性と TestCleanup 属性を使用して二重用途のテスト クラスを作成する
 `SharePointEmulationScope` を使用してクラスのすべてのテスト、またはほとんどのテストを実行すると、クラス レベルの手法を利用して、エミュレーション モードを設定できます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute> および <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute> を使用して属性設定されているテスト クラス メソッドが、スコープを作成および破棄できます。

- クラス レベルで `EmulationMode` を設定すると、`EmulationMode.Enabled` および `EmulationMode.Passthrough` の間のモード変更を自動化できます。

  `[TestInitialize]` を使用して属性設定されているクラス メソッドが、各テスト メソッドの開始時に実行され、`[TestCleanup]` を使用して属性設定されているメソッドが、各テスト メソッドの終了時に実行されます。 クラス レベルで `SharePointEmulationScope` オブジェクトのプライベート フィールドを宣言し、`TestInitialize` 属性付きメソッドで初期化して、`TestCleanup` 属性付きメソッドでオブジェクトを破棄できます。

  任意のメソッドを選択して使用し、`EmulationMode`の選択を自動化できます。 1 つは、プリプロセッサ ディレクティブを使用してシンボルの存在をチェックする方法です。 たとえば、エミュレーターを使用してクラスでテスト メソッドを実行するために、テスト プロジェクト ファイルまたはビルド コマンド ラインで `USE_EMULATION` などのシンボルを定義できます。 シンボルを定義すると、クラス レベルの `EmulationMode` 定数が宣言され、`Enabled` に設定されます。 それ以外の場合、定数は `Passthrough` に設定されます。

  次のテスト クラスの例は、プリプロセッサ ディレクティブ、`TestInitialize` 属性付きメソッド、および `TestCleanup` 属性付きメソッドを使用して、エミュレーション モードを設定する方法を示しています。

```csharp
//namespace declarations
...

namspace MySPAppTests
{
    [TestClass]
    public class BookAnAppointmentWebPartTests
    {

        // emulationScope is a class level field
        private SharePointEmulationScope emulationScope;

        // preprocessor directives determine the value of emulatorMode
        #if USE_EMULATIONprivate const EmulationMode emulatorMode = EmulationMode.Enabled;#elseprivate const EmulationMode emulatorMode = EmulationMode.Passthrough;#endif

        // InitializeTest sets the emulation scope at the beginning of each test method
        [TestInitialize]public void InitializeTest(){this.emulationScope = new SharePointEmulationScope(emulatorMode);}

        // CleanupTest disposes the emulation scope at the end of each test method
        [TestCleanup]public void CleanupTest(){this.emulationScope.Dispose();}

        [TestMethod]
        public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
        {
            // remove the SharePointEmulationScope using statement from the method
            using( var site = new SPSite("http://localhost"))
            using (var webPart = new BookAnAppointmentWebPart())
            {
                // Arrange
                string errorMsg = string.Empty;
                DateTime date = DateTime.Now;
                SPList list = AddListToSiteHelper(site);

                // Act
                bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
                    "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
                    out errorMsg);
                list.Delete()

                // Assert
                Assert.IsTrue(success);
            }
        }

        ...// More tests

    }
}

```

 [このトピックの内容](#BKMK_In_this_topic)

## <a name="handling-non-emulated-sharepoint-methods"></a><a name="BKMK_Handling_non_emulated_SharePoint_methods"></a> エミュレートされていない SharePoint メソッドの処理
 すべての SharePoint 型がエミュレートされるわけではありません。また、エミュレートされた型のすべてのメソッドがエミュレートされるわけでもありません。 テスト対象のコードが、エミュレートされていない SharePoint メソッドを呼び出すと、そのメソッドによって `NotSupportedException` 例外がスローされます。 例外が発生したら、SharePoint メソッドの Fakes shim を追加します。

 **SharePoint Fakes の準備**

 Microsoft Fakes shim を明示的に呼び出すには:

1. エミュレートされていない SharePoint クラスに shim を使用する場合は、Microsoft.SharePoint.fakes ファイルを編集し、shim が使用されたクラスの一覧にそのクラスを追加します。 「[Microsoft Fakes におけるコード生成、コンパイル、および名前付け規則](../test/code-generation-compilation-and-naming-conventions-in-microsoft-fakes.md)」の [stub と shim のコード生成の構成](https://msdn.microsoft.com/library/hh708916.aspx#bkmk_configuring_code_generation_of_stubs)に関するセクションを参照してください。

    ![ソリューション エクスプローラーの Fakes フォルダー](../test/media/ut-emulators-fakesfilefolder.png "UT_EMULATORS_FakesFileFolder")

2. Microsoft SharePoint エミュレーター パッケージのインストール後、Microsoft.SharePoint.Fakes ファイルを編集した場合、少なくとも 1 回はテスト プロジェクトをリビルドします。 プロジェクトをビルドすると、ディスク上のプロジェクト ルート フォルダーに **FakesAssembly** フォルダーが作成され、設定されます。

    ![FakesAssembly フォルダー](../test/media/ut-emulators-fakesassemblyfolder.png "UT_EMULATORS_FakesAssemblyFolder")

3. **FakesAssembly** フォルダーにある **Microsoft.SharePoint.14.0.0.0.Fakes.dll** アセンブリに参照を追加します。

4. (省略可能) 名前空間ディレクティブを、使用する `Microsoft.QualityTools.Testing.Fakes`、`Microsoft.SharePoint.Fakes`、および `Microsoft.SharePoint.Fakes` の入れ子になった名前空間のテスト クラスに追加します。

   **SharePoint メソッドの shim デリゲートの実装**

   この例のプロジェクトでは、`GetAppointmentsForToday` メソッドは [SPList.GetItems (SPQuery)](https://msdn.microsoft.com/library/ms457534.aspx) SharePoint API メソッドを呼び出しています。

```csharp
// method under test
public string GetAppointmentsForToday(string listName, SPWeb web)
{
    SPList list = web.Lists[listName];
    DateTime today = DateTime.Now;
    var listQuery = new SPQuery{Query = String.Format("<Where><Eq><FieldRef Name='Date'/>" +"<Value Type='Text'>{0}</Value>" +"</Eq></Where>", today.ToString("D"))};
    var result = new System.Text.StringBuilder();
    foreach (SPListItem item in list.GetItems(listQuery))
    {
        result.AppendFormat("Name: {0}, Phone: {1}, Email: {2}, Age: {3}, Date: {4}\n",
            item["Name"], item["Phone"], item["Email"], item["Age"], item["Date"]);
    }
    return result.ToString();
}

```

 オーバーロードされた `SPList.GetItems(SPQuery)` メソッドの `GetItems` バージョンはエミュレートされません。 したがって、`GetAppointmentsForToday` では、`SharePoint.Emulation.Scope` の既存のテストをラップできません。 機能するテストを作成するには、テスト対象の結果を返す Fakes デリゲート `ShimSPList.GetItemsSPQuery` の実装を記述する必要があります。

 Fakes デリゲートを実装する既存のテスト メソッド `GetAppointmentsForTodayReturnsOnlyTodaysAppointments` を次のように変更します。 必要な変更については、コメントで説明が示されています。

> [!IMPORTANT]
> テストが `ShimNotSupported` コンテキストで実行されると、Fake shim を明示的に作成するテスト メソッドにより `EmulationMode.Passthrough` 例外がスローされます。 この問題を回避するには、変数を使用して `EmulationMode` 値を設定し、値をテストする `if` ステートメントで Fakes コードをラップします。

```csharp
// class level field to set emulation mode
private const EmulationMode emulatorMode = EmulationMode.Enabled

[TestMethod]
public void GetAppointmentsForTodayReturnsOnlyTodaysAppointments()
{

    // create the emulation scope with a using statement
    using (var emulationScope = new SharePointEmulationScope(emulatorMode))
    using( var site = new SPSite("http://localhost"))
    using (var webPart = new BookAnAppointmentWebPart())
    {
        // Arrange
        DateTime date = DateTime.Now;
        SPList list = AddListToSiteHelper(site);
        // insert 2 items into list
        AddItemsToListHelper(list, new string[] {"Raisa Pokrovskaya", "425-555-0163",
            "raisa@outlook.com", "55", date.ToString("D") });
        AddItemsToListHelper(list, new string[] {"Francis Totten", "313-555-0100",
            "francis@contoso.com", "42", date.AddDays(1).ToString("D") });

        // use Fakes shims only if emulation is enabled
        if (emulatorMode == EmulationMode.Enabled){var sList = new ShimSPList(list);sList.GetItemsSPQuery = (query) =>{var shim = new ShimSPListItemCollection();shim.Bind(new[] { list.Items[0] });return shim.Instance;}}

        // Act
        string result = webPart.GetAppointmentsForToday(list.Title, site.RootWeb);
        list.Delete();

        // Assert
        Assert.IsTrue(result.Contains(String.Format(
            "Name: Raisa Pokrovskaya, Phone: 425-555-0163, Email: raisa@outlook.com," +
            "Age: 55, Date: {0}", date.ToString("D"))));
        Assert.IsFalse(result.Contains("Name: Francis Totten"));
    }
}

```

 このメソッドでは、最初に、エミュレーションが有効になっていることをテストします。 有効になっている場合は、`SPList` リストに対して Fakes shim オブジェクトを作成してから、メソッドを作成して、その `GetItemsSPQuery` デリゲートに割り当てます。 デリゲートは Fake `Bind` メソッドを使用して、呼び出し元に返される `ShimSPListItemCollection` に正しいリスト項目を追加します。

 [このトピックの内容](#BKMK_In_this_topic)

## <a name="writing-emulation-tests-from-scratch-and-a-summary"></a><a name="BKMK_Writing_emulation_tests_from_scratch__and_a_summary"></a> 最初からのエミュレーションテストの作成と概要
 前のセクションで説明したエミュレーション テストおよび二重用途のテストを作成する手法では、既存のテストを変換することを前提としていますが、テストをゼロから記述する手法も使用できます。 次の一覧にこの手法の概要を示します。

- テスト プロジェクトでエミュレーターを使用するには、Microsoft.SharePoint.Emulators NuGet パッケージをプロジェクトに追加します。

- テスト メソッドでエミュレーターを使用するには、メソッドの先頭で `SharePointEmulationScope` オブジェクトを作成します。 サポートされる SharePoint API はすべて、スコープが破棄されるまでエミュレートされます。

- 実際の SharePoint API に記述しているように、テスト コードを記述します。 エミュレーションのコンテキストによって、SharePoint メソッドへの呼び出しはそのメソッドのエミュレーターに自動的に迂回します。

- すべての SharePoint オブジェクトがエミュレートされるわけではありません。また、エミュレートされたオブジェクトのすべてのメソッドがエミュレートされるわけでもありません。 エミュレートされていないオブジェクトまたはメソッドを使用すると、`NotSupportedException` 例外がスローされます。 この場合は、そのメソッドに対して Fake shim デリゲートを明示的に作成し、必要な動作を返します。

- 二重用途のテストを作成するには、`SharePointEmulationScope(EmulationMode)` コンストラクターを使用して、エミュレーション スコープ オブジェクトを作成します。 `EmulationMode` 値では、SharePoint 呼び出しが実際の SharePoint サイトに対してエミュレートまたは実行されているかどうかを指定します。

- テスト クラスのテスト メソッドのほとんどまたはすべてがエミュレーションのコンテキストで実行される場合は、クラス レベルの `TestInitialize` 属性付きメソッドを使用して `SharePointEmulationScope` オブジェクトを作成し、クラス レベルのフィールドを使用してエミュレーション モードを設定できます。 これは、エミュレーション モードの変更を自動化するときに役立ちます。 その後、`TestCleanup` 属性付きメソッドを使用して、スコープ オブジェクトを破棄します。

  [このトピックの内容](#BKMK_In_this_topic)

## <a name="example"></a><a name="BKMK_Example"></a> 例
 次に示す最後の例には、上記の SharePoint エミュレーター手法が組み込まれています。

```csharp
using System;
//other namespace declarations
...
// code under test
using MySPApps;
using Microsoft.SharePoint;
// unit testing and emulators
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Microsoft.QualityTools.Testing.Emulators;
using Microsoft.SharePoint.Emulators;
// explicit Fakes shims
using Microsoft.QualityTools.Testing.Fakes;
using Microsoft.SharePoint.Fakes

namspace MySPAppTests
{
    [TestClass]
    public class BookAnAppointmentWebPartTests
    {

        // emulationScope is a class level field
        private SharePointEmulationScope emulationScope;

        // preprocessor directives determine the value of emulatorMode
        #if USE_EMULATION
            private const EmulationMode emulatorMode = EmulationMode.Enabled;
        #else
            private const EmulationMode emulatorMode = EmulationMode.Passthrough;
        #endif

        // InitializeTest sets the emulation scope at the beginning of each test method
        [TestInitialize]
        public void InitializeTest()
        {
            this.emulationScope = new SharePointEmulationScope(emulatorMode);
        }

        // CleanupTest disposes the emulation scope at the end of each test method
        [TestCleanup]
        public void Cleanup()
        {
            this.emulationScope.Dispose();
        }

        [TestMethod]
        public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
        {
            // remove the SharePointEmulationScope using statement from the method
            using( var site = new SPSite("http://localhost"))
            using (var webPart = new BookAnAppointmentWebPart())
            {
                // Arrange
                string errorMsg = string.Empty;
                DateTime date = DateTime.Now;
                SPList list = AddListToSiteHelper(site);

                // Act
                bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
                    "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
                    out errorMsg);
                list.Delete()

                // Assert
                Assert.IsTrue(success);
            }
        }

        [TestMethod]
        public void GetAppointmentsForTodayReturnsOnlyTodaysAppointments()
        {

            // remove the SharePointEmulationScope using statement from the method
            using( var site = new SPSite("http://localhost"))
            using (var webPart = new BookAnAppointmentWebPart())
            {
                // Arrange
                DateTime date = DateTime.Now;
                SPList list = AddListToSiteHelper(site);
                // insert 2 items into list
                AddItemsToListHelper(list, new string[] {"Raisa Pokrovskaya", "425-555-0163",
                    "raisa@outlook.com", "55", date.ToString("D") });
                AddItemsToListHelper(list, new string[] {"Francis Totten", "313-555-0100",
                    "francis@contoso.com", "42", date.AddDays(1).ToString("D") });

                // use Fakes shims only if emulation is enabled
                if (emulatorMode == EmulationMode.Enabled)
                {
                    var sList = new ShimSPList(list);

                    sList.GetItemsSPQuery = (query) =>
                    {
                        var shim = new ShimSPListItemCollection();
                        shim.Bind(new[] { list.Items[0] });
                        return shim.Instance;
                    }
                }

                // Act
                string result = webPart.GetAppointmentsForToday(list.Title, site.RootWeb);
                list.Delete();

                // Assert
                Assert.IsTrue(result.Contains(String.Format(
                    "Name: Raisa Pokrovskaya, Phone: 425-555-0163, Email: raisa@outlook.com," +
                    "Age: 55, Date: {0}", date.ToString("D"))));
                Assert.IsFalse(result.Contains("Name: Francis Totten"));
            }
        }

        ...// More tests

    }
}

```

## <a name="emulated-sharepoint-types"></a><a name="BKMK_Emulated_SharePoint_types"></a> エミュレートされた SharePoint の種類
 [Microsoft.SharePoint.SPField](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPField)

 [Microsoft.SharePoint.SPFieldIndex](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFieldIndex)

 [Microsoft.SharePoint.SPFieldIndexCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFieldIndexCollection)

 [Microsoft.SharePoint.SPFieldLink](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFieldLink)

 [Microsoft.SharePoint.SPFieldLinkCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFieldLinkCollection)

 [Microsoft.SharePoint.SPFieldUrlValue](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFieldUrlValue)

 [Microsoft.SharePoint.SPFile](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFile)

 [Microsoft.SharePoint.SPFileCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFileCollection)

 [Microsoft.SharePoint.SPFolder](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFolder)

 [Microsoft.SharePoint.SPFolderCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFolderCollection)

 [Microsoft.SharePoint.SPItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPItem)

 [Microsoft.SharePoint.SPItemEventDataCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPItemEventDataCollection)

 [Microsoft.SharePoint.SPItemEventProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPItemEventProperties)

 [Microsoft.SharePoint.SPList](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPList)

 [Microsoft.SharePoint.SPListCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPListCollection)

 [Microsoft.SharePoint.SPListEventProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPListEventProperties)

 [Microsoft.SharePoint.SPListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPListItem)

 [Microsoft.SharePoint.SPListItemCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPListItemCollection)

 [Microsoft.SharePoint.SPQuery](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPQuery)

 [Microsoft.SharePoint.SPRoleAssignment](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPRoleAssignment)

 [Microsoft.SharePoint.SPRoleAssignmentCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPRoleAssignmentCollection)

 [Microsoft.SharePoint.SPSecurableObject](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurableObject)

 [Microsoft.SharePoint.SPSecurity](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity)

 [Microsoft.SharePoint.SPSite](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite)

 [Microsoft.SharePoint.SPUser](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPUser)

 [Microsoft.SharePoint.SPUserCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPUserCollection)

 [Microsoft.SharePoint.SPView](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPView)

 [Microsoft.SharePoint.SPViewCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPViewCollection)

 [Microsoft.SharePoint.SPViewContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPViewContext)

 [Microsoft.SharePoint.SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb)

 [Microsoft.SharePoint.SPWebCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWebCollection)

 [このトピックの内容](#BKMK_In_this_topic)

## <a name="see-also"></a>参照
 コード化され[た UI テストを使用した sharepoint 2010 アプリケーションの](../test/testing-sharepoint-2010-applications-with-coded-ui-tests.md)[単体テストコード](../test/unit-test-your-code.md)化された UI テストでの[Web パフォーマンスとロードテスト sharepoint 2010 および2013アプリケーション](https://msdn.microsoft.com/library/20c2e469-0e4e-4296-a739-c0e8fff36e54)の[開発 sharepoint ソリューションの開発](https://msdn.microsoft.com/library/059bce0f-c301-4234-a0b4-9c14b7cdfa3e)
