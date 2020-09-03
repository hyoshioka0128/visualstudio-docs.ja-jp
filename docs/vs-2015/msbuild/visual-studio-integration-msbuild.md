---
title: Visual Studio の統合 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, reference resolution
- MSBuild, well-known target names
- MSBuild, hosting
- MSBuild, editing project files
- MSBuild, Visual Studio integration
- MSBuild, IntelliSense
- MSBuild, output groups
- MSBuild, in-process compilers
- MSBuild, design-time target execution
ms.assetid: 06cd6d7f-8dc1-4e49-8a72-cc9e331d7bca
caps.latest.revision: 26
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c90019aa24047524005ba70aa4f1aec75f89c71d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67825423"
---
# <a name="visual-studio-integration-msbuild"></a>Visual Studio の統合 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio は、マネージド プロジェクトの読み込みとビルドを行う [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] をホストしています。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] はプロジェクトに対応しているため、そのプロジェクトが他のツールで作成されていたり、ビルド処理がカスタマイズされていたりしても、 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 形式のほとんどすべてのプロジェクトを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で問題なく使用できます。  
  
 このトピックでは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]に読み込んでビルドするプロジェクトおよび .targets ファイルをカスタマイズする際に考慮が必要な、 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] による [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]のホストに固有な事項について説明します。 これらの事項は、IntelliSense やデバッグなどの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の機能をカスタム プロジェクトに対して有効にするうえで役立ちます。  
  
 C++ プロジェクトの詳細については、「 [Project Files](/cpp/build/reference/project-files)」を参照してください。  
  
## <a name="project-file-name-extensions"></a>プロジェクト ファイルの拡張子  
 MSBuild.exe は、.*proj のパターンに一致するすべてのプロジェクト ファイル拡張子を認識します。 ただし、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、プロジェクトを読み込む言語固有のプロジェクト システムを決定する、これらのプロジェクト ファイル拡張子のサブセットしか認識しません。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] には、言語に依存しない [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] ベースのプロジェクト システムが備わっていないためです。  
  
 たとえば、 [!INCLUDE[csprcs](../includes/csprcs-md.md)] のプロジェクト システムは .csproj ファイルを読み込みますが、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では .xxproj ファイルを読み込むことができません。 任意の言語のソース ファイル用のプロジェクト ファイルには、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] に読み込む [!INCLUDE[csprcs](../includes/csprcs-md.md)] または [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]プロジェクト ファイルと同じ拡張子を使用する必要があります。  
  
## <a name="well-known-target-names"></a>既知のターゲット名  
 **の** [ビルド] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] をクリックすると、プロジェクトの既定のターゲットが実行されます。 このターゲットも `Build`という名前になっていることがよくあります。 **[リビルド]** または **[消去]** を選択すると、プロジェクト内の同じ名前のターゲットが実行されます。 **[発行]** をクリックすると、プロジェクト内の `PublishOnly` という名前のターゲットが実行されます。  
  
## <a name="configurations-and-platforms"></a>構成とプラットフォーム  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトの構成は、 `PropertyGroup` 属性を含む `Condition` 要素内にグループ化されているプロパティによって表されます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、表示するプロジェクト構成およびプラットフォームのリストを作成するために、これらの条件を確認します。 このリストを正常に抽出するには、条件の形式が次のようになっている必要があります。  
  
```  
Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' "  
Condition=" '$(Configuration)' == 'Release' "   
Condition=" '$(Something)|$(Configuration)|$(SomethingElse)' == 'xxx|Debug|yyy' "  
```  
  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] はこの目的のために、 `PropertyGroup`、 `ItemGroup`、 `Import`、プロパティ、および項目要素の条件を確認します。  
  
## <a name="additional-build-actions"></a>その他のビルド アクション  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]では、[[ファイルのプロパティ](https://msdn.microsoft.com/013c4aed-08d6-4dce-a124-ca807ca08959)] ウィンドウの [**ビルドアクション**] プロパティを使用して、プロジェクト内のファイルの項目の種類名を変更できます。 `Compile`、 `EmbeddedResource`、 `Content`、および `None` の各項目の種類名は、プロジェクト内に既に存在する他の項目の種類名と共に、常にこのメニューに表示されます。 このメニューにカスタムの項目の種類名すべてが常に表示されるようにするには、 `AvailableItemName`という項目の種類に名前を追加します。 たとえば、プロジェクト ファイルに次の内容を追加すると、このファイルをインポートするすべてのプロジェクトの当該メニューに、カスタム型 `JScript` が追加されます。  
  
