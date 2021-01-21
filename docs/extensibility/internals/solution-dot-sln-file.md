---
title: ソリューション (..Sln) ファイル
description: .Sln ファイルについて説明します。これは、Visual Studio でプロジェクトの状態情報を保持するファイルの1つです。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 903b33d72d3a97eb4ed3f7ad0bc865999bee54cf
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877508"
---
# <a name="solution-sln-file"></a>ソリューション (.sln) ファイル

ソリューションは、Visual Studio でプロジェクトを整理するための構造です。 このソリューションでは、プロジェクトの状態情報を次の2つのファイルに保持します。

- .sln ファイル (テキストベース、共有)

- .suo ファイル (バイナリ、ユーザー固有のソリューションオプション)

.Suo ファイルの詳細については、「 [ソリューションユーザーオプション (」を参照してください。.Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md)。

VSPackage が .sln ファイルで参照された結果として読み込まれた場合、環境はを呼び出して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> .sln ファイルを読み取ります。

.Sln ファイルには、永続化されたデータの名前と値のパラメーターの検索と読み込みに使用するテキストベースの情報が含まれています。この情報は、Vspackage が参照するプロジェクトです。 ユーザーがソリューションを開くと、環境は .sln ファイル内の、、およびの情報を循環して、ソリューション、ソリューション `preSolution` `Project` 内の `postSolution` プロジェクト、およびソリューションに関連付けられている保存された情報を読み込みます。

各プロジェクトのファイルには、そのプロジェクトの項目を階層に設定するために環境によって読み取られた追加情報が含まれています。 階層データの永続化は、プロジェクトによって制御されます。 通常、データは .sln ファイルに格納されませんが、.sln ファイルにプロジェクト情報を意図的に書き込むことができます。 永続化の詳細については、「 [プロジェクトの永続](../../extensibility/internals/project-persistence.md) 化」と「 [プロジェクト項目を開いて保存](../../extensibility/internals/opening-and-saving-project-items.md)する」を参照してください。

## <a name="file-header"></a>ファイルヘッダー

.Sln ファイルのヘッダーは次のようになります。

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
(最近の) Visual Studio のメジャーバージョンは、このソリューションファイルを保存しました。 この情報は、ソリューションアイコンのバージョン番号を制御します。

`VisualStudioVersion = 15.0.26730.15`\
ソリューションファイルが保存された (最近の) 完全バージョンの Visual Studio。 同じメジャーバージョンを持つ新しいバージョンの Visual Studio によってソリューションファイルが保存されている場合、ソリューションファイルのチャーンを軽減するために、この値は更新されません。

`MinimumVisualStudioVersion = 10.0.40219.1`\
このソリューションファイルを開くことができる Visual Studio の最小 (最も古い) バージョン。

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
(最近の) Visual Studio のメジャーバージョンは、このソリューションファイルを保存しました。 この情報は、ソリューションアイコンのバージョン番号を制御します。

`VisualStudioVersion = 16.0.28701.123`\
ソリューションファイルが保存された (最近の) 完全バージョンの Visual Studio。 同じメジャーバージョンを持つ新しいバージョンの Visual Studio によってソリューションファイルが保存されている場合、ファイルのチャーンを軽減するために、この値は更新されません。

`MinimumVisualStudioVersion = 10.0.40219.1`\
このソリューションファイルを開くことができる Visual Studio の最小 (最も古い) バージョン。

::: moniker-end

## <a name="file-body"></a>ファイルの本文

.Sln ファイルの本文は、次の `GlobalSection` ように、というラベルの付いたいくつかのセクションで構成されています。

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

ソリューションを読み込むには、環境で次の一連のタスクを実行します。

1. 環境は、.sln ファイルのグローバルセクションを読み取り、とマークされたすべてのセクションを処理し `preSolution` ます。 この例のファイルには、次のようなステートメントが1つあります。

   ```
   GlobalSection(SolutionConfiguration) = preSolution
        ConfigName.0 = Debug
        ConfigName.1 = Release
   ```

   環境がタグを読み取ると、 `GlobalSection('name')` レジストリを使用して、名前を VSPackage にマップします。 キー名は、[HKLM \\<APPLICATION ID Registry Root \SolutionPersistence\AggregateGUIDs] の下のレジストリに存在する必要があり \> ます。 キーの既定値は、エントリを書き込んだ VSPackage のパッケージ GUID (REG_SZ) です。

2. 環境は、VSPackage を読み込み、 `QueryInterface` インターフェイスの VSPackage に対してを呼び出し、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> VSPackage がデータを格納できるように、セクションのデータを使用してメソッドを呼び出します。 環境によって、各セクションでこのプロセスが繰り返され `preSolution` ます。

3. 環境は、プロジェクトの永続化ブロックを反復処理します。 この場合、1つのプロジェクトがあります。

   ```
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
   EndProject
   ```

   このステートメントには、一意のプロジェクト GUID とプロジェクトの種類の GUID が含まれています。 この情報は、ソリューションに属するプロジェクトファイル、および各プロジェクトに必要な VSPackage を検索するために、環境によって使用されます。 プロジェクト GUID は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> プロジェクトに関連する特定の VSPackage を読み込むためにに渡され、プロジェクトは VSPackage によって読み込まれます。 この場合、このプロジェクトのために読み込まれる VSPackage が Visual Basic ます。

   各プロジェクトは、ソリューション内の他のプロジェクトによって必要に応じてアクセスできるように、一意のプロジェクトインスタンス ID を永続化することができます。 理想的には、ソリューションとプロジェクトがソースコード管理下にある場合、プロジェクトへのパスは、ソリューションへのパスに対する相対パスである必要があります。 ソリューションが最初に読み込まれるときに、プロジェクトファイルをユーザーのコンピューター上に配置することはできません。 プロジェクトファイルをソリューションファイルと比較してサーバーに保存することで、プロジェクトファイルを検索してユーザーのコンピューターにコピーすることが比較的簡単になります。 その後、プロジェクトに必要な残りのファイルをコピーして読み込みます。

4. .Sln ファイルの project セクションに格納されている情報に基づいて、環境は各プロジェクトファイルを読み込みます。 プロジェクト自体は、プロジェクト階層の設定と入れ子になったプロジェクトの読み込みを行います。

5. .Sln ファイルのすべてのセクションが処理されると、ソリューションがソリューションエクスプローラーに表示され、ユーザーが変更できるようになります。

ソリューション内のプロジェクトを実装する VSPackage の読み込みに失敗した場合、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A> メソッドが呼び出され、ソリューション内の他のすべてのプロジェクトは、読み込み中に行われた変更を無視する可能性があります。 解析エラーが発生した場合、可能な限り多くの情報がソリューションファイルと共に保持され、環境によって、ソリューションが破損したことをユーザーに警告するダイアログボックスが表示されます。

ソリューションが保存または閉じられると、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A> メソッドが呼び出されて階層に渡され、.sln ファイルに入力する必要があるソリューションに変更が加えられたかどうかが確認されます。 でに渡される null 値は `QuerySaveSolutionProps` 、 <xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS> ソリューションの情報が永続化されていることを示します。 値が null でない場合、永続化された情報は、インターフェイスへのポインターによって決定される特定のプロジェクトに対して行われ <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。

保存する情報がある場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> メソッドへのポインターを使用してインターフェイスが呼び出され <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>次に、メソッドが環境によって呼び出され、インターフェイスから名前と値のペアを取得 `IPropertyBag` し、情報を .sln ファイルに書き込みます。

`SaveSolutionProps` および `WriteSolutionProps` オブジェクトは、 `IPropertyBag` すべての変更が .sln ファイルに入力されるまで、インターフェイスから保存される情報を取得するために、環境によって再帰的に呼び出されます。 このようにして、情報がソリューションと共に永続化され、次にソリューションが開いたときに使用できるようにすることができます。

読み込まれたすべての VSPackage を列挙して、.sln ファイルに保存するものがあるかどうかを確認します。 レジストリキーが照会されるのは読み込み時だけです。 環境は、読み込まれたすべてのパッケージを認識しています。これは、ソリューションが保存されるときにメモリ内にあるためです。

.Sln ファイルには、 `preSolution` セクションとセクションのエントリが含まれてい `postSolution` ます。 .Suo ファイルには、この情報が正しく読み込まれる必要があるため、類似するセクションはありません。 .Suo ファイルには、プライベートノートなどのユーザー固有のオプションが含まれています。このオプションは、共有したり、ソースコード管理下に配置するためのものではありません。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- [ソリューション ユーザー オプション (.Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md)
- [ソリューション](../../extensibility/internals/solutions-overview.md)
