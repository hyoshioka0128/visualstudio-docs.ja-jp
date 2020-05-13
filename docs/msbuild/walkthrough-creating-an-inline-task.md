---
title: 'チュートリアル: インライン タスクの作成 | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tutorial
- MSBuild, tasks
ms.assetid: 438194cb-668c-41a9-a7e2-c118d14c1ea7
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70ce19a6dcd9c61b0e14d0d88c52072f59f87fb9
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77631160"
---
# <a name="walkthrough-create-an-inline-task"></a>チュートリアル: インライン タスクの作成

MSBuild タスクは通常、<xref:Microsoft.Build.Framework.ITask> インターフェイスを実装するクラスをコンパイルして作成します。 .NET Framework Version 4 以降では、プロジェクト ファイルでタスクをインラインで作成できます。 個別のアセンブリを作成してタスクをホストする必要はありません。 詳細については、「[インライン タスク](../msbuild/msbuild-inline-tasks.md)」を参照してください。

 このチュートリアルでは、次のインライン タスクを作成し、実行する方法について説明します。

- 入力パラメーターも出力パラメーターも持たないタスク。

- 1 つの入力パラメーターを持つが出力パラメーターを持たないタスク。

- 2 つの入力パラメーターと、MSBuild プロパティを返す 1 つの出力パラメーターを持つタスク。

- 2 つの入力パラメーターと、MSBuild 項目を返す 1 つの出力パラメーターを持つタスク。

タスクを作成して実行するには、Visual Studio と **Visual Studio コマンド プロンプト ウィンドウ**を使用して次の操作を実行します。

1. Visual Studio を使用して MSBuild プロジェクト ファイルを作成します。

2. Visual Studio でプロジェクト ファイルを変更してインライン タスクを作成します。

3. **コマンド プロンプト ウィンドウ**を使用してプロジェクトをビルドし、結果を確認します。

## <a name="create-and-modify-an-msbuild-project"></a>MSBuild プロジェクトの作成と変更を行う

 Visual Studio プロジェクト システムは MSBuild に基づいています。 したがって、ビルド プロジェクト ファイルは Visual Studio を使用して作成できます。 このセクションでは、Visual C# プロジェクト ファイルを作成します (代わりに、Visual Basic プロジェクト ファイルを作成することもできます。 このチュートリアルのコンテキストでは、2 つのプロジェクト ファイルにはわずかな違いしかありません)。

#### <a name="to-create-and-modify-a-project-file"></a>プロジェクト ファイルを作成および変更するには

1. Visual Studio で、C# **Windows フォーム アプリケーション** テンプレートを使用して新しいプロジェクトを作成します。 **[名前]** ボックスに「 `InlineTasks`」と入力します。 ソリューションの**場所**を入力します (*D:\\* など)。 **[ソリューションのディレクトリを作成]** がオンになっていることと、 **[ソース管理に追加]** がオフになっていること、さらに **[ソリューション名]** が **InlineTasks** になっていることを確認します。

3. **[OK]** をクリックして、プロジェクト ファイルを作成します。

3. **ソリューション エクスプローラー**で、 **[InlineTasks]** プロジェクト ノードを右クリックし、 **[プロジェクトのアンロード]** をクリックします。

4. プロジェクト ノードを再度右クリックし、 **[InlineTasks.csproj の編集]** をクリックします。

     コード エディターにプロジェクト ファイルが表示されます。

## <a name="add-a-basic-hello-task"></a>基本的な Hello タスクを追加する

 ここでは、"Hello, world!" というメッセージを表示する基本的なタスクをプロジェクト ファイルに追加します。 また、タスクを呼び出す既定の TestBuild ターゲットを追加します。

#### <a name="to-add-a-basic-hello-task"></a>基本的な Hello タスクを追加するには

1. ルートの `Project` ノードで、`DefaultTargets` 属性を `TestBuild` に変更します。その結果、`Project` ノードは次の例のようになります。

   ```xml
   <Project ToolsVersion="4.0" DefaultTargets="TestBuild" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
   ```

2. プロジェクト ファイルの `</Project>` タグの直前に、次のインライン タスクとターゲットを追加します。

   ```xml
   <UsingTask TaskName="Hello" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup />
     <Task>
       <Code Type="Fragment" Language="cs">
         Log.LogMessage(MessageImportance.High, "Hello, world!");
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <Hello />
   </Target>
   ```