```  
<ItemGroup>  
    <AvailableItemName Include="JScript"/>  
</ItemGroup>  
```  
  
> [!NOTE]
> 一部の項目の種類名は [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 特有のものですが、このドロップダウン リストには表示されません。  
  
## <a name="in-process-compilers"></a>インプロセス コンパイラ  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、可能な限り [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] コンパイラのインプロセス バージョンを使用して、パフォーマンスの向上を計ります  (には適用されません [!INCLUDE[csprcs](../includes/csprcs-md.md)] )。これが正常に機能するには、次の条件を満たす必要があります。  
  
- `Vbc` プロジェクトの場合、プロジェクトのターゲットに [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] という名前のタスクが存在すること。  
  
- このタスクの `UseHostCompilerIfAvailable` パラメーターが true に設定されていること。  
  
## <a name="design-time-intellisense"></a>デザイン時における IntelliSense のサポート  
 ビルドによって出力アセンブリが生成される前に、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で IntelliSense がサポートされるようにするには、次の条件が満たされている必要があります。  
  
- `Compile`という名前のターゲットが存在すること。  
  
- `Compile` ターゲットまたはその依存関係のいずれかによって、 `Csc` や `Vbc`などの、プロジェクトのコンパイラ タスクが呼び出されること。  
  
- `Compile` ターゲットまたはその依存関係のいずれかによって、IntelliSense に必要なすべてのパラメーター (特にすべての参照) をコンパイラが受け取ること。  
  
- 「インプロセス コンパイラ」のセクションに示した条件が満たされていること。  
  
## <a name="building-solutions"></a>ソリューションの構築  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]内では、ソリューション ファイルおよびプロジェクトのビルドの順序は [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 自体によって制御されます。 コマンド ラインで msbuild.exe を使用してソリューションをビルドする場合、 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] はソリューション ファイルを解析し、プロジェクトのビルドの順序を指定します。 どちらの場合も、プロジェクトは依存関係の順序で個別にビルドされ、プロジェクト間参照は走査されません。 逆に、msbuild.exe を使用して個々のプロジェクトをビルドする場合は、プロジェクト間参照が走査されます。  
  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の内部でビルドする場合は、 `$(BuildingInsideVisualStudio)` プロパティを `true`に設定します。 これをプロジェクトまたは .targets ファイル内で使用することにより、ビルドの動作を変更できます。  
  
## <a name="displaying-properties-and-items"></a>プロパティと項目の表示  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、特定のプロパティ名とプロパティ値を認識します。 たとえば、プロジェクト内で次のプロパティを使用すると、 **プロジェクト デザイナー** の **[アプリケーションの種類]** ボックスに **Windows アプリケーション**が表示されます。  
  
```  
<OutputType>WinExe</OutputType>  
```  
  
 プロパティ値は、 **プロジェクト デザイナー** で編集してプロジェクト ファイルに保存できます。 このようなプロパティを編集する際に無効な値を指定した場合、プロジェクトを読み込むと [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] によって警告メッセージが表示され、無効な値が既定値に置き換えられます。  
  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は一部のプロパティの既定値を認識しています。 これらのプロパティは、既定値以外の値を持つ場合だけプロジェクト ファイルに保存されます。  
  
 恣意的な名前のプロパティは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]では表示されません。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で恣意的な名前のプロパティを変更するには、XML エディターでプロジェクト ファイルを開き、手動で編集する必要があります。 詳細については、このトピックで後述する「 [Editing Project Files in Visual Studio](#BKMK_EditingProjects) 」を参照してください。  
  
 任意の項目の種類名を使用してプロジェクト内で定義された項目は、既定では、ソリューション エクスプローラーのプロジェクト ノードの下に表示されます。 項目が表示されないようにするには、 `Visible` メタデータを `false`に設定します。 たとえば、次の項目はビルド処理に参加しますが、ソリューション エクスプローラーには表示されません。  
  
```  
<ItemGroup>  
    <IntermediateFile Include="cache.temp">  
        <Visible>false</Visible>  
    </IntermediateFile>  
</ItemGroup>  
```  
  
 プロジェクトにインポートしたファイルで宣言されている項目は、既定では表示されません。 ビルド処理中に作成された項目がソリューション エクスプローラーに表示されることは決してありません。  
  
## <a name="conditions-on-items-and-properties"></a>項目とプロパティの条件  
 ビルド時には、すべての条件が完全に遵守されます。  
  
 表示するプロパティ値を決定する際、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が、構成に依存すると見なすプロパティは、構成に依存しないと見なすプロパティとは評価方法が異なります。 構成に依存すると見なされるプロパティの場合、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は `Configuration` プロパティと `Platform` プロパティを適切に設定し、 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] に対しプロジェクトを再評価するように指示します。 構成に依存しないと見なされるプロパティの場合、条件の評価方法は不確定です。  
  
 項目の条件式は、その項目をソリューション エクスプローラーに表示するかどうかを決めるという目的では常に無視されます。  
  
