---
title: ソリューション (..Sln) File |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- sln files, VSPackages
- solutions, .sln files
- .sln files, VSPackages
ms.assetid: 7d7ef539-2e4b-4637-b853-8ec7626609df
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d9e045ab707620fe985e34174238081f6168e5af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68154965"
---
# <a name="solution-sln-file"></a>ソリューション (.Sln) ファイル
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソリューションは、Visual Studio でプロジェクトを整理するための構造です。 このソリューションでは、.sln (テキストベース、共有) ファイルと .suo (バイナリ、ユーザー固有のソリューションオプション) ファイル内のプロジェクトの状態情報を保持します。 .Suo ファイルの詳細については、「 [ソリューションユーザーオプション (」を参照してください。.Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md)。  
  
 VSPackage が .sln ファイルで参照された結果として読み込まれた場合、環境はを呼び出して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> .sln ファイルを読み取ります。  
  
 .Sln ファイルには、永続化されたデータの名前と値のパラメーターの検索と読み込みに使用するテキストベースの情報が含まれています。この情報は、Vspackage が参照するプロジェクトです。 ユーザーがソリューションを開くと、環境は .sln ファイル内の、、およびの情報を循環して、ソリューション、ソリューション `preSolution` `Project` 内の `postSolution` プロジェクト、およびソリューションに関連付けられている保存された情報を読み込みます。  
  
 各プロジェクトのファイルには、そのプロジェクトの項目を階層に設定するために環境によって読み取られた追加情報が含まれています。 階層データの永続化は、プロジェクトによって制御されます。通常、データは .sln ファイルに格納されませんが、.sln ファイルにプロジェクト情報を意図的に書き込むことができます。 永続化に関する詳細については、「 [プロジェクトの永続](../../extensibility/internals/project-persistence.md) 化」と「 [プロジェクト項目を開いて保存](../../extensibility/internals/opening-and-saving-project-items.md)する」を参照してください。  
  
## <a name="solution-file-contents"></a>ソリューションファイルの内容  
 .Sln ファイルは、次のコードに示すように、いくつかのセクションで構成されています。  
  
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
  
1. 環境は、.sln ファイルのグローバルセクションを読み取り、とマークされたすべてのセクションを処理し `preSolution` ます。 この場合、次のようなステートメントが1つあります。  
  
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
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>   
 [ソリューションユーザーオプション (..Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md)   
 [ソリューション](../../extensibility/internals/solutions-overview.md)
