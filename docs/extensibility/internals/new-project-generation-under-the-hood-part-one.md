---
title: '新しいプロジェクト生成: フードの下で、 パート1 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 66778698-0258-467d-8b8b-c351744510eb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aca35e85e57a07a2b411a23d81b99cff9983b9c2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707052"
---
# <a name="new-project-generation-under-the-hood-part-one"></a>新しいプロジェクトの生成: 内部、パート 1
独自のプロジェクトの種類を作成する方法について考えたことがありますか? 新しいプロジェクトを作成すると、実際に何が起こるのでしょうか? フードの下を覗いて、実際に何が起こっているのかを見てみましょう。

 Visual Studio で調整されるタスクがいくつかあります。

- 使用可能なすべてのプロジェクト タイプのツリーが表示されます。

- プロジェクトの種類ごとにアプリケーション テンプレートの一覧が表示され、選択できます。

- プロジェクト名やパスなど、アプリケーションのプロジェクト情報を収集します。

- この情報はプロジェクトファクトリに渡されます。

- 現在のソリューションでプロジェクト項目とフォルダーを生成します。

## <a name="the-new-project-dialog-box"></a>[新しいプロジェクト] ダイアログ ボックス
 新しいプロジェクトのプロジェクトタイプを選択すると、すべて始まります。 まず、[**ファイル**] メニューの **[新しいプロジェクト**] をクリックします。 [**新しいプロジェクト**] ダイアログ ボックスが表示されます。

 ![[新しいプロジェクト] ダイアログ ボックス](../../extensibility/internals/media/newproject.gif "NewProject")

 詳しく見ていきましょう。 **[プロジェクトの種類]** ツリーには、作成できるさまざまなプロジェクト タイプが一覧表示されます。 **Visual C# Windows**などのプロジェクトの種類を選択すると、開始するアプリケーション テンプレートの一覧が表示されます。 **Visual Studio のインストールされたテンプレート**は、Visual Studio によってインストールされ、コンピューターのすべてのユーザーが使用できます。 作成または収集した新しいテンプレートは **、マイ テンプレート**に追加でき、自分だけが利用できます。

 **Windows アプリケーション**などのテンプレートを選択すると、アプリケーションの種類の説明がダイアログ ボックスに表示されます。この場合 **、Windows ユーザー インターフェイスを使用してアプリケーションを作成するためのプロジェクト**。

 [**新しいプロジェクト**] ダイアログ ボックスの下部に、詳細情報を収集する複数のコントロールが表示されます。 表示されるコントロールはプロジェクトの種類によって異なりますが、通常はプロジェクト**名**テキスト ボックス、[**場所]** テキスト ボックスと関連する **[参照**] ボタン、[**ソリューション名]** テキスト ボックス、[**ソリューション用のディレクトリの作成**] チェック ボックスが含まれます。

## <a name="populating-the-new-project-dialog-box"></a>[新しいプロジェクトの設定] ダイアログ ボックス
 **[新しいプロジェクト**] ダイアログ ボックスはどこから情報を取得しますか? ここでは 2 つのメカニズムが使用されていますが、そのうちの 1 つは非推奨です。 [**新しいプロジェクト**]ダイアログ ボックスは、両方のメカニズムから取得した情報を結合して表示します。

 古い (非推奨) メソッドでは、システム レジストリ エントリと .vsdir ファイルが使用されます。 このメカニズムは、Visual Studio が開いたときに実行されます。 新しい方法では .vstemplate ファイルが使用されます。 このメカニズムは、Visual Studio が初期化されるときに実行されます。

```
devenv /setup
```

 or

```
devenv /installvstemplates
```

### <a name="project-types"></a>プロジェクトの種類
 Visual **C#** や**他の言語**などの**プロジェクトの種類**のルート ノードの位置と名前は、システム レジストリ エントリによって決まります。 **データベース**や**スマート デバイス**などの子ノードの構成は、対応する .vstemplate ファイルを含むフォルダーの階層を反映します。 まずルートノードを見てみましょう。

#### <a name="project-type-root-nodes"></a>プロジェクトタイプのルートノード
 初期化[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]されると、システム レジストリ キーのサブキーHKEY_LOCAL_MACHINE\SOFTWARE\VisualStudio\14.0\NewProjectTemplates\TemplateDirs を走査して、**プロジェクトの種類**ツリーのルート ノードをビルドして名前を付けます。 この情報は、後で使用するためにキャッシュされます。 テンプレートディレクトリ\\{FAE04EC1-301F-11D3-BF4B-00C04F79EFBC}\\/1 キーを見てください。 各エントリは、VS パッケージ GUID です。 サブキーの名前 (/1) は無視されますが、その存在は**プロジェクトの種類**のルート ノードであることを示します。 ルート ノードには、**プロジェクトの種類**ツリーでの外観を制御する複数のサブキーが含まれる場合があります。 それらのいくつかを見てみましょう。