## <a name="debugging"></a>デバッグ  
 出力アセンブリを見つけて起動し、デバッガーをアタッチするには、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、 `OutputPath`、および `AssemblyName`の各プロパティが `OutputType` で正しく定義されている必要があります。 ビルド処理においてコンパイラが .pdb ファイルを生成しない場合、デバッガーはアタッチされません。  
  
## <a name="design-time-target-execution"></a>デザイン時におけるターゲットの実行  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、プロジェクトを読み込む際に、特定の名前を持つターゲットを実行しようとします。 このようなターゲットとしては、`Compile`、`ResolveAssemblyReferences`、`ResolveCOMReferences`、`GetFrameworkPaths`、`CopyRunEnvironmentFiles` などがあります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] はこれらのターゲットを実行することにより、IntelliSense が使用できるようにコンパイラを初期化し、デバッガーを初期化し、さらにソリューション エクスプローラーに表示される参照を解決します。 これらのターゲットが存在しない場合、プロジェクトは正常に読み込まれてビルドされますが、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のデザイン時環境は完全には機能しません。  
  
## <a name="editing-project-files-in-visual-studio"></a><a name="BKMK_EditingProjects"></a> Editing Project Files in Visual Studio  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトを直接編集するには、Visual Studio の XML エディターでプロジェクト ファイルを開きます。  
  
#### <a name="to-unload-and-edit-a-project-file-in-visual-studio"></a>Visual Studio でプロジェクト ファイルをアンロードして編集するには  
  
1. **ソリューション エクスプローラー**で、プロジェクトのショートカット メニューを開き、 **[プロジェクトのアンロード]** をクリックします。  
  
     プロジェクトに **(利用不可)** のマークが付きます。  
  
2. **ソリューションエクスプローラー**で、使用できないプロジェクトのショートカットメニューを開き、[**編集 \<Project File> **] を選択します。  
  
     Visual Studio XML エディターでプロジェクト ファイルが開きます。  
  
3. プロジェクト ファイルを編集し、保存して閉じます。  
  
4. **ソリューション エクスプローラー**で、利用不可のプロジェクトのショートカット メニューを開き、 **[プロジェクトの再読み込み]** をクリックします。  
  
## <a name="intellisense-and-validation"></a>IntelliSense と検証  
 XML エディターを使用してプロジェクト ファイルを編集する際、 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] のスキーマ ファイルによって IntelliSense と検証が実行されます。 これらはスキーマキャッシュにインストールされ、\Xml\schemas\1033\msbuild にあるにあります。 *\<Visual Studio installation directory>*  
  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] の中心となる型は Microsoft.Build.Core.xsd で定義され、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が使用する共通の型は Microsoft.Build.CommonTypes.xsd で定義されます。 カスタムの項目の種類名、プロパティ、およびタスク用に IntelliSense と検証を使用できるようにスキーマをカスタマイズするには、Microsoft.Build.xsd を編集するか、CommonTypes スキーマまたは Core スキーマを含む独自のスキーマを作成します。 独自のスキーマを作成する場合は、 **[プロパティ]** ウィンドウを使用してこのスキーマを見つけるように XML エディターに指示する必要があります。  
  
## <a name="editing-loaded-project-files"></a>読み込んだプロジェクト ファイルの編集  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、プロジェクト ファイルの内容やプロジェクト ファイルによってインポートしたファイルの内容をキャッシュします。 読み込んだプロジェクト ファイルを編集すると、プロジェクトを再読み込みして変更を有効にするように求めるメッセージが [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] によって自動的に表示されます。 ただし、読み込んだプロジェクトによってインポートされたファイルを編集した場合は、再読み込みを求めるメッセージが表示されないため、手動でプロジェクトのアンロードと再読み込みを行い、変更内容を有効にする必要があります。  
  
