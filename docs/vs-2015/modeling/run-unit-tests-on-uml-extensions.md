---
title: Run unit tests on UML extensions | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 745d74ae-e48c-4fd9-a755-4354b81b9f8a
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f634f028dafea3260a69537893513f13cc0ebe83
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74292541"
---
# <a name="run-unit-tests-on-uml-extensions"></a>単体テストを UML 拡張機能で実行する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

変更が続いてもコードを安定した状態に保つため、単体テストを記述し、定期的なビルド処理の一部として実行することをお勧めします。 詳細については、「 [Unit Test Your Code](../test/unit-test-your-code.md)」を参照してください。 Visual Studio のモデル拡張でテストを設定するには、いくつかの重要な情報が必要です。 概要:

- [Setting up a Unit Test for VSIX Extensions](#Host)

   VS IDE ホスト アダプターでテストを実行します。 各テスト メソッドにプレフィックス `[HostType("VS IDE")]`を付けます。 テストが実行されると、このホスト アダプターにより [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が起動します。

- [Accessing DTE and ModelStore](#DTE)

   通常は、テストの初期化時にモデルとその図を開いて、 `IModelStore` にアクセスする必要があります。

- [Opening a Model Diagram](#Opening)

   `EnvDTE.ProjectItem` を `IDiagramContext`との間でキャストできます。

- [Performing Changes in the UI Thread](#UiThread)

   モデル ストアに変更を加えるテストは UI スレッドで実行する必要があります。 これには `Microsoft.VSSDK.Tools.VsIdeTesting.UIThreadInvoker` を使用できます。

- [Testing commands, gestures and other MEF components](#MEF)

   MEF コンポーネントをテストするには、インポートされたプロパティを値に明示的に接続する必要があります。

  これらの点については、以降のセクションで詳しく説明します。

## <a name="requirements"></a>［要件］
 「 [要件](../modeling/extend-uml-models-and-diagrams.md#Requirements)」を参照してください。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="Host"></a> Setting up a Unit Test for VSIX Extensions
 モデリング拡張機能のメソッドは通常、既に開いている図で行います。 メソッドでは、 **IDiagramContext** や **ILinkedUndoContext**などの MEF インポートを使います。 テストを実行する前にテスト環境でこのコンテキストを設定する必要があります。

#### <a name="to-set-up-a-unit-test-that-executes-in-includevsprvsincludesvsprvs-mdmd"></a>[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で実行される単体テストを設定するには

1. UML 拡張プロジェクトおよび単体テスト プロジェクトを作成します。

    1. **A UML extension project.** 通常、これはコマンド、ジェスチャ、または検証プロジェクト テンプレートを使って作成します。 For example, see [Define a menu command on a modeling diagram](../modeling/define-a-menu-command-on-a-modeling-diagram.md).

    2. **A unit test project.** 詳細については、「 [Unit Test Your Code](../test/unit-test-your-code.md)」を参照してください。

2. UML モデリング プロジェクトを含む [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションを作成します。 このソリューションは、テストの初期段階として使用します。 Visual Studio ソリューションは、UML 拡張機能とその単体テストを記述するソリューションとは別にする必要があります。 For more information, see [Create UML modeling projects and diagrams](../modeling/create-uml-modeling-projects-and-diagrams.md).

3. **UML 拡張プロジェクトで**、.csproj ファイルをテキストとして編集し、次の行で `true`が表示されていることを確認します。

    ```
    <CopyBuildOutputToOutputDirectory>true</CopyBuildOutputToOutputDirectory>
        <CopyOutputSymbolsToOutputDirectory>true</CopyOutputSymbolsToOutputDirectory>
    ```

     .csproj ファイルをテキストとして編集するには、ソリューション エクスプローラーにあるプロジェクトのショートカット メニューで **[プロジェクトのアンロード]** をクリックします。 その後、 **[.csproj の編集]** をクリックします。 テキストを編集した後、 **[プロジェクトの再読み込み]** をクリックします。

4. UML 拡張プロジェクトで、次の行を **Properties\AssemblyInfo.cs**に追加します。 これにより、単体テストがテスト対象のメソッドにアクセスできるようになります。

    ```csharp
    [assembly:InternalsVisibleTo("MyUnitTests")] // Name of unit tests assembly.
    ```

5. **単体テスト プロジェクトで**、次のアセンブリ参照を追加します。

    - *Your UML extension project*

    - **EnvDTE.dll**

    - **Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll**

    - **Microsoft.VisualStudio.ComponentModelHost.dll**

    - **Microsoft.VisualStudio.QualityTools.UnitTestFramework.dll**

    - **Microsoft.VisualStudio.Uml.Interfaces.dll**

    - **Microsoft.VSSDK.TestHostFramework.dll**

6. 初期化メソッドを含む各テスト メソッドに、属性 `[HostType("VS IDE")]` をプレフィックスとして含めます。

     これにより、テストが Visual Studio の実験的なインスタンスで実行されることが保証されます。

## <a name="DTE"></a> Accessing DTE and ModelStore
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]でモデリング プロジェクトを開くメソッドを記述します。 通常は、各テストの実行で 1 度だけソリューションを開きます。 メソッドを 1 度だけ実行するには、メソッドに `[AssemblyInitialize]` 属性をプレフィックスとして付けます。 また、各テスト メソッドで [HostType("VS IDE")] 属性も必要です。  (例:

```csharp
using EnvDTE;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Microsoft.VSSDK.Tools.VsIdeTesting;

namespace UnitTests
{
  [TestClass]
  public static class TestSetup
  {

    // Location of a VS Solution that defines an initial state for your tests:
    private const string testSolutionFilePath = @"C:\MyTestFolder\TestModelSln\TestModel.sln";
    // Name of a modeling project within the test solution:
    private const string testModelingProjectName = "MyTestModel";

    // Make Solution and IModelStore available to test methods:
    public static Solution ModelSolution = null;
    public static IModelingProject ModelingProject = null;
    public static IModelStore ModelStore = null;

    // This method will be performed once to initialize tests for this assembly:
    [AssemblyInitialize]
    [HostType("VS IDE")]
    public static void OpenTestModelingProject(TestContext testContext)
    {
      // To make sure that we always start the tests in the same state,
      // copy the test solution from a read-only directory:
      // TODO: copy test solution folder.

      // Open a solution that is the initial state for your tests:
      ModelSolution = VsIdeTestHostContext.Dte.Solution;
      ModelSolution.Open(testSolutionFilePath);

      // Find the ModelingProject and IModelStore:
      foreach (Project project in ModelSolution.Projects)
      {
        // https://msdn.microsoft.com/library/ee791691.aspx
        ModelingProject = project as IModelingProject;
        if (ModelingProject != null)
        {
          // This is a modeling project.
          ModelStore = ModelingProject.Store;
          break;
        }
        // else this is another kind of project.
      }

      Assert.IsNotNull(ModelSolution, "VS solution not found");
      Assert.IsNotNull(ModelStore, "Modeling store not found");
    }
    [AssemblyCleanup]
    public static void RemoveTestSolution ()
    {
      // TODO: Remove copied test solution directory.
    }
  }
}

```

 If an instance of <xref:EnvDTE.Project?displayProperty=fullName> represents a modeling project, then you can cast it to and from [IModelingProject](/previous-versions/ee789474(v=vs.140)).

## <a name="Opening"></a> Opening a Model Diagram
 各テストまたはテストのクラスでは、開いている図で作業することがよくあります。 次の例では、このテスト クラスの他のメソッドよりも先にこのメソッドを実行する `[ClassInitialize]` 属性を使用します。 ここでも、各テスト メソッドには属性 [HostType("VS IDE")] も必要です。

```csharp
//
private IDiagram diagram;
// This class contains unit tests:
[TestClass]
public class MyTestClass
{
  // Map filenames to open diagram files:
  private static Dictionary<string, IDiagram> diagrams = new Dictionary<string, IDiagram>();

  // This method will be called once for this test class:
  [ClassInitialize]
  [HostType("VS IDE")]
  public static void TestClassInitialize(TestContext testContext)
  {
    // Open all the diagrams in the model:
    foreach (ProjectItem item in (TestSetup.ModelingProject as Project).ProjectItems)
    {
      // Get the filename of the principal file (not the .layout subsidiary):
      string fileName = item.FileNames[0];
      // If this is a model diagram file, it can be cast to IDiagramContext:
      IDiagramContext modelingItem = item as IDiagramContext;
      if (modelingItem != null)
      {
        IDiagram diagram = modelingItem.CurrentDiagram;
        if (diagram == null)
        {
          // Diagram is closed. Open it:
          item.Open().Activate();
          diagram = modelingItem.CurrentDiagram;
        }
        diagrams[fileName] = diagram;
      }
      // else item is not a model diagram.
    }
    Assert.IsTrue(diagrams.Count>0, "UML diagram not found");
  }
// Insert test methods here ...
}

```

## <a name="UiThread"></a> Perform Model Changes in the UI Thread
 テストまたはテストのメソッドがモデル ストアを変更する場合は、それらをユーザー インターフェイス スレッドで実行する必要があります。 こうしない場合、 `AccessViolationException`が表示される可能性があります。 起動する呼び出しの中の、テスト メソッドのコードを囲みます。

```
using System.Windows.Forms;
using Microsoft.VSSDK.Tools.VsIdeTesting;
 ...
    [TestMethod]
    [HostType("VS IDE")]
    public void MyTest1()
    {
      // Store operations must run in the UI thread:
      UIThreadInvoker.Invoke((System.Action)delegate()
      {
        SetupTestState(TestSetup.ModelStore, diagram);
        ExecuteMethodUnderTest(TestSetup.ModelStore, diagram);
      });
    }
```

## <a name="MEF"></a> Testing command, gesture and other MEF components
 MEF コンポーネントは、 `[Import]` 属性を持つプロパティ宣言を使用します。プロパティの値は、そのホストにより設定されます。 通常、そのようなプロパティには IDiagramContext、SVsServiceProvider、および ILinkedUndoContext が含まれます。 これらのいずれかのプロパティを使用するメソッドをテストする場合、テストでメソッドを実行する前にその値を設定する必要があります。 たとえば、次のコードのようなコマンド拡張機能を記述したとします。

```

  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension]
  class MyCommand : ICommandExtension
  {
    [Import] IDiagramContext context { get; set; }
    [Import]
Microsoft.VisualStudio.Shell.SVsServiceProvider
serviceProvider {get;set;}
    [Import] ILinkedUndoContext linkedUndoContext { get; set; }
    public void Execute(IMenuCommand command)
    {
      DoCommand();
    }
    private void DoCommand()
    {
      IDiagram diagram = context.CurrentDiagram;
      using (ILinkedUndoTransaction t = linkedUndoContext.BeginTransaction("go"))
      { ... }}}

```

 インポートされたプロパティを次のように設定できます。

```

using System.ComponentModel.Composition;
using Microsoft.VisualStudio.ComponentModelHost;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Microsoft.VSSDK.Tools.VsIdeTesting;
...
    [TestMethod]
    [HostType("VS IDE")]
    public void Test1()
    {
      // Create an instance of the class under test:
      MyCommand myCommand = new MyCommand();
      // Get the components service:
      IComponentModel components = VsIdeTestHostContext.ServiceProvider
        .GetService(typeof(SComponentModel)) as IComponentModel;
      // Set the imported properties of the instance under test:
      // Extension requires "using System.ComponentModel.Composition;" :
      components.DefaultCompositionService.SatisfyImportsOnce(myCommand);
      // Call method(s) under test:
      UIThreadInvoker.Invoke((System.Action)delegate()
      {
        myCommand.DoCommand();
      });
...}
```

 インポートされたプロパティをパラメーターとするメソッドをテストする場合、テスト クラスにプロパティをインポートして、テスト インスタンスに `SatisfyImportsOnce` を適用できます。 (例:

```

using System.ComponentModel.Composition;
...
  [TestClass]
  public class MyTestClass
  {
    [Import] ILinkedUndoContext linkedUndoContext { get; set; }

    // Called before each test method:
    [TestInitialize, HostType("VS IDE")]
    public void TestInitializer()
    {
      IComponentModel components = VsIdeTestHostContext.ServiceProvider
            .GetService(typeof(SComponentModel)) as IComponentModel;
      // Extension requires "using System.ComponentModel.Composition;" :
      components.DefaultCompositionService.SatisfyImportsOnce(this);
    }
    [TestMethod, HostType("VS IDE")]
    public void Test2()
    {
     UIThreadInvoker.Invoke((System.Action)delegate()
      {
      // Pass context items to class under test:
      Class1 item1 = new Class1(this.linkedUndoContext);
      item1.Method1(); // Can use linkedUndoContext
     });
   }
}

```

 この例では、便宜上、各テスト メソッドの 2 つの属性が 1 行に記述されています。

## <a name="access-from-tests-to-private-methods-and-variables"></a>テストからプライベート メソッドおよび変数へのアクセス
 場合によっては、テストのメソッドを実行する前後に、プライベートなメソッドをテストする、またはプライベートなフィールドの状態を確認する必要が生じます。 この場合、テストは、テストされるクラスとは異なるアセンブリにあるため困難が生じます。 このような場合には、次のようないくつかの手法を検討できます。

 Test only by using public and internal items Write your tests so that they use only public (or internal) classes and members. これが最善の方法です。 テストのアセンブリの内部実装をリファクタリングしても、テストは引き続き機能します。 変更の前後で同じテストを適用することにより、変更がアセンブリの動作に影響していないことを確認できます。

 これを可能にするには、場合によってはコードを再構築する必要があります。 たとえば、一部のメソッドを別のクラスに分割することが必要になる場合があります。

 この方法を本格的に検討すると、多くの場合、コードの確認と変更がより簡単になり、変更が必要なときにはエラーが少なくなることに気づきます。

 テスト対象のプロジェクトの **Properties\AssemblyInfo.cs** に属性を追加することで、テスト アセンブリからの内部項目へのアクセスを許可することができます。

```csharp
[assembly:InternalsVisibleTo("MyUnitTests")] // Name of unit tests assembly.
```

 Define a test interface Define an interface that includes both the public members of a class to be tested, and additional properties and methods for the private members that you want the tests to be able to use. テスト対象のプロジェクトにこのインターフェイスを追加します。 (例:

```csharp
internal interface MyClassTestInterface {
  void PublicMethod1();
  string PublicProperty1 { get; }
  string privateField1_Accessor { get; }
  int privateMethod1_Accessor (string p1);
 }
```

 テスト対象のクラスにメソッドを追加して、アクセサー メソッドを明示的に実装します。 これらの追加のメソッドは、個別のファイルの部分クラス定義に記述して、メイン クラスとは切り離しておきます。 (例:

```csharp
partial public class MyClass
{
  string MyClassTestInterface.privateField1_Accessor
  { get { return privateField1; } }
  int MyClassTestInterface.privateMethod1_Accessor (string p1)
  { return privateMethod1(p1); }
}

```

 テスト対象のアセンブリにこの属性を追加して、テスト アセンブリがテスト インターフェイスを使用できるようにします。

```csharp
[assembly:InternalsVisibleTo("MyUnitTests")] // Name of unit tests assembly.
```

 単体テスト メソッドで、テスト インターフェイスを使います。 (例:

```csharp
MyClassTestInterface testInstance = new MyClass();
testInstance.PublicMethod1();
Assert.AreEqual("hello", testInstance.privateField1_Accessor);
```

 Define accessors by using reflection This is the way that we recommend least. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の古いバージョンでは、それぞれのプライベート メソッドにアクセサー メソッドを自動的に作成するユーティリティが用意されていました。 これは便利ですが、経験上、テストするアプリケーションの内部構造に非常に強く結びついた単体テストになる傾向があります。 結果として、要件やアーキテクチャに変更があると、その実装に応じてテストも変更する必要があるため、余分の作業が生じます。 また、実装の設計に関する間違った前提もテストに組み込まれているため、テストではエラーを発見できません。

## <a name="see-also"></a>参照
 [Anatomy of a Unit Test](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144) [Define a menu command on a modeling diagram](../modeling/define-a-menu-command-on-a-modeling-diagram.md)