3. プロジェクト ファイルを保存します。

   このコードによって、パラメーター、参照、または `Using` ディレクティブがない Hello という名前のインライン タスクが作成されます。 この Hello タスクには、既定のログ デバイス (通常はコンソール ウィンドウ) に Hello メッセージを表示する 1 行のコードのみが含まれています。

### <a name="run-the-hello-task"></a>Hello タスクを実行する

 **コマンド プロンプト ウィンドウ**を使用して MSBuild を実行し、Hello タスクを構築して、そのタスクを呼び出す TestBuild ターゲットを処理します。

##### <a name="to-run-the-hello-task"></a>Hello タスクを実行するには

1. **[スタート]** 、 **[すべてのプログラム]** の順にクリックし、 **[Visual Studio Tools]** フォルダーを見つけて **[Visual Studio コマンド プロンプト]** をクリックします。

2. **コマンド プロンプト ウィンドウ**で、プロジェクト ファイルが格納されているフォルダー (この場合は *D:\InlineTasks\InlineTasks\\* ) を見つけます。

3. コマンド スイッチを指定せずに「**msbuild**」と入力し、**Enter** キーを押します。 既定では、これによって *InlineTasks.csproj* ファイルがビルドされ、Hello タスクを呼び出す既定のターゲット TestBuild が処理されます。

4. **コマンド プロンプト ウィンドウ**で出力を確認します。 次の行が表示されます。

    `Hello, world!`

   > [!NOTE]
   > Hello メッセージが表示されない場合は、プロジェクト ファイルをもう一度保存してから Hello タスクを実行してみてください。

   コード エディターと**コマンド プロンプト ウィンドウ**を交互に使用すると、プロジェクト ファイルを変更してすばやく結果を確認できます。

## <a name="define-the-echo-task"></a>Echo タスクを定義する

 文字列パラメーターを受け取って既定のログ デバイスに文字列を表示するインライン タスクを作成します。

#### <a name="to-define-the-echo-task"></a>Echo タスクを定義するには

1. コード エディターで、次のコードを使用して、Hello タスクと TestBuild ターゲットを置き換えます。

   ```xml
   <UsingTask TaskName="Echo" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup>
       <Text Required="true" />
     </ParameterGroup>
     <Task>
       <Code Type="Fragment" Language="cs">
         Log.LogMessage(MessageImportance.High, Text);
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <Echo Text="Greetings!" />
   </Target>
   ```

2. **コマンド プロンプト ウィンドウ**で、コマンド スイッチを指定せずに「**msbuild**」と入力し、**Enter** キーを押します。 既定では、これによって Echo タスクを呼び出す既定のターゲット TestBuild が処理されます。

3. **コマンド プロンプト ウィンドウ**で出力を確認します。 次の行が表示されます。

    `Greetings!`

   このコードによって、必須の入力パラメーター Text を 1 つだけ持つ Echo という名前のインライン タスクが定義されます。 既定では、パラメーターの型は System.String です。 Text パラメーターの値は、TestBuild ターゲットによって Echo タスクが呼び出されたときに設定されます。

## <a name="define-the-adder-task"></a>Adder タスクを定義する

 2 つの整数パラメーターを追加して、その合計を MSBuild プロパティとして生成するインライン タスクを作成します。

#### <a name="to-define-the-adder-task"></a>Adder タスクを定義するには

1. コード エディターで、次のコードを使用して、Echo タスクと TestBuild ターゲットを置き換えます。

   ```xml
   <UsingTask TaskName="Adder" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup>
       <A ParameterType="System.Int32" Required="true" />
       <B ParameterType="System.Int32" Required="true" />
       <C ParameterType="System.Int32" Output="true" />
     </ParameterGroup>
     <Task>
       <Code Type="Fragment" Language="cs">
         C = A + B;
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <Adder A="4" B="5">
       <Output PropertyName="Sum" TaskParameter="C" />
     </Adder>
     <Message Text="The sum is $(Sum)" Importance="High" />
   </Target>
   ```

2. **コマンド プロンプト ウィンドウ**で、コマンド スイッチを指定せずに「**msbuild**」と入力し、**Enter** キーを押します。 既定では、これによって Echo タスクを呼び出す既定のターゲット TestBuild が処理されます。