##### <a name="default"></a>(既定値)。
 ルート ノードの名前を指定するローカライズされた文字列のリソース ID です。 文字列リソースは、VSPackage GUID によって選択されたサテライト DLL にあります。

 この例では、VS パッケージ GUID は次のようになります。

 {FAE04EC1-301F-11D3-BF4B-00C04F79EFBC}

 ルート ノード (/1) のリソース ID (既定値) が#2345

 近くのパッケージ キーで GUID を検索し、SatelliteDll サブキーを調べると、文字列リソースを含むアセンブリのパスを見つけることができます。

 \<Visual Studio のインストール パス>\VC#\VCSパッケージ\1033\csprojui.dll

 これを確認するには、ファイル エクスプローラーを開き、csprojui.dll を Visual Studio ディレクトリにドラッグします。 文字列テーブルは、リソース #2345に Visual **C#** というキャプションが付いていることを示しています。

##### <a name="sortpriority"></a>SortPriority
 これにより、**プロジェクトタイプ**ツリー内のルートノードの位置が決まります。

 並べ替え優先順位 REG_DWORD 0x00000014 (20)

 優先順位の数が小さいと、ツリー内の位置が高くなります。

##### <a name="developeractivity"></a>開発者の活動
 このサブキーが存在する場合、ルート ノードの位置は [開発者設定] ダイアログ ボックスで制御されます。 たとえば、次のように入力します。

 VCREG_SZ開発者アクティビティ#

 Visual Studio が[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]開発用に設定されている場合、Visual C# がルート ノードになることを示します。 それ以外の場合は、その子ノードが **[その他の言語] の子**ノードになります。

##### <a name="folder"></a>Folder
 このサブキーが存在する場合、ルート ノードは指定されたフォルダーの子ノードになります。 可能なフォルダの一覧がキーの下に表示されます。

 HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\11.0\新しいプロジェクトテンプレート\擬似フォルダ

 たとえば、データベース プロジェクトエントリには、擬似フォルダの他のプロジェクトの種類のエントリと一致するフォルダー キーがあります。 したがって、**プロジェクトの種類**ツリーでは、**データベース プロジェクト**は他のプロジェクトの**種類**の子ノードになります。

#### <a name="project-type-child-nodes-and-vstdir-files"></a>プロジェクトの種類子ノードと .vstdir ファイル
 **プロジェクトタイプ**ツリー内の子ノードの位置は、プロジェクトテンプレートフォルダ内のフォルダの階層に従います。 マシン テンプレート (**Visual Studio がインストールされているテンプレート**) の場合、一般的な場所は \プログラム ファイル\Microsoft Visual Studio 14.0\Common7\IDE\ProjectTemplates\ およびユーザー テンプレート ( マイ\\**テンプレート**) の場合、一般的な場所は \マイ ドキュメント\Visual Studio 14.0\テンプレート\プロジェクト テンプレートです。 これら 2 つの場所のフォルダー階層は、**プロジェクトの種類**ツリーを作成するためにマージされます。

 C# の開発者設定を使用した Visual Studio の**場合、プロジェクトの種類**ツリーは次のようになります。

 ![プロジェクトの種類](../../extensibility/internals/media/projecttypes.png "プロジェクトの種類")

 対応するプロジェクト テンプレート フォルダは次のようになります。

 ![プロジェクト テンプレート](../../extensibility/internals/media/projecttemplates.png "プロジェクトテンプレート")

 [**新しいプロジェクト**] ダイアログ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ボックスが開いたら、ProjectTemplates フォルダを走査し、プロジェクト**タイプ**ツリーで構造を再作成します。

- **プロジェクトタイプ**ツリーのルートノードは、アプリケーションテンプレートによって決定されます。

- ノード名はローカライズでき、特殊文字を含むことができます。

- 並べ替え順序は変更できます。

##### <a name="finding-the-root-node-for-a-project-type"></a>プロジェクトタイプのルートノードの検索
 Visual Studio は、プロジェクト テンプレート フォルダーを走査すると、すべての .zip ファイルを開き、すべての .vstemplate ファイルを抽出します。 .vstemplate ファイルは、XML を使用してアプリケーション テンプレートを記述します。 詳細については、「[新しいプロジェクト生成: フードの下でパート 2](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)」を参照してください。

 プロジェクト\<タイプ>タグは、アプリケーションのプロジェクトタイプを決定します。 たとえば、\CSharp\スマートデバイス\WindowsCE\1033\WindowsCE-空のプロジェクト.zipファイルには、次のタグを持つEmptyProject.vstemplateファイルが含まれています。

