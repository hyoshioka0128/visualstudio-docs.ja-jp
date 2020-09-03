---
title: ソリューション間の依存関係のマッピング |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.progression.codemap
- vs.progression.standardgraphsdialog
helpviewer_keywords:
- Visual Studio Ultimate, dependency graphs
- code exploration, dependency graphs
- dependency graphs, exporting
- code exploration, relationships
- DGML
- graph documents
- code visualization [Visual Studio ALM]
- graph documents, saving
- dependencies, visualizing
- dependency graphs, saving
- Visual Studio Ultimate, code visualization
- code, visualizing
- dependency graphs, creating
- dependency graphs
- graph documents, exporting
- code exploration, visualizing
ms.assetid: e04850a2-17c5-459b-93ec-6c74143b3292
caps.latest.revision: 245
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d70016229ad9599c7ededbefaf08744f2bb6f351
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548084"
---
# <a name="map-dependencies-across-your-solutions"></a>ソリューション間の依存関係をマップする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード内の依存関係を理解するには、コード マップを作成して視覚化します。 このことは、ファイルとコード行全体を読むことなく、コードの相関を確認するのに役立ちます。

 ![ソリューション間の依存関係を表示する](../modeling/media/codemapsmainintro.png "CodeMapsMainIntro")

 **ビデオ**:

- [視覚化によるコードの依存関係の理解](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Understand-your-code-dependencies-through-visualization)

- [変更の影響の視覚化](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Visualize-the-impact-of-a-change)

- [コード マップで複雑なコードを理解する](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Understanding-complex-code-with-Code-Map-ENU)

## <a name="get-started-with-code-maps"></a><a name="GetStarted"></a> コードマップを使ってみる
 **コード マップを使用するには、次のいずれかが必要です**。

- Visual Studio Enterprise: コード エディター、ソリューション エクスプローラー、クラス ビュー、またはオブジェクト ブラウザーからコード マップを生成できます。

- Visual Studio Professional: コード マップを開き、制限付きの編集を行い、コード内を移動できます。

> [!WARNING]
> Visual Studio Professional を使用する他のユーザーと Visual Studio Enterprise で生成されたマップを共有する前に、非表示の項目、展開されたグループ、グループ間リンクなど、マップのすべての項目が表示されることを確認してください。

 **次の言語でコードの依存関係をマップできます**。

- ソリューションまたはアセンブリの Visual C# .NET または Visual Basic .NET (.dll または .exe)

- Visual C++ プロジェクト、ヘッダー ファイル (.h または `#include`)、またはバイナリのネイティブまたはマネージド C コードまたは C++ コード

- Microsoft Dynamics AX の .NET モジュールから作られた X++ プロジェクトおよびアセンブリ

  **注:** C# または Visual Basic .NET 以外のプロジェクトの場合、コード マップを開始したり、既存のコード マップに項目を追加したりするためのオプションは少なくなります。 たとえば、C++ プロジェクトのテキスト エディター内のオブジェクトを右クリックすることも、コード マップにそのオブジェクト追加することもできません。 ただし、ソリューション エクスプローラー、クラス ビュー、およびオブジェクト ブラウザーから、個々のコード要素またはファイルをドラッグ アンド ドロップできます。

#### <a name="to-see-the-overall-dependencies-across-your-solution"></a>ソリューション内の全体的な依存関係を表示するには

1. **[アーキテクチャ]** メニューを開きます。

2. ソリューションを開いただけでまだビルドしていない場合、または前回のビルド以降にコードを変更した場合は、 **[ソリューションのコード マップを生成]** を選択します。

3. 前回のビルド以降にコードを変更していない場合は、 **[ビルドなしでソリューションのコード マップを生成]** を選択すると、マップ生成時のパフォーマンスが向上します。

