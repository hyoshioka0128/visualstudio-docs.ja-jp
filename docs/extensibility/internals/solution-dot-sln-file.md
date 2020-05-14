---
title: ソリューション (.Sln) ファイル
ms.date: 03/15/2019
ms.topic: conceptual
helpviewer_keywords:
- sln files, VSPackages
- solutions, .sln files
- .sln files, VSPackages
ms.assetid: 7d7ef539-2e4b-4637-b853-8ec7626609df
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9f4eee1f0a5e8371d239b3c33d10e1d9d7998095
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705328"
---
# <a name="solution-sln-file"></a>ソリューション (.sln) ファイル

ソリューションは、Visual Studio でプロジェクトを整理するための構造です。 ソリューションは、プロジェクトの状態情報を 2 つのファイルに保持します。

- .sln ファイル (テキスト ベース、共有)

- .suo ファイル (バイナリ、ユーザー固有のソリューション オプション)

suo ファイルの詳細については、「ソリューション[ユーザー オプション (.Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md).

VSPackage が .sln ファイルで参照された結果として読み込まれる場合、環境は<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A>.sln ファイルで読み取りを呼び出します。

.sln ファイルには、永続化されたデータと参照するプロジェクト VSPackages の名前値パラメーターを検索して読み込むために、環境が使用するテキスト ベースの情報が含まれています。 ユーザーがソリューションを開くと、環境は`preSolution`、.sln ファイル内の 、`Project`ソリューション`postSolution`内のプロジェクト、およびソリューションに添付されている永続化された情報を読み込むために、.sln ファイル内の情報を循環します。

各プロジェクトのファイルには、そのプロジェクトの項目を階層に取り込むために環境によって読み取られた追加情報が含まれています。 階層データの永続性は、プロジェクトによって制御されます。 通常、データは .sln ファイルに格納されませんが、プロジェクト情報を .sln ファイルに書き込む場合は、そのファイルに意図的に書き込むことができます。 永続性の詳細については、「[プロジェクトの永続性](../../extensibility/internals/project-persistence.md)」および「[プロジェクト項目を開いて保存](../../extensibility/internals/opening-and-saving-project-items.md)する 」を参照してください。

## <a name="file-header"></a>ファイルヘッダー

.sln ファイルのヘッダーは次のようになります。

::: moniker range="vs-2017"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio 15
VisualStudioVersion = 15.0.26730.15
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>定義

`Microsoft Visual Studio Solution File, Format Version 12.00`\
ファイル形式のバージョンを定義する標準ヘッダー。

`# Visual Studio 15`\
このソリューション ファイルを (最近) 保存した Visual Studio のメジャー バージョン。 この情報は、ソリューション アイコンのバージョン番号を制御します。

`VisualStudioVersion = 15.0.26730.15`\
(最近) ソリューション ファイルを保存した Visual Studio の完全なバージョン。 ソリューション ファイルが、同じメジャー バージョンを持つ新しいバージョンの Visual Studio によって保存された場合、この値は、ソリューション ファイルの解約を軽減するために更新されません。

`MinimumVisualStudioVersion = 10.0.40219.1`\
このソリューション ファイルを開くことができる、Visual Studio の最小 (最も古い) バージョン。

::: moniker-end

::: moniker range=">=vs-2019"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio Version 16
VisualStudioVersion = 16.0.28701.123
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>定義

`Microsoft Visual Studio Solution File, Format Version 12.00`\
ファイル形式のバージョンを定義する標準ヘッダー。

`# Visual Studio Version 16`\
このソリューション ファイルを (最近) 保存した Visual Studio のメジャー バージョン。 この情報は、ソリューション アイコンのバージョン番号を制御します。

`VisualStudioVersion = 16.0.28701.123`\
(最近) ソリューション ファイルを保存した Visual Studio の完全なバージョン。 ソリューション ファイルが、同じメジャー バージョンを持つ新しいバージョンの Visual Studio によって保存された場合、この値は更新されず、ファイルの解約が軽減されます。

`MinimumVisualStudioVersion = 10.0.40219.1`\
このソリューション ファイルを開くことができる、Visual Studio の最小 (最も古い) バージョン。

::: moniker-end

## <a name="file-body"></a>ファイル本文

.sln ファイルの本文は、次のように、 という`GlobalSection`ラベルが付いた複数のセクションで構成されます。

```
Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1", "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
EndProject
Global
  GlobalSection(SolutionNotes) = postSolution
  EndGlobalSection
  GlobalSection(SolutionConfiguration) = preSolution
       ConfigName.0 = Debug
       ConfigName.1 = Release
  EndGlobalSection
  GlobalSection(ProjectDependencies) = postSolution
  EndGlobalSection
  GlobalSection(ProjectConfiguration) = postSolution
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.ActiveCfg = Debug|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.Build.0 = Debug|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.ActiveCfg = Release|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.Build.0 = Release|x86
  EndGlobalSection
  GlobalSection(ExtensibilityGlobals) = postSolution
  EndGlobalSection
  GlobalSection(ExtensibilityAddIns) = postSolution
  EndGlobalSection
EndGlobal
```

ソリューションを読み込むには、環境で次の一連のタスクが実行されます。

1. 環境は .sln ファイルのグローバル セクションを読み取り、`preSolution`とマークされたすべてのセクションを処理します。 このファイル例では、次のようなステートメントが 1 つあります。

   ```
   GlobalSection(SolutionConfiguration) = preSolution
        ConfigName.0 = Debug
        ConfigName.1 = Release
   ```

   環境は、タグを`GlobalSection('name')`読み取るとき、レジストリを使用して VSPackage に名前をマップします。 キー名は[HKLM\\<アプリケーション ID レジストリ ルート\>\ソリューション永続性\集計 GUID] の下のレジストリに存在する必要があります。 キーの既定値は、エントリを書き込んだ VSPackage のパッケージ GUID (REG_SZ) です。

2. 環境は、VSPackage を読`QueryInterface`み込み、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>インターフェイスの VSPackage を<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A>呼び出し、VSPackage がデータを格納できるように、セクション内のデータを使用してメソッドを呼び出します。 環境では、セクションごとに`preSolution`このプロセスを繰り返します。

3. 環境は、プロジェクトの永続性ブロックを反復処理します。 この場合、1 つのプロジェクトがあります。

   ```
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
   EndProject
   ```

   このステートメントには、一意のプロジェクト GUID とプロジェクトの種類の GUID が含まれています。 この情報は、ソリューションに属するプロジェクト ファイル、および各プロジェクトに必要な VSPackage を見つけるために環境によって使用されます。 プロジェクト GUID は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>プロジェクトに関連する特定の VSPackage を読み込むために渡され、その後、プロジェクトは、VSPackage によって読み込まれます。 この場合、このプロジェクトに読み込まれる VSPackage は Visual Basic です。

   各プロジェクトは、ソリューション内の他のプロジェクトが必要に応じてアクセスできるように、一意のプロジェクト インスタンス ID を保持できます。 ソリューションとプロジェクトがソース コード管理下にある場合、プロジェクトへのパスはソリューションへのパスを基準にするのが理想的です。 ソリューションが最初に読み込まれたときに、プロジェクト ファイルをユーザーのコンピューターに置くことはできません。 ソリューション ファイルに関連してプロジェクト ファイルをサーバーに格納することで、プロジェクト ファイルを見つけてユーザーのコンピュータにコピーするのも比較的簡単です。 次に、プロジェクトに必要な残りのファイルをコピーして読み込みます。

4. 環境は、.sln ファイルのプロジェクト セクションに含まれる情報に基づいて、各プロジェクト ファイルを読み込みます。 プロジェクト自体は、プロジェクト階層の設定と入れ子になったプロジェクトの読み込みを行います。

5. .sln ファイルのすべてのセクションが処理されると、ソリューションがソリューション エクスプローラーに表示され、ユーザーが変更できるようになります。

ソリューション内のプロジェクトを実装する VSPackage が読み込みに失敗<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A>した場合、メソッドが呼び出され、ソリューション内の他のすべてのプロジェクトは、読み込み中に行った変更を無視する機会が与えられます。 解析エラーが発生した場合、ソリューション ファイルにできるだけ多くの情報が保存され、ソリューションが破損していることを警告するダイアログ ボックスが表示されます。

ソリューションが保存または終了されると、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A>メソッドが呼び出され、階層に渡され、.sln ファイルに入力する必要があるソリューションに変更が加えられているかどうかを確認します。 に渡される`QuerySaveSolutionProps`<xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS>null 値は、ソリューションの情報が永続化されていることを示します。 値が null でない場合、永続化された情報は、インターフェイスへのポインターによって決定される特定のプロジェクトに<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>対するものです。

保存する情報がある場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>インターフェイスは<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A>メソッドへのポインターを使用して呼び出されます。 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>メソッドは、インターフェイスから`IPropertyBag`名前と値のペアを取得し、情報を .sln ファイルに書き込むために、環境によって呼び出されます。

`SaveSolutionProps`オブジェクト`WriteSolutionProps`は、すべての変更が .sln ファイルに入力されるまで、インターフェイス`IPropertyBag`から保存される情報を取得するために、環境によって再帰的に呼び出されます。 これにより、ソリューションと共に情報が保持され、次回ソリューションを開いたときに使用できるようになります。

すべての読み込まれた VSPackage は、.sln ファイルに保存する何かを持っているかどうかを確認するために列挙されます。 レジストリ キーが照会されるのは、読み込み時だけです。 環境は、ソリューションが保存された時点でメモリに含まれているため、読み込まれたパッケージのすべてが認識されます。

セクションと セクションにエントリが含まれているの`preSolution`は`postSolution`、.sln ファイルだけです。 ソリューションが正しく読み込まれるには、この情報が必要なので、.suo ファイルに類似したセクションはありません。 suo ファイルには、共有したりソース コード管理下に配置したりすることを意図していない、プライベート メモなどのユーザー固有のオプションが含まれています。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- [ソリューション ユーザー オプション (.Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md)
- [ソリューション](../../extensibility/internals/solutions-overview.md)
