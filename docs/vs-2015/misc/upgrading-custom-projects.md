---
title: カスタム プロジェクトのアップグレード |マイクロソフトドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- upgrading project systems
- projects [Visual Studio SDK], upgrading
- project system upgrades [Visual Studio]
ms.assetid: 262ada44-7689-44d8-bacb-9c6d33834d4e
caps.latest.revision: 11
manager: jillfra
ms.openlocfilehash: c91013e7d5650e82fd9e5f6e39e28c4609e4fbfe
ms.sourcegitcommit: c1339f64fbeee6f17bf80fedea81afc8dac40dc0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82037208"
---
# <a name="upgrading-custom-projects"></a>カスタム プロジェクトのアップグレード
プロジェクト ファイルに永続化されている情報を、ご使用の製品の異なる Visual Studio バージョン間で変更する場合、プロジェクト ファイルの旧バージョンから新しいバージョンへのアップグレードをサポートする必要があります。 **Visual Studio 変換ウィザード**に参加できるアップグレードをサポートするには、インターフェイスを実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>します。 このインターフェイスにはコピーのアップグレードに使用できる機能しか含まれていません。 プロジェクトのアップグレードは、ソリューションを開くことの一部として行われます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスはプロジェクト ファクトリによって実装されます。あるいは、少なくともプロジェクト ファクトリから取得できる必要があります。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> インターフェイスを使用する従来の機能は引き続きサポートされますが、概念上はプロジェクトを開くことの一部としてプロジェクト システムをアップグレードします。 したがって、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスが呼び出される、または実装される場合でも、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> インターフェイスが [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 環境によって呼び出されます。 この方法なら、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> を使用してプロジェクトのコピーとアップグレードの部分だけを実装できます。そして、残りの作業を <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> インターフェイスが一括 (通常は新しい場所) で実行するよう委任できます。  
  
 の実装例<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>については、「 [VSSDK サンプル](../misc/vssdk-samples.md)」を参照してください。  
  
 プロジェクトのアップグレードに伴って次の状況が発生します。  
  
- プロジェクトがサポートできるものよりもファイルの形式が新しい場合、そのことを示すエラーを返す必要があります。 これは、ご使用の製品の古いバージョン (Visual Studio .NET 2003 など) にバージョンを確認するためのコードがあることを前提としています。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> フラグが <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> メソッドで指定された場合、アップグレードはプロジェクトを開く前に一括アップグレードとして実装されます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> フラグが <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> メソッドで指定された場合、アップグレードはコピーのアップグレードとして実装されます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> フラグが <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 呼び出しで指定された場合、プロジェクトが開かれた後に一括アップグレードとしてプロジェクト ファイルをアップグレードするよう、環境からユーザーに対してダイアログが既に表示されています。 たとえば、ユーザーが古いバージョンのソリューションを開いた場合、環境からユーザーに対してアップグレードを促すダイアログが表示されます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> フラグが <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 呼び出しで指定されていない場合は、プロジェクト ファイルのアップグレードを促すダイアログをユーザーに対して表示する必要があります。  
  
     以下は、アップグレードのプロンプト メッセージの例です。  
  
     "プロジェクト '%1' は、古いバージョンの Visual Studio で作成されています。 このバージョンの Visual Studio でこのプロジェクトを開くと、Visual Studio の以前のバージョンでは開くことができなくなる場合があります。 続行してこのプロジェクトを開きますか?"  
  
### <a name="to-implement-ivsprojectupgradeviafactory"></a>IVsProjectUpgradeViaFactory を実装するには  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスのメソッド、特にプロジェクト ファクトリの実装で <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> メソッドを実装するか、その実装をプロジェクト ファクトリの実装から呼び出すことができるようにします。  
  
2. ソリューションを開くことの一部として一括アップグレードを行う場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> の実装の `VSPUVF_FLAGS` パラメーターとして、フラグ <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> を指定します。  
  
3. ソリューションを開くことの一部として一括アップグレードを行う場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> の実装の `VSPUVF_FLAGS` パラメーターとして、フラグ <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> を指定します。  
  
4. 手順 2 と手順 3 の両方で、実際のファイルのアップグレードの手順は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> を使用して、「`IVsProjectUpgade` の実装」のセクションの説明どおりに実装できます。あるいは、実際のファイル アップグレードを <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> に委任できます。  
  
5. Visual Studio 移行ウィザードを使用するユーザーに、アップグレードに関連したメッセージをポストするために、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> メソッドを使用します。  
  
6. <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileUpgrade> インターフェイスは、プロジェクト アップグレードの一部として実行する必要がある種類のファイル アップグレードを実装するために使用します。 このインターフェイスは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> から呼び出されることはありませんが、プロジェクト システムの一部であるファイルをアップグレードするメカニズムとして提供されます。しかし、主なプロジェクト システムはこれを直接に認識しない場合があります。 たとえば、コンパイラ関連のファイルとプロパティが、プロジェクト システムの残りを扱うのと同じ開発チームによって扱われない場合に、この状況が発生する可能性があります。  
  
## <a name="ivsprojectupgrade-implementation"></a>IVsProjectUpgrade の実装  
 プロジェクト システムが<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>実装されている場合は **、Visual Studio 変換ウィザード**に参加できません。 ただし、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスを実装しても、ファイルのアップグレードを <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> の実装に委任することはできます。  
  
#### <a name="to-implement-ivsprojectupgrade"></a>IVsProjectUpgrade を実装するには  
  
1. ユーザーがプロジェクトを開こうとするときには、プロジェクトが開かれてから、プロジェクト上で他の何らかのユーザー アクションが実行できるようになるまでの間に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> メソッドが環境によって呼び出されます。 既にユーザーに対してソリューションをアップグレードするよう促すダイアログが表示された場合、<xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> フラグが `grfUpgradeFlags` のパラメーターで渡されます。 **[既存プロジェクトの追加]** コマンドを使用するなどしてユーザーがプロジェクトを直接開いた場合<xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS>、フラグは渡されず、プロジェクトはユーザーにアップグレードを求めるメッセージを表示する必要があります。  
  
2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> の呼び出しに応じて、プロジェクトはプロジェクト ファイルがアップグレードされているかどうかを評価する必要があります。 プロジェクトがプロジェクトの種類を新しいバージョンにアップグレードする必要がない場合は、単に <xref:Microsoft.VisualStudio.VSConstants.S_OK> フラグを返すことができます。  
  
3. プロジェクトがプロジェクトの種類を新しいバージョンにアップグレードする必要がある場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> メソッドを呼び出し、`rgfQueryEdit` パラメーターに値 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> を渡して、プロジェクト ファイルを変更できるかどうかを確認する必要があります。 次いでプロジェクトは次の操作を行う必要があります。  
  
   - `pfEditCanceled` パラメーターで返される `VSQueryEditResult` 値が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> である場合、プロジェクト ファイルに書き込みができるので、アップグレードを続けることができます。  
  
   - `pfEditCanceled` パラメーターで返される `VSQueryEditResult` 値が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> であり、`VSQueryEditResult` 値に <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> のビットが設定されている場合、ユーザーがアクセス許可の問題を自分で解決する必要があるため、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> はエラーを返す必要があります。 次いでプロジェクトは次の操作を行う必要があります。  
  
        <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> を呼び出して、ユーザーにエラーを報告します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> に <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes> エラー コードを返します。  
  
   - `VSQueryEditResult` 値が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> で、`VSQueryEditResultFlags` 値に <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> ビットが設定されている場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>、...) を呼び出してプロジェクト ファイルをチェックアウトする必要があります。  
  