3. **コマンド プロンプト ウィンドウ**で出力を確認します。 次の行が表示されます。

    `The sum is 9`

   このコードによって、Adder という名前のインライン タスクが定義されます。このタスクには、2 つの必須の整数入力パラメーター A と B、および 1 つの整数出力パラメーター C があります。Adder タスクによって 2 つの入力パラメーターが追加され、出力パラメーターで合計が返されます。 合計は MSBuild プロパティ `Sum` として生成されます。 入力パラメーターの値は、TestBuild ターゲットによって Adder タスクが呼び出されたときに設定されます。

## <a name="define-the-regx-task"></a>RegX タスクを定義する

 項目グループおよび正規表現を受け取って、正規表現と一致するファイルの内容を含むすべての項目の一覧を返すインライン タスクを作成します。

#### <a name="to-define-the-regx-task"></a>RegX タスクを定義するには

1. コード エディターで、次のコードを使用して、Adder タスクと TestBuild ターゲットを置き換えます。

   ```xml
   <UsingTask TaskName="RegX" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup>
       <Expression Required="true" />
       <Files ParameterType="Microsoft.Build.Framework.ITaskItem[]" Required="true" />
       <Result ParameterType="Microsoft.Build.Framework.ITaskItem[]" Output="true" />
     </ParameterGroup>
     <Task>
       <Using Namespace="System.Text.RegularExpressions"/>
       <Code Type="Fragment" Language="cs">
   <![CDATA[
         if (Files.Length > 0)
         {
           Result = new TaskItem[Files.Length];
           for (int i = 0; i < Files.Length; i++)
           {
             ITaskItem item = Files[i];
             string path = item.GetMetadata("FullPath");
             using(StreamReader rdr = File.OpenText(path))
             {
               if (Regex.Match(rdr.ReadToEnd(), Expression).Success)
               {
                 Result[i] = new TaskItem(item.ItemSpec);
               }
             }
           }
         }
   ]]>
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <RegX Expression="public|protected" Files="@(Compile)">
       <Output ItemName="MatchedFiles" TaskParameter="Result" />
     </RegX>
     <Message Text="Input files: @(Compile)" Importance="High" />
     <Message Text="Matched files: @(MatchedFiles)" Importance="High" />
   </Target>
   ```

2. **コマンド プロンプト ウィンドウ**で、コマンド スイッチを指定せずに「**msbuild**」と入力し、**Enter** キーを押します。 既定では、これによって RegX タスクを呼び出す既定のターゲット TestBuild が処理されます。

3. **コマンド プロンプト ウィンドウ**で出力を確認します。 次の行が表示されます。

   ```
   Input files: Form1.cs;Form1.Designer.cs;Program.cs;Properties\AssemblyInfo.cs;Properties\Resources.Designer.cs;Properties\Settings.Designer.cs
   ```

   ```
   Matched files: Form1.cs;Form1.Designer.cs;Properties\Settings.Designer.cs
   ```

   このコードによって、次の 3 つのパラメーターを持つ RegX という名前のインライン タスクが定義されます。

- `Expression`: 照合する正規表現を示す値を持つ必須の文字列入力パラメーター。 この例では、正規表現は "public" または "protected" という語と一致します。

- `Files`: 一致する語を検索するファイルの一覧を示す値を持つ必須の項目一覧入力パラメーター。 この例では、`Files` はプロジェクト ソース ファイルを一覧表示する `Compile` 項目に設定されます。

- `Result`: 正規表現と一致する内容を含むファイルの一覧を示す値を持つ出力パラメーター。

  入力パラメーターの値は、TestBuild ターゲットによって RegX タスクが呼び出されたときに設定されます。 RegX タスクによってすべてのファイルが読み取られ、正規表現と一致するファイルの一覧が返されます。 この一覧は `Result` 出力パラメーターとして返され、MSBuild 項目 `MatchedFiles` として生成されます。

### <a name="handle-reserved-characters"></a>予約文字を使用する

 MSBuild パーサーによってインライン タスクが XML として処理されます。 XML で意味が予約されている文字 ("\<" や ">" など) は、.NET ソース コードではなく XML として検出されて処理されます。 コード式に予約文字を含めるには (`Files.Length > 0` など)、次のように `Code` 要素を記述して、その内容が CDATA 式に含まれるようにします。

 ```xml
<Code Type="Fragment" Language="cs">
  <![CDATA[

  // Your code goes here.

  ]]>
</Code>
```

## <a name="see-also"></a>関連項目

- [インライン タスク](../msbuild/msbuild-inline-tasks.md)
- [タスク](../msbuild/msbuild-tasks.md)
- [ターゲット](../msbuild/msbuild-targets.md)