4. [全体的な依存関係の表示](#SeeOverviewSource) により、コード マップを使用して、ソリューション全体の依存関係をすべて表示する方法を理解できます。

#### <a name="to-see-specific-dependencies-within-your-solution"></a>ソリューション内の特定の依存関係を表示するには

1. ソリューションを読み込んでから、 **ソリューション エクスプローラー**を開きます。

2. マップする必要のあるプロジェクト、アセンブリ参照、フォルダー、ファイル、型、またはメンバーをすべて選択します。

3. **ソリューションエクスプローラー**ツールバーで、[![選択したノードから新しいグラフを作成します] ボタン](../modeling/media/createnewgraphfromselectedbutton.gif "CreateNewGraphFromSelectedButton")をクリックします。 **Show on Code Map** または、ショートカット メニューを開き、 **[コード マップに表示]** をクリックします。 クラス ビューまたはオブジェクト ブラウザーから新規または既存のコード マップに項目をドラッグすることもできます。

4. [特定の依存関係の表示](#SeeSpecificSource) で、コード マップを使用して、ソリューション内の特定の依存関係を表示する方法を理解します。

### <a name="to-add-a-new-empty-code-map-to-your-solution"></a><a name="CreateEmptyMap"></a> ソリューションに新しい空のコード マップを追加するには

1. **ソリューション エクスプローラー**で、最上位のソリューション ノードのショートカット メニューを表示します。 **[追加]** 、 **[新しい項目]** の順にクリックします。

2. **[インストール済み]** の **[全般]** をクリックします。

3. 右ウィンドウで、 **[有向グラフのドキュメント]** 、 **[追加]** の順に選択します。

     空のマップが作成され、現在のソリューションの **[ソリューション項目]** フォルダーに表示されます。

#### <a name="to-create-a-new-empty-code-map-without-adding-it-to-your-solution"></a>ソリューションに追加せずに新しい空のコード マップを作成するには

1. **[アーキテクチャ]** メニューを開き、 **[新しいコード マップ]** をクリックします。

     \- または

2. **[ファイル]** メニューを開き、 **[新規作成]** 、 **[ファイル]** の順にクリックします。

3. **[インストール済み]** の **[全般]** をクリックします。

4. 右ウィンドウで、 **[有向グラフのドキュメント]** 、 **[開く]** の順に選択します。

     空のマップが作成されますが、現在のソリューションのフォルダーには表示されません。

## <a name="see-overall-dependencies"></a><a name="SeeOverviewSource"></a> 全体的な依存関係の表示

### <a name="see-dependencies-across-your-solution"></a><a name="OverviewSource"></a> ソリューション間の依存関係を表示する

1. **[アーキテクチャ]** メニューで、 **[ソリューションのコード マップを生成]** をクリックします。

    ![コード マップ生成コマンド](../modeling/media/codemapsarchitecturemenu.png "CodeMapsArchitectureMenu")

    最上位レベル アセンブリとそれらのアセンブリ間の集約されたリンクを示すマップが作成されます。 集約リンクを広げると、表される依存関係が多くなります。

2. コード マップ ツールバーの **[凡例]** ボタンを使用して、プロジェクトの種類のアイコン (テスト プロジェクト、Web プロジェクト、Phone プロジェクトなど)、コード項目 (クラス、メソッド、プロパティなど)、および関係の種類 (継承元、実装、呼び出しなど) のリストを表示または非表示にします。

    ![アセンブリの上位&#45;レベルの依存関係グラフ](../modeling/media/dependencygraph-toplevelassemblies.png "DependencyGraph_TopLevelAssemblies")

    このソリューション例には、ソリューション フォルダー (**[テスト]** と **[コンポーネント]**)、テスト プロジェクト、Web プロジェクト、およびアセンブリが含まれています。 既定では、コンテインメイト リレーションシップはすべて、展開および折りたたみができる *グループ*として表示されます。 **[外部]** グループには、プラットフォームの依存関係など、ソリューションの外部のものがすべて含まれます。 外部アセンブリには、使用中の項目のみが表示されます。 既定では、視認性を高めるため、システムの基本型はマップに表示されません。

3. マップをドリル ダウンするには、プロジェクトおよびアセンブリを表すグループを展開します。 **CTRL キーを押しながら A キー** を押してすべてのノードを選択し、ショートカット メニューから **[グループ]**、 **[展開]** の順に選択すると、すべてを展開できます。

    ![コード マップ内のすべてのグループを展開する](../modeling/media/codemapsexpandallgroups.png "CodeMapsExpandAllGroups")

4. ただし、これは大規模なソリューションには不向きな場合があります。 実際、複雑なソリューションでは、メモリ制限のためにすべてのグループを展開できない場合があります。 代わりに、個々のノードを展開して内部を表示します。 マウス ポインターをノード上に移動し、シェブロン (下矢印) が表示されたらクリックします。

    ![コード マップ内のノードを展開する](../modeling/media/dependencygraph-containment.png "DependencyGraph_Containment")

    または、キーボードを使用して項目を選択し、プラスキー () を押し **+** ます。 さらに深いレベルのコードを確認するには、名前空間、型、およびメンバーに対して同じ操作を行います。

   > [!TIP]
   > マウス、キーボード、およびタッチを使用したコードマップの操作の詳細については、「 [コードマップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)」を参照してください。

5. マップを簡略化し個々の部分に注目するには、コード マップ ツールバーで **[フィルター]** を選択し、必要なノードおよびリンクの種類だけを選択します。 たとえば、すべてのソリューション フォルダーとアセンブリのコンテナーを非表示にできます。

    ![コンテナーをフィルター処理して、マップを簡略化する](../modeling/media/codemapsfilterfoldersassemblies.png "CodeMapsFilterFoldersAssemblies")

    個々のグループおよび項目をマップで非表示にしたりマップから削除したりして、マップを簡略化できます。この操作は、基のソリューション コードには影響を与えません。

6. 項目間のリレーションシップを表示するには、マップでそれらを選択します。 リンクの色は、 **[凡例]** ウィンドウの表示に対応しており、リレーションシップの種類を表しています。

    ![ソリューション間の依存関係を表示する](../modeling/media/codemapsmainintro.png "CodeMapsMainIntro")

    この例で、紫色のリンクは呼び出し、点線のリンクは参照、および薄青色のリンクはフィールド アクセスを表しています。 緑色のリンクは継承を表す場合もありますが、複数のリレーションシップ (または *カテゴリ* ) の種類を表す *集約リンク*の可能性もあります。

   > [!TIP]
   > 緑色のリンクが表示されている場合、単に継承関係の存在のみを示しているわけではない可能性があります。 メソッドの呼び出しも存在する場合がありますが、これらは継承関係によって非表示になっています。 特定の種類のリンクを表示するには、 **フィルター** ウィンドウのチェック ボックスを使用して、必要のない種類を非表示にします。

7. 項目またはリンクに関する詳細情報を確認するには、ポインターをその項目の上に移動してツールヒントを表示します。 これにより、コード要素またはリンクが表すカテゴリの詳細が表示されます。

    ![リレーションシップのカテゴリを表示する](../modeling/media/codemapsshowlinkcatgories.png "CodeMapsShowLinkCatgories")

8. 集約リンクによって表される項目と依存関係を調べるには、最初にリンクを選択して、そのショートカット メニューを開きます。 **[寄与するリンクの表示]** または **[新しいコード マップ上の寄与するリンクの表示]** をクリックします。 これにより、リンクの両端のグループが展開され、リンクに関係する項目と依存関係のみが表示されます。

9. マップの特定の部分に注目するために、必要のない項目を継続的に削除することができます。 たとえば、クラス ビューとメンバー ビューを詳細表示するには、 **[フィルター]** ウィンドウですべての名前空間ノードをフィルター処理するだけです。

     ![クラスとメンバーのレベルまでグループをドリルダウンする](../modeling/media/dependencygraph-expandedselectedgroups-2012.png "DependencyGraph_ExpandedSelectedGroups_2012")

10. 複雑なソリューション マップで必要な項目に注目するもう 1 つの方法は、既存のマップから、選択した項目を含む新しいマップを生成することです。 **Ctrl** キーを押しながら注目する項目を選択し、ショートカット メニューを開き、 **[選択項目から新しいグラフを作成]** をクリックします。

     ![選択された項目を新しいコード マップに表示する](../ide/media/codemapsshowonnewmap.png "CodeMapsShowOnNewMap")

11. 含んでいるコンテキストは、新しいマップに引き継がれます。 **[フィルター]** ウィンドウを使用して、ソリューション フォルダーや表示する必要のない他のすべてのコンテナーを非表示にします。

     ![コンテナーをフィルター処理してビューを簡略化する](../modeling/media/codemapsexpandnewgroups.png "CodeMapsExpandNewGroups")

12. グループを展開し、リレーションシップを表示するマップ内の項目を選択します。

     ![リレーションシップを表示する項目を選択する](../modeling/media/codemapsviewnewrelationships.png "CodeMapsViewNewRelationships")

    関連項目:

- [コード マップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)

- [DGML ファイルを編集してコード マップをカスタマイズする](../modeling/customize-code-maps-by-editing-the-dgml-files.md)

- [アナライザーを実行](../modeling/find-potential-problems-using-code-map-analyzers.md)して、コード内の潜在的な問題を見つけます。

### <a name="see-dependencies-across-assemblies-or-binaries"></a><a name="OverviewCompiled"></a> アセンブリまたはバイナリ間の依存関係の表示

1. [空のコード マップを作成する](#GetStarted)か、既存のコード マップ (.dgml ファイル) を開きます。

2. Visual Studio の外部から、マップするアセンブリまたはバイナリをマップにドラッグします。 たとえば、Windows エクスプローラーまたはファイル エクスプローラーから、アセンブリやバイナリをドラッグします。

> [!NOTE]
> Windows エクスプローラーまたはファイル エクスプローラーからアセンブリやバイナリをドラッグできるのは、エクスプローラーを同じユーザー アクセス制御 (UAC) アクセス許可レベルで実行している場合のみです。 たとえば、UAC がオンになっていて、Visual Studio を管理者として実行している場合、Windows エクスプローラーまたはファイル エクスプローラーはドラッグ操作をブロックします。 これを回避するには、両者が同じアクセス許可レベルで実行するようにするか、UAC を無効にします。

## <a name="see-specific-dependencies"></a><a name="SeeSpecificSource"></a> 特定の依存関係の表示
 たとえば、保留中の変更があるいくつかのファイルでコード レビューを行うとします。 これらの変更の依存関係を表示するため、これらのファイルからコード マップを作成できます。

 ![特定の依存関係をコード マップに表示する](../modeling/media/codemapsspecificdependenciesintro.png "CodeMapsSpecificDependenciesIntro")

### <a name="see-specific-dependencies-in-your-solution"></a>ソリューション内の特定の依存関係の表示

1. **ソリューション エクスプローラー**を開きます。 関心のあるプロジェクト、アセンブリ参照、フォルダー、ファイル、型、およびメンバーを選択します。 型またはメンバーの依存関係を持つ項目を探すには、 **ソリューション エクスプローラー**から型またはメンバーのショートカット メニューを開きます。 依存関係の種類を選択し、結果をクリックします。

2. 項目とそのメンバーをマップします。 **ソリューションエクスプローラー**ツールバーで、[**コードマップに表示**] をクリックし、[![選択したノードから新しいグラフを作成します] ボタン](../modeling/media/createnewgraphfromselectedbutton.gif "CreateNewGraphFromSelectedButton")をクリックします。

     ![マップする項目を選択する](../modeling/media/codemapsselectinsolutionexplorer.png "CodeMapsSelectInSolutionExplorer")

3. アセンブリ内の選択した項目がマップに表示されます。

     ![マップでグループとして表示するように選択された項目](../modeling/media/codemapsshowitemsfromsolnexplorer.png "CodeMapsShowItemsFromSolnExplorer")

     ソリューション エクスプローラー、クラス ビュー、またはオブジェクト ブラウザーから、項目を空のコード マップまたは既存のコード マップにドラッグすることもできます。 空のマップを作成するには、「 [空のコード マップを作成する](#GetStarted)」を参照してください。 項目の親階層を含めるには、 **Ctrl** キーを押したまま項目をドラッグするか、コード マップ ツールバーで **[親を含める]** ボタンを使用して既定のアクションを指定します。

    > [!NOTE]
    > Windows Phone または Windows ストアなどの複数のアプリで共有されるプロジェクトから項目を追加すると、その項目は、現在アクティブなアプリ プロジェクトと共にマップに表示されます。 コンテキストを別のアプリ プロジェクトに変更し、共有プロジェクトからさらに項目を追加した場合、その項目は、新しくアクティブになったアプリ プロジェクトと共に表示されます。 マップ上の項目に実行する操作は、同じコンテキストを共有する項目にのみ適用されます。

4. 項目を確認するには、その項目を展開します。 マウス ポインターを項目の上に移動し、シェブロン (下矢印) アイコンが表示されたらクリックします。

     ![コード マップ内のノードを展開する](../modeling/media/dependencygraph-containment.png "DependencyGraph_Containment")

     すべての項目を展開するには、 **CTRL キーを押しながら A キー**を押してそれらを選択し、マップのショートカット メニューを開いて、 **[グループ]**、 **[展開]** の順にクリックします。 ただし、すべてのグループを展開すると使用に適さないマップになったりメモリの問題が発生したりする場合、このオプションは使用できません。

5. 確認したい項目を、必要に応じてクラスやメンバーのレベルまで展開します。

     ![クラスとメンバーのレベルにグループを展開する](../modeling/media/codemapsexpandtoclassandmember.png "CodeMapsExpandToClassAndMember")

     コードに含まれるがマップに表示されないメンバーを表示するには、グループの左上隅にある **再フェッチ children** アイコン ![再フェッチ children アイコン](../modeling/media/dependencygraph-deletednodesicon.png "DependencyGraph_DeletedNodesIcon") をクリックします。

6. マップ上の項目に関連する項目をさらに表示するには、1 つを選択し、コード マップ ツールバーで **[関連表示]** を選択して、マップに追加する関連項目の種類を選択します。 あるいは、1 つまたは複数の項目を選択し、ショートカット メニューを開き、マップに追加する関連項目の種類の **[表示...]** オプションを選択します。 次に例を示します。

     **アセンブリ**の場合、次のように選択します。

    |オプション|説明|
    |-|-|
    |**参照されるアセンブリの表示**|このアセンブリの参照先のアセンブリを追加します。 外部アセンブリは **[外部]** グループに表示されます。|
    |**参照元のアセンブリの表示**|このアセンブリを参照するソリューション内のアセンブリを追加します。|

     **名前空間**の場合、表示されていなければ、 **[含んでいるアセンブリの表示]** をクリックします。

     **クラス** または **インターフェイス**の場合は、次から選択します。

    |オプション|説明|
    |-|-|
    |**基本型の表示**|クラスの場合、基底クラスおよび実装されたインターフェイスを追加します。<br /><br /> インターフェイスの場合、基本インターフェイスを追加します。|
    |**派生型の表示**|クラスの場合、派生クラスを追加します。<br /><br /> インターフェイスの場合、派生インターフェイスと、実装するクラスまたは構造体を追加します。|
    |**参照される型の表示**|すべてのクラスと、このクラスが使用するメンバーを追加します。|
    |**参照元の型の表示**|すべてのクラスと、このクラスを使用するメンバーを追加します。|
    |**含んでいる名前空間の表示**|親の名前空間を追加します。|
    |**含んでいる名前空間とアセンブリの表示**|親コンテナーの階層を追加します。|
    |**すべての基本型の表示**|基底クラスまたはインターフェイス階層を再帰的に追加します。|
    |**すべての派生型の表示**|クラスの場合、すべての派生クラスを再帰的に追加します。<br /><br /> インターフェイスの場合、すべての派生インターフェイスと、実装するクラスまたは構造体を再帰的に追加します。|

     **メソッド**の場合、次から選択します。

    |オプション|説明|
    |-|-|
    |**呼び出されるメソッドの表示**|このメソッドが呼び出すメソッドを追加します。|
    |**参照されるフィールドの表示**|このメソッドが参照するフィールドを追加します。|
    |**含んでいる型の表示**|親の型を追加します。|
    |**含んでいる型、名前空間、およびアセンブリの表示**|親コンテナーの階層を追加します。|
    |**オーバーライドされたメソッドの表示**|他のメソッドをオーバーライドするか、インターフェイスのメソッドを実装するメソッドの場合、オーバーライドされた基底クラスのすべての抽象メソッドまたは仮想メソッド、および実装されたインターフェイスのメソッドがある場合はそのメソッドを追加します。|

     **フィールド** または **プロパティ**の場合、次から選択します。

    |オプション|説明|
    |-|-|
    |**含んでいる型の表示**|親の型を追加します。|
    |**含んでいる型、名前空間、およびアセンブリの表示**|親コンテナーの階層を追加します。|

     ![このメンバーによって呼び出されるメソッドを表示する](../modeling/media/codemapsshowrelatedmethods.png "CodeMapsShowRelatedMethods")

7. マップには、リレーションシップが表示されます。 この例では、 `Find` メソッドによって呼び出されるメソッド、およびそれらのメソッドの場所 (ソリューション内あるいは外部) です。

     ![特定の依存関係をコード マップに表示する](../modeling/media/codemapsspecificdependenciesintro.png "CodeMapsSpecificDependenciesIntro")

8. マップを簡略化し個々の部分に注目するには、コード マップ ツールバーで **[フィルター]** を選択し、必要なノードおよびリンクの種類だけを選択します。 たとえば、ソリューション フォルダー、アセンブリ、および名前空間の表示をオフにします。

     ![フィルター ペインを使用して表示を簡略化する](../modeling/media/almcodemapfilterpane.png "ALMCodeMapFilterPane")

## <a name="see-dependencies-between-c-and-c-source-files-and-header-files"></a><a name="SeeSourceHeader"></a> C および C++ のソース ファイルとヘッダー ファイルの間の依存関係の表示
 C++ プロジェクトのより完全なマップを作成する場合は、そのプロジェクトに対してブラウザー情報のコンパイラ オプション (**/FR**) を設定します。 「 [/FR, /Fr (Create .Sbr File)](https://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896)」を参照してください。 設定されていない場合は、メッセージが表示され、このオプションを設定することが求められます。 **[OK]** を選択した場合、このオプションは現在のマップに対してのみ設定されます。 以後のすべてのマップについて、メッセージを非表示にするように選択できます。 このメッセージを非表示にしても、再び表示されるようにできます。 次のレジストリ キーを `0` に設定するか、削除します。

 **HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\14.0\NativeProvider: AutoEnableSbr**

 Visual C++ のプロジェクトを含むソリューションを開くときは、IntelliSense データベースの更新に時間がかかる場合があります。 この間は、IntelliSense データベースの更新が終了するまで、ヘッダー (.h または `#include`) ファイルのコード マップを生成できない場合があります。 更新の進行状況は、Visual Studio のステータス バーで監視できます。 IntelliSense の特定の設定が無効になっているために表示されるメッセージまたは問題を解決するには、「 [C および C++ コードのマップのトラブルシューティング](#Troubleshooting)」を参照してください。

- ソリューションのすべてのソース ファイルとヘッダー ファイル間の依存関係を表示するには、 **[アーキテクチャ]** メニューで、 **[インクルード ファイルのグラフを生成]** をクリックします。

     ![ネイティブ コードの依存関係グラフ](../modeling/media/dependencygraphgeneral-nativecode.png "DependencyGraphGeneral_NativeCode")

- 現在開いているファイルと関連するソース ファイルおよびヘッダー ファイルとの間の依存関係を表示するには、そのソース ファイルまたはヘッダー ファイルを開きます。 ファイル内の任意の場所でファイル ショートカット メニューを開きます。 **[インクルード ファイルのグラフを生成]** をクリックします。

     ![.H ファイルの最初の&#45;レベルの依存関係グラフ](../modeling/media/dependencygraph-native-firstlevel.png "DependencyGraph_Native_FirstLevel")

### <a name="troubleshoot-maps-for-c-and-c-code"></a><a name="Troubleshooting"></a> C および C++ コードのマップのトラブルシューティング
 これらの項目は C および C++ コードではサポートされていません。

- 基本型は、親階層を含むマップには表示されません。

- **表示** メニューのほとんどの項目は、C および C++ コードでは使用できません。

  C および C++ のコードのコード マップを生成するときに、次の問題が発生する場合があります。

|**問題点**|**考えられる原因**|**解像度**|
|---------------|------------------------|--------------------|
|コード マップを生成できませんでした。|ソリューション内のプロジェクトが正常にビルドされませんでした。|発生したビルド エラーを修正してから、マップを再生成します。|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [アーキテクチャ] **メニューからコード マップを生成しようとすると、** が応答しなくなる。|プログラム データベース (.pdb) ファイルが壊れている可能性があります。<br /><br /> .pdb ファイルには、型、メソッド、ソース ファイル情報などのデバッグ情報が格納されます。|ソリューションをリビルドしてから、もう一度実行します。|
|IntelliSense 参照データベースの特定の設定が無効になる。|IntelliSense の特定の設定が、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**[オプション]** ダイアログ ボックスで無効になっている可能性があります。|設定をオンにして有効にします。<br /><br /> 「 [オプション」、「テキストエディター」、「C/c + +」、「詳細](../ide/reference/options-text-editor-c-cpp-advanced.md)」を参照してください。|
|" **不明なメソッド** " という内容のメッセージがメソッド ノードで表示される。<br /><br /> この問題は、メソッドの名前を解決できないために発生します。|バイナリ ファイルにベース再配置テーブルがない可能性があります。|リンカーで **/FIXED:NO** オプションをオンにします。<br /><br /> 「 [/FIXED (Fixed Base Address)](https://msdn.microsoft.com/library/929bba5e-b7d8-40ed-943e-056aa3710fc5)」を参照してください。|
||プログラム データベース (.pdb) ファイルがビルドされていない可能性があります。<br /><br /> .pdb ファイルには、型、メソッド、ソース ファイル情報などのデバッグ情報が格納されます。|リンカーで **/DEBUG** オプションをオンにします。<br /><br /> 「 [/DEBUG (Generate Debug Info)](https://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103)」を参照してください。|
||予想される場所で .pdb ファイルを開くことができないか、ファイルが見つかりません。|.pdb ファイルが予想される場所にあることを確認します。|
||デバッグ情報が .pdb ファイルから取り除かれています。|**/PDBSTRIPPED** オプションをリンカーで使用した場合は、代わりに完全な .pdb ファイルを使用します。<br /><br /> 「 [/PDBSTRIPPED (Strip Private Symbols)](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55)」を参照してください。|
||呼び出し元が関数ではなく、バイナリ ファイル内のサンクまたはデータ セクション内のポインターです。|呼び出し元がサンクの場合は、 `_declspec(dllimport)` を使用してサンクの回避を試みます。<br /><br /> 参照:<br /><br /> -   [一般的な規則と制限事項](https://msdn.microsoft.com/library/6c48902d-4259-4761-95d4-e421d69aa050)<br />-   [__Declspec (dllimport) を使用した関数呼び出しのインポート](https://msdn.microsoft.com/library/6b53c616-0c6d-419a-8e2a-d2fff20510b3)<br />-   [dllexport、dllimport](https://msdn.microsoft.com/library/ff95b645-ef55-4e72-b848-df44657b3208)|

## <a name="make-code-maps-render-more-quickly"></a><a name="RenderMoreQuickly"></a> コード マップをよりすばやく表示する
 マップを初めて生成したときに、Visual Studio は、見つかったすべての依存関係のインデックスを作成します。 このプロセスには、特に大規模なソリューションの場合に時間がかかることがありますが、以降のパフォーマンスは向上します。 コードを変更すると、Visual Studio は、更新されたコードのインデックスだけを再作成します。 マップの表示にかかる時間を最小限に抑えたい場合は、次の作業を検討してください。

- [目的の依存関係のみをマップする。](#SeeSpecificSource)

- ソリューション全体のマップを生成する前に、ソリューションのスコープを縮小する。

- コード マップ ツールバーの **[ビルドのスキップ]** ボタンを使用して、ソリューションの自動ビルドをオフにする。

- コード マップ ツールバーの **[親を含める]** ボタンを使用して、親項目の自動追加をオフにする。

- コード マップ ファイルを直接編集し、不要なノードとリンクを削除する。 マップを変更しても、基のコードには影響しません。 「 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

  ![[ビルドのスキップ] ボタンと [親を含める] ボタン](../modeling/media/codemapsfilterskipbuildicons.png "CodeMapsFilterSkipBuildIcons")

  Visual Studio は 1 GB のメモリで実行できますが、Visual Studio でコード インデックスを作成してマップを生成する際の待ち時間が長くならないように、メモリを 2 GB 以上搭載したコンピューターを使用することをお勧めします。

  プロジェクト項目の **[出力ディレクトリにコピー]** プロパティが **[常にコピーする]** に設定されていると、マップの生成や、ソリューション エクスプローラーからマップへの項目の追加に時間がかかることがあります。 これにより、インクリメンタル ビルドと Visual Studio でプロジェクトが毎回リビルドされることになる問題が発生する場合があります。 パフォーマンスを向上させるには、このプロパティを **[新しい場合はコピーする]** または `PreserveNewest`に変更します。 「 [Incremental Builds](../msbuild/incremental-builds.md)」を参照してください。

  完成されたマップには、ビルドに成功したコードの依存関係のみが表示されます。 特定のコンポーネントにビルド エラーが発生すると、そのエラーがマップに表示されます。 マップに基づいてアーキテクチャを決定する前に、コンポーネントが実際にビルドされ、その依存関係がマップ上に表示されていることを確認してください。

## <a name="share-code-maps"></a><a name="SavingExporting"></a> コード マップの共有

### <a name="share-the-map-with-other-visual-studio-users"></a>マップを他の Visual Studio ユーザーと共有する
 マップを保存するには、 **[ファイル]** メニューを使用します。

 - または -

 マップを特定のプロジェクトの一部として保存するには、マップのツールバーで、[**共有**]、[.dgml の**移動**] の順に選択し、 \<*CodeMapName*> **.dgml into**マップを保存するプロジェクトを選択します。

 ![マップを別のプロジェクトに移動する](../modeling/media/codemapsmovemapmenu.png "CodeMapsMoveMapMenu")

 Visual Studio では、マップは .dgml ファイル形式で保存され、他の Visual Studio Enterprise および Visual Studio Professional ユーザーと共有できます。

> [!NOTE]
> Visual Studio Professional を使用するユーザーとマップを共有する前に、グループを展開しておくこと、非表示のノードとグループ間リンクを表示しておくこと、マップに表示する必要のある削除済みのノードを取得しておくことが必要です。 そうしない場合、他のユーザーはそれらの項目を表示できなくなります。
>
> モデリング プロジェクト内のマップまたはモデリング プロジェクトから別の場所にコピーされたマップを保存すると、次のエラーが発生する可能性があります。
>
> "プロジェクト ディレクトリの外部で *fileName* を保存できません。 リンクされた項目はサポートされていません。"
>
> Visual Studio にはエラーが表示されます。ただし、保存したバージョンは生成されます。 このエラーを回避するには、モデリング プロジェクトの外部でマップを生成します。 その後、目的の場所にグラフを保存できます。 単にソリューション内の別の場所にファイルをコピーし、その後で保存しようとすると失敗します。

### <a name="export-the-map-as-an-image-so-you-can-copy-it-into-other-applications-such-as-microsoft-word-or-powerpoint"></a>Microsoft Word や PowerPoint などの他のアプリケーションにコピーできるように、マップをイメージとしてエクスポートする

1. コード マップ ツールバーで、 **[共有]**、 **[画像として電子メールで送信]** または **[イメージのコピー]** の順にクリックします。

2. そのイメージを他のアプリケーションに貼り付けます。

### <a name="export-the-map-as-an-xps-file-so-you-can-see-it-in-xml-or-xaml-viewers-like-internet-explorer"></a>Internet Explorer のような XML ビューアーや XAML ビューアーで表示できるように、マップを XPS ファイルとしてエクスポートする

1. コード マップ ツールバーで、 **[共有]**、 **[ポータブル XPS として電子メールで送信]** または **[ポータブル XPS として保存]** の順にクリックします。

2. ファイルを保存する場所を参照します。

3. コード マップの名前を付けます。 [ **名前を付けて保存** ] ボックスが **xps ファイル ( \* .xps)** に設定されていることを確認します。 **[保存]** を選びます。

## <a name="what-else-can-i-do"></a>その他にできること

- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)

- [デバッグを行うときの呼び出し履歴に対するメソッドのマップ](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)

- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)

- [コード マップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)

- [DGML ファイルを編集してコード マップをカスタマイズする](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