4. プロジェクト ファイルで <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> が呼び出されてファイルがチェックアウトされ、最新バージョンが取得されると、プロジェクトがアンロードされて再度読み込まれます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> メソッドは、プロジェクトの別のインスタンスが作成された後で再び呼び出されます。 この 2 つ目の呼び出しで、プロジェクト ファイルをディスクに書き込むことができるようになります。プロジェクトが、以前の形式でプロジェクト ファイルのコピーを保存してこれに拡張子 .OLD を付け、必要なアップグレードの変更を行い、新しい形式でプロジェクト ファイルを保存することをお勧めします。 アップグレード プロセスのいずれかの部分が失敗した場合は、先と同様、メソッドは <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes> を返して失敗したことを示す必要があります。 これにより、ソリューション エクスプローラーでプロジェクトがアンロードされます。  
  
    <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> メソッドの呼び出し (値 ReportOnly を指定) が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> および <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> フラグを返すケースで環境に発生するプロセス全体を理解することは重要です。  
  
5. ユーザーは、プロジェクト ファイルを開こうとします。  
  
6. 環境は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> の実装を呼び出します。  
  
7. <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> が `true` を返す場合、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> の実装を呼び出します。  
  
8. 環境は <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> の実装を呼び出してファイルを開き、プロジェクト オブジェクト (Project1 など) を初期化します。  
  