## <a name="output-groups"></a>出力グループ  
 Microsoft.Common.targets で定義したいくつかのターゲットの名前は、最後の部分が `OutputGroups` または `OutputGroupDependencies`となります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] はこれらのターゲットを呼び出して、特定のプロジェクト出力のリストを取得します。 たとえば、`SatelliteDllsProjectOutputGroup` ターゲットを呼び出すと、ビルドが作成したすべてのサテライト アセンブリのリストが作成されます。 これらの出力グループは、発行、配置、およびプロジェクト間参照などの機能によって使用されます。 これらのターゲットを定義していなくても、プロジェクトは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]に読み込まれてビルドされますが、一部の機能が正常に動作しない場合があります。  
  
## <a name="reference-resolution"></a>参照の解決  
 参照の解決とは、プロジェクト ファイルに格納されている参照項目を使用して、実際のアセンブリを検索する処理をいいます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、 **[プロパティ]** ウィンドウに参照ごとに詳細なプロパティを表示するために、参照の解決を実行する必要があります。 次の一覧では、3 種類の参照とその解決方法について説明します。  
  
- アセンブリ参照  
  
  プロジェクト システムは、 `ResolveAssemblyReferences`という既知の名前を持つターゲットを呼び出します。 このターゲットは、 `ReferencePath`という項目の種類名を持つ項目を生成します。 これらの項目のそれぞれが、参照への完全パスを含む項目規定 (項目の `Include` 属性の値) を持ちます。 これらの項目には、以下の新しいメタデータに加え、入力項目のすべてのメタデータも渡されます。  

  - アセンブリを出力フォルダーにコピーするかどうかを示す`CopyLocal`。true または false に設定されます。  

  - 参照の元の項目規定を格納している`OriginalItemSpec`。  

  - `ResolvedFrom`ディレクトリから解決された場合に "{TargetFrameworkDirectory}" に設定される [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。  
  
- COM 参照  
  
     プロジェクト システムは、 `ResolveCOMReferences`という既知の名前を持つターゲットを呼び出します。 このターゲットは、 `ComReferenceWrappers`という項目の種類名を持つ項目を生成します。 これらの項目のそれぞれが、COM 参照のための相互運用機能アセンブリへの完全パスを含む項目規定を持ちます。 これらの項目には、アセンブリを出力フォルダーにコピーするかどうかを示す `CopyLocal`という名前の新しいメタデータ (true または false に設定) に加え、入力項目のすべてのメタデータも渡されます。  
  
- ネイティブ参照  
  
     プロジェクト システムは、 `ResolveNativeReferences`という既知の名前を持つターゲットを呼び出します。 このターゲットは、 `NativeReferenceFile`という項目の種類名を持つ項目を生成します。 これらの項目には、参照の元の項目規定を格納する `OriginalItemSpec`という名前の新しいメタデータに加え、入力項目のすべてのメタデータも渡されます。  
  
## <a name="performance-shortcuts"></a>パフォーマンスに関するヒント  
 Visual Studio の UI でデバッグを開始する (F5 キーを押すか、メニュー バーの **[デバッグ]**、 **[デバッグの開始]** を選択する) と、パフォーマンスを向上させるために、ビルド処理で高速更新チェックを使用します。 カスタマイズされたビルドで、順次ビルドするファイルを作成した場合、高速更新チェックでは変更されたファイルが正しく識別されません。 徹底した更新プログラムのチェックを必要とするプロジェクトでは、 `DISABLEFASTUPTODATECHECK=1`環境変数を設定することで高速チェックを無効にできます。 また、プロジェクトまたはプロジェクトでインポートしたファイルで、MSBuild プロパティとしてこれを設定することもできます。  
  
 Visual Studio の通常のビルドでは、高速更新チェックは適用されず、コマンド プロンプトでビルドを開始する場合と同じ方法でプロジェクトがビルドされます。  
  
## <a name="see-also"></a>参照  
 [方法: Visual Studio のビルドプロセスを拡張する](../msbuild/how-to-extend-the-visual-studio-build-process.md)   
 [IDE 内からのビルドの開始](../msbuild/starting-a-build-from-within-the-ide.md)   
 [.NET Framework の拡張機能を登録しています](../msbuild/registering-extensions-of-the-dotnet-framework.md)   
 [MSBuild の概念](../msbuild/msbuild-concepts.md)   
 [Item 要素 (MSBuild)](../msbuild/item-element-msbuild.md)   
 [Property 要素 (MSBuild)](../msbuild/property-element-msbuild.md)   
 [Target 要素 (MSBuild)](../msbuild/target-element-msbuild.md)   
 [Csc タスク](../msbuild/csc-task.md)   
 [Vbc.exe タスク](../msbuild/vbc-task.md)