```
<ProjectType>CSharp</ProjectType>
```

 \<ProjectType> タグは、プロジェクト テンプレート フォルダー内のサブフォルダーではなく、**プロジェクトの種類**ツリーでアプリケーションのルート ノードを決定します。 この例では、Windows CE アプリケーションは**Visual C#** ルート ノードの下に表示され、WindowsCE フォルダを VisualBasic フォルダに移動しても、Windows CE アプリケーションは**Visual C#** ルート ノードの下に表示されます。

##### <a name="localizing-the-node-name"></a>ノード名のローカライズ
 Visual Studio は、プロジェクト テンプレート フォルダーを走査するときに、見つかった .vstdir ファイルを調べます。 .vstdir ファイルは、**新しいプロジェクト**ダイアログ ボックスでプロジェクトの種類の外観を制御する XML ファイルです。 vstdir ファイルで、LocalizedName \<> タグを使用して**プロジェクトの種類**のノードに名前を付けます。

 たとえば、\CSharp\データベース\テンプレートインデックス.vstdirファイルには次のタグが含まれています。

```
<LocalizedName Package="{462b036f-7349-4835-9e21-bec60e989b9c}" ID="4598"/>
```

 これにより、ルート ノードに名前を付けたローカライズされた文字列 (この場合は Database ) のサテライト DLL とリソース ID**が**決定されます。 ローカライズされた名前には **、.NET**などのフォルダー名では使用できない特殊文字を含めることができます。

 LocalizedName \<> タグが存在しない場合、プロジェクトの種類は、フォルダー自体によって名前が付けられます、 **SmartPhone2003**。

##### <a name="finding-the-sort-order-for-a-project-type"></a>プロジェクトタイプのソート順の検索
 プロジェクトの種類の並べ替え順序を決定するには、.vstdir\<ファイルは SortOrder> タグを使用します。

 たとえば、\CSharp\Windows\Windows.vstdir ファイルには次のタグが含まれています。

```
<SortOrder>5</SortOrder>
```

 \CSharp\データベース\テンプレートインデックス.vstdirファイルには、より大きな値を持つタグがあります。

```
<SortOrder>5000</SortOrder>
```

 \<SortOrder>タグの数値が小さいほど、ツリー内の位置が高くなるので **、Windows**ノードは**プロジェクトタイプ**ツリーの**データベース**ノードよりも高く表示されます。

 プロジェクトの\<種類に SortOrder> タグが指定されていない場合、並べ替え順序>仕様を\<含むプロジェクトの種類の後に、そのタグがアルファベット順に表示されます。

 マイ ドキュメント (**マイ テンプレート**) フォルダには .vstdir ファイルが存在しません。 ユーザー アプリケーション プロジェクトの種類名はローカライズされず、アルファベット順に表示されます。

#### <a name="a-quick-review"></a>クイックレビュー
 **[新しいプロジェクト**] ダイアログ ボックスを変更して、新しいユーザー プロジェクト テンプレートを作成してみましょう。

1. サブフォルダーを \プログラム ファイル\マイクロソフト ビジュアル スタジオ 14.0\Common7\IDE\プロジェクトテンプレート\CSharp フォルダーに追加します。

2. 任意のテキスト エディターを使用して、MyProject.vstdir フォルダーに MyProject.vstdir ファイルを作成します。

3. 次の行を .vstdir ファイルに追加します。

   ```
   <TemplateDir Version="1.0.0">
       <SortOrder>6</SortOrder>
   </TemplateDir>
   ```

4. vstdir ファイルを保存して閉じます。

5. 任意のテキスト エディターを使用して、MyProject.vstemplate フォルダーに MyProject.vstemplate ファイルを作成します。

6. 次の行を .vstemplate ファイルに追加します。

   ```
   <VSTemplate Version="2.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
       <TemplateData>
           <ProjectType>CSharp</ProjectType>
       </TemplateData>
   </VSTemplate>
   ```

7. vstemplate ファイルを保存し、エディターを閉じます。

8. 新しい圧縮された MyProjectNode\MyProject.zip フォルダーに .vstemplate ファイルを送信します。

9. Visual Studio コマンド ウィンドウで、次のように入力します。

    ```
    devenv /installvstemplates
    ```

   Visual Studio を開きます。

10. [**新しいプロジェクト**] ダイアログ ボックスを開き **、Visual C#** プロジェクト ノードを展開します。

    ![MyProjectNode](../../extensibility/internals/media/myprojectnode.png "MyProjectNode")

    **マイプロジェクトノードは**、Windows ノードのすぐ下にビジュアル C# の子ノードとして表示されます。

## <a name="see-also"></a>関連項目
- [新しいプロジェクトの生成: 内部、パート 2](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)