9. プロジェクト ファイルをアップグレードする必要があるかどうかを判断するために、環境は `IVsProjectUpgrade::UpgradeProject` の実装を呼び出します。  
  
10. <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> を呼び出し、値 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> を `rgfQueryEdit` のパラメーターに渡します。  
  
11. 環境は `VSQueryEditResult` に関して <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> を返し、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> ビットが `VSQueryEditResultFlags` に設定されます。  
  
12. <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> の実装が `IVsQueryEditQuerySave::QueryEditFiles` (<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>) を呼び出します。  
  
    この呼び出しによって、プロジェクト ファイルを再度読み込む必要が生じるだけでなく、プロジェクト ファイルの新しいコピーがチェックアウトされ、最新バージョンが取得される可能性もあります。 この時点で、次の 2 つのいずれかが行われます。  
  
- 独自のプロジェクトの再度読み込みを処理する場合、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> (VSITEMID_ROOT) の実装を呼び出します。 この呼び出しを受け取ったら、プロジェクトの最初のインスタンス (Project1) を再度読み込んで、プロジェクト ファイルのアップグレードを続けてください。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>) で `true` を返せば、環境は独自のプロジェクト再度読み込みが処理されることがわかります。  
  
- 独自のプロジェクト再度読み込みを処理しない場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>) で `false` を返してください。 この場合、(QEF_ForceEdit_NoPrompting <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>[QEF_ForceEdit_NoPrompting](/dotnet/api/microsoft.visualstudio.shell.interop.tagvsqueryeditflags) [、QEF_DisallowInMemoryEdits)](/dotnet/api/microsoft.visualstudio.shell.interop.tagvsqueryeditflags)が返される前に、環境はプロジェクトの新しいインスタンス(たとえば Project2 など)を次のように作成します。  
  
  1. 環境は、最初のプロジェクト オブジェクト (Project1) で <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.Close%2A> を呼び出し、このオブジェクトを非アクティブ状態にします。  
  
  2. 環境は、プロジェクトの 2 つ目のインスタンス (Project2) を作成するために、 `IVsProjectFactory::CreateProject` の実装を呼び出します。  
  
  3. 環境は、ファイルを開き、2 つ目のプロジェクト オブジェクト (Project2) を初期化するために、 `IPersistFileFormat::Load` の実装を呼び出します。  
  
  4. 環境は、プロジェクト オブジェクトをアップグレードする必要があるかどうかを判断するために、2 度目に `IVsProjectUpgrade::UpgradeProject` を呼び出します。 しかし、この呼び出しは、プロジェクトの新しい 2 番目のインスタンス (Project2) に対して行われます。 これは、ソリューションで開くプロジェクトです。  
  
      > [!NOTE]
      > 最初のプロジェクト (Project1) を非アクティブ状態にした場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> の実装への最初の呼び出しから <xref:Microsoft.VisualStudio.VSConstants.S_OK> を返す必要があります。 の実装については、[基本プロジェクト](https://msdn.microsoft.com/385fd2a3-d9f1-4808-87c2-a3f05a91fc36)を`IVsProjectUpgrade::UpgradeProject`参照してください。  
  
  5. <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> を呼び出し、値 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> を `rgfQueryEdit` のパラメーターに渡します。  
  
  6. 環境は <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> を返し、プロジェクト ファイルを書き込める状態になったので、アップグレードを続けることができます。  
  
  アップグレードに失敗した場合は、`IVsProjectUpgrade::UpgradeProject` から <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes> を返してください。 アップグレードの必要がない場合、またはアップグレードしないことにした場合は、操作なしとして `IVsProjectUpgrade::UpgradeProject` 呼び出しを処理します。 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes> を返すと、プレースホルダーのノードがプロジェクトのソリューションに追加されます。  
  
## <a name="see-also"></a>参照  
 [ビジュアル スタジオ変換ウィザード](https://msdn.microsoft.com/4acfd30e-c192-4184-a86f-2da5e4c3d83c)   
 [プロジェクト項目のアップグレード](../misc/upgrading-project-items.md)   
 [プロジェクト](../extensibility/internals/projects.md)