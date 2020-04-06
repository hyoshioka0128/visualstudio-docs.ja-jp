---
title: プロジェクトのアップグレード |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- upgrading VSPackages
- upgrading applications, strategies
- VSPackages, upgrade support
ms.assetid: e01cb44a-8105-4cf4-8223-dfae65f8597a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a99207fc14cf9f462bc1abc88d6fed166ea6523f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704267"
---
# <a name="upgrading-projects"></a>プロジェクトのアップグレード

Visual Studio のバージョンから次のバージョンへのプロジェクト モデルの変更では、新しいバージョンで実行できるように、プロジェクトとソリューションをアップグレードする必要があります。 には[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]、独自のプロジェクトでアップグレード サポートを実装するために使用できるインターフェイスが用意されています。

## <a name="upgrade-strategies"></a>アップグレード戦略

アップグレードをサポートするには、プロジェクト システムの実装でアップグレード戦略を定義し、実装する必要があります。 戦略を決定する際には、サイド バイ サイド (SxS) バックアップ、コピー バックアップ、またはその両方をサポートすることを選択できます。

- SxS バックアップとは、プロジェクトが適切なファイル名サフィックス (例: ".old" など) を追加して、その場でアップグレードする必要があるファイルのみをコピーすることを意味します。

- コピー バックアップとは、プロジェクトがすべてのプロジェクト項目をユーザー指定のバックアップ場所にコピーすることを意味します。 その後、元のプロジェクトの場所にある関連ファイルがアップグレードされます。

## <a name="how-upgrade-works"></a>アップグレードのしくみ

以前のバージョンの Visual Studio で作成されたソリューションを新しいバージョンで開くと、IDE はソリューション ファイルをチェックして、アップグレードが必要かどうかを判断します。 アップグレードが必要な場合は、**アップグレード ウィザード**が自動的に起動され、アップグレード プロセスが実行されます。

ソリューションは、アップグレードが必要な場合、各プロジェクト ファクトリにアップグレード戦略を照会します。 この方針は、プロジェクトファクトリがコピーバックアップまたはSxSバックアップをサポートしているかどうかを決定します。 情報は **、バックアップ**に必要な情報を収集し、該当するオプションをユーザーに提示するアップグレード ウィザード に送信されます。

### <a name="multi-project-solutions"></a>マルチプロジェクトソリューション

ソリューションに複数のプロジェクトが含まれ、アップグレード方法が異なる場合 (SxS バックアップのみをサポートする C++ プロジェクトとコピー バックアップのみをサポートする Web プロジェクトの場合など)、プロジェクト ファクトリはアップグレード戦略をネゴシエートする必要があります。

ソリューションは、各プロジェクト ファクトリに<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>対して を照会します。 次に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly%2A>グローバル プロジェクト ファイルのアップグレードが必要かどうかを確認し、サポートされているアップグレード方法を決定する呼び出しを行います。 **アップグレード ウィザード**が起動されます。

ユーザーがウィザードを完了すると、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A>各プロジェクト ファクトリで実際のアップグレードを実行するように呼び出されます。 バックアップを容易にするために、IVsProjectUpgradeViaFactory メソッド<xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger>は、アップグレード プロセスの詳細をログに記録するサービスを提供します。 このサービスはキャッシュできません。

関連するすべてのグローバル ファイルを更新した後、各プロジェクト ファクトリはプロジェクトのインスタンス化を選択できます。 プロジェクトの実装では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>をサポートする必要があります。 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A>メソッドは、関連するすべてのプロジェクト項目をアップグレードするために呼び出されます。

> [!NOTE]
> この<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A>メソッドは、SVsUpgradeLogger サービスを提供しません。 このサービスは、 を呼<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>び出すことによって取得できます。

## <a name="best-practices"></a>ベスト プラクティス

このサービス<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>を使用して、編集前にファイルを編集できるかどうか、および保存前に保存できるかどうかを確認します。 これにより、バックアップおよびアップグレードの実装で、ソース管理下のプロジェクト ファイルや、アクセス許可が不十分なファイルなどを処理できます。

アップグレード<xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger>プロセスの成功または失敗に関する情報を提供するには、バックアップとアップグレードのすべてのフェーズでサービスを使用します。

プロジェクトのバックアップとアップグレードの詳細については、vsshell2.idl の IVsProjectUpgrade のコメントを参照してください。

## <a name="upgrading-custom-projects"></a><a name="upgrading-custom-projects"></a>カスタム プロジェクトのアップグレード

プロジェクト ファイルに永続化されている情報を、ご使用の製品の異なる Visual Studio バージョン間で変更する場合、プロジェクト ファイルの旧バージョンから新しいバージョンへのアップグレードをサポートする必要があります。 **Visual Studio 変換ウィザード**に参加できるアップグレードをサポートするには、インターフェイスを実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>します。 このインターフェイスにはコピーのアップグレードに使用できる機能しか含まれていません。 プロジェクトのアップグレードは、ソリューションを開くことの一部として行われます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスはプロジェクト ファクトリによって実装されます。あるいは、少なくともプロジェクト ファクトリから取得できる必要があります。

<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> インターフェイスを使用する従来の機能は引き続きサポートされますが、概念上はプロジェクトを開くことの一部としてプロジェクト システムをアップグレードします。 したがって<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>、インターフェイスは、呼び出された場合や実装されている<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>場合でも、Visual Studio 環境によって呼び出されます。 この方法なら、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> を使用してプロジェクトのコピーとアップグレードの部分だけを実装できます。そして、残りの作業を <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> インターフェイスが一括 (通常は新しい場所) で実行するよう委任できます。

の実装例<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>については、「 [VSSDK サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)」を参照してください。

プロジェクトのアップグレードに伴って次の状況が発生します。

- プロジェクトがサポートできるものよりもファイルの形式が新しい場合、そのことを示すエラーを返す必要があります。 この場合、古いバージョンの製品には、バージョンを確認するコードが含まれていることを前提としています。

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP> フラグが <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> メソッドで指定された場合、アップグレードはプロジェクトを開く前に一括アップグレードとして実装されます。

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_COPYBACKUP> フラグが <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> メソッドで指定された場合、アップグレードはコピーのアップグレードとして実装されます。

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> フラグが <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 呼び出しで指定された場合、プロジェクトが開かれた後に一括アップグレードとしてプロジェクト ファイルをアップグレードするよう、環境からユーザーに対してダイアログが既に表示されています。 たとえば、ユーザーが古いバージョンのソリューションを開いた場合、環境からユーザーに対してアップグレードを促すダイアログが表示されます。

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> フラグが <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 呼び出しで指定されていない場合は、プロジェクト ファイルのアップグレードを促すダイアログをユーザーに対して表示する必要があります。

     以下は、アップグレードのプロンプト メッセージの例です。

     "プロジェクト '%1' は、古いバージョンの Visual Studio で作成されています。 このバージョンの Visual Studio でこのプロジェクトを開くと、Visual Studio の以前のバージョンでは開くことができなくなる場合があります。 続行してこのプロジェクトを開きますか?"

### <a name="to-implement-ivsprojectupgradeviafactory"></a>IVsProjectUpgradeViaFactory を実装するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスのメソッド、特にプロジェクト ファクトリの実装で <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> メソッドを実装するか、その実装をプロジェクト ファクトリの実装から呼び出すことができるようにします。

2. ソリューションを開くことの一部として一括アップグレードを行う場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> の実装の `VSPUVF_FLAGS` パラメーターとして、フラグ <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP> を指定します。

3. ソリューションを開くことの一部として一括アップグレードを行う場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> の実装の `VSPUVF_FLAGS` パラメーターとして、フラグ <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_COPYBACKUP> を指定します。

4. 手順 2 と手順 3 の両方で、実際のファイルのアップグレードの手順は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> を使用して、「`IVsProjectUpgade` の実装」のセクションの説明どおりに実装できます。あるいは、実際のファイル アップグレードを <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> に委任できます。

5. Visual Studio 移行ウィザードを使用するユーザーに、アップグレードに関連したメッセージをポストするために、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> メソッドを使用します。

6. <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileUpgrade> インターフェイスは、プロジェクト アップグレードの一部として実行する必要がある種類のファイル アップグレードを実装するために使用します。 このインターフェイスは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> から呼び出されることはありませんが、プロジェクト システムの一部であるファイルをアップグレードするメカニズムとして提供されます。しかし、主なプロジェクト システムはこれを直接に認識しない場合があります。 たとえば、コンパイラ関連のファイルとプロパティが、プロジェクト システムの残りを扱うのと同じ開発チームによって扱われない場合に、この状況が発生する可能性があります。

### <a name="ivsprojectupgrade-implementation"></a>IVsProjectUpgrade の実装

プロジェクト システムが<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>実装されている場合は **、Visual Studio 変換ウィザード**に参加できません。 ただし、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスを実装しても、ファイルのアップグレードを <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> の実装に委任することはできます。

#### <a name="to-implement-ivsprojectupgrade"></a>IVsProjectUpgrade を実装するには

1. ユーザーがプロジェクトを開こうとするときには、プロジェクトが開かれてから、プロジェクト上で他の何らかのユーザー アクションが実行できるようになるまでの間に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> メソッドが環境によって呼び出されます。 既にユーザーに対してソリューションをアップグレードするよう促すダイアログが表示された場合、<xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> フラグが `grfUpgradeFlags` のパラメーターで渡されます。 **[既存プロジェクトの追加]** コマンドを使用するなどしてユーザーがプロジェクトを直接開いた場合<xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE>、フラグは渡されず、プロジェクトはユーザーにアップグレードを求めるメッセージを表示する必要があります。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> の呼び出しに応じて、プロジェクトはプロジェクト ファイルがアップグレードされているかどうかを評価する必要があります。 プロジェクトがプロジェクトの種類を新しいバージョンにアップグレードする必要がない場合は、単に <xref:Microsoft.VisualStudio.VSConstants.S_OK> フラグを返すことができます。

3. プロジェクトがプロジェクトの種類を新しいバージョンにアップグレードする必要がある場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> メソッドを呼び出し、`rgfQueryEdit` パラメーターに値 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> を渡して、プロジェクト ファイルを変更できるかどうかを確認する必要があります。 次いでプロジェクトは次の操作を行う必要があります。

    - `pfEditCanceled` パラメーターで返される `VSQueryEditResult` 値が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditOK> である場合、プロジェクト ファイルに書き込みができるので、アップグレードを続けることができます。

    - `pfEditCanceled` パラメーターで返される `VSQueryEditResult` 値が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> であり、`VSQueryEditResult` 値に <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyNotUnderScc> のビットが設定されている場合、ユーザーがアクセス許可の問題を自分で解決する必要があるため、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> はエラーを返す必要があります。 次いでプロジェクトは次の操作を行う必要があります。

         ユーザーに対して呼び出し<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>を行って<xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED>エラーを報告<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>し、エラー コードを に返します。

    - `VSQueryEditResult` 値が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> で、`VSQueryEditResultFlags` 値に <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyUnderScc> ビットが設定されている場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ForceEdit_NoPrompting>、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_DisallowInMemoryEdits>、...) を呼び出してプロジェクト ファイルをチェックアウトする必要があります。

4. プロジェクト ファイルで <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> が呼び出されてファイルがチェックアウトされ、最新バージョンが取得されると、プロジェクトがアンロードされて再度読み込まれます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> メソッドは、プロジェクトの別のインスタンスが作成された後で再び呼び出されます。 この 2 つ目の呼び出しで、プロジェクト ファイルをディスクに書き込むことができるようになります。プロジェクトが、以前の形式でプロジェクト ファイルのコピーを保存してこれに拡張子 .OLD を付け、必要なアップグレードの変更を行い、新しい形式でプロジェクト ファイルを保存することをお勧めします。 アップグレード プロセスのいずれかの部分が失敗した場合は、先と同様、メソッドは <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED> を返して失敗したことを示す必要があります。 これにより、ソリューション エクスプローラーでプロジェクトがアンロードされます。

     <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> メソッドの呼び出し (値 ReportOnly を指定) が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> および <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyUnderScc> フラグを返すケースで環境に発生するプロセス全体を理解することは重要です。

5. ユーザーは、プロジェクト ファイルを開こうとします。

6. 環境は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> の実装を呼び出します。

7. <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> が `true` を返す場合、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> の実装を呼び出します。

8. 環境は <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> の実装を呼び出してファイルを開き、プロジェクト オブジェクト (Project1 など) を初期化します。

9. プロジェクト ファイルをアップグレードする必要があるかどうかを判断するために、環境は `IVsProjectUpgrade::UpgradeProject` の実装を呼び出します。

10. <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> を呼び出し、値 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ReportOnly> を `rgfQueryEdit` のパラメーターに渡します。

11. 環境は `VSQueryEditResult` に関して <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> を返し、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyUnderScc> ビットが `VSQueryEditResultFlags` に設定されます。

12. <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> の実装が `IVsQueryEditQuerySave::QueryEditFiles` (<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ForceEdit_NoPrompting>、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_DisallowInMemoryEdits>) を呼び出します。

この呼び出しによって、プロジェクト ファイルを再度読み込む必要が生じるだけでなく、プロジェクト ファイルの新しいコピーがチェックアウトされ、最新バージョンが取得される可能性もあります。 この時点で、次の 2 つのいずれかが行われます。

- 独自のプロジェクトの再度読み込みを処理する場合、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> (VSITEMID_ROOT) の実装を呼び出します。 この呼び出しを受け取ったら、プロジェクトの最初のインスタンス (Project1) を再度読み込んで、プロジェクト ファイルのアップグレードを続けてください。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_HandlesOwnReload>) で `true` を返せば、環境は独自のプロジェクト再度読み込みが処理されることがわかります。

- 独自のプロジェクト再度読み込みを処理しない場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_HandlesOwnReload>) で `false` を返してください。 この場合、(QEF_ForceEdit_NoPrompting、QEF_DisallowInMemoryEdits)が返される前<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>に、環境はプロジェクトの新しいインスタンスを作成します(たとえば Project2)。

    1. 環境は、最初のプロジェクト オブジェクト (Project1) で <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.Close%2A> を呼び出し、このオブジェクトを非アクティブ状態にします。

    2. 環境は、プロジェクトの 2 つ目のインスタンス (Project2) を作成するために、 `IVsProjectFactory::CreateProject` の実装を呼び出します。

    3. 環境は、ファイルを開き、2 つ目のプロジェクト オブジェクト (Project2) を初期化するために、 `IPersistFileFormat::Load` の実装を呼び出します。

    4. 環境は、プロジェクト オブジェクトをアップグレードする必要があるかどうかを判断するために、2 度目に `IVsProjectUpgrade::UpgradeProject` を呼び出します。 しかし、この呼び出しは、プロジェクトの新しい 2 番目のインスタンス (Project2) に対して行われます。 これは、ソリューションで開くプロジェクトです。

        > [!NOTE]
        > 最初のプロジェクト (Project1) を非アクティブ状態にした場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> の実装への最初の呼び出しから <xref:Microsoft.VisualStudio.VSConstants.S_OK> を返す必要があります。

    5. <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> を呼び出し、値 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ReportOnly> を `rgfQueryEdit` のパラメーターに渡します。

    6. 環境は <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditOK> を返し、プロジェクト ファイルを書き込める状態になったので、アップグレードを続けることができます。

アップグレードに失敗した場合は、`IVsProjectUpgrade::UpgradeProject` から <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED> を返してください。 アップグレードの必要がない場合、またはアップグレードしないことにした場合は、操作なしとして `IVsProjectUpgrade::UpgradeProject` 呼び出しを処理します。 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED> を返すと、プレースホルダーのノードがプロジェクトのソリューションに追加されます。

## <a name="upgrading-project-items"></a>プロジェクト項目のアップグレード

実装していないプロジェクト システム内で項目を追加または管理する場合は、プロジェクトのアップグレード プロセスに参加する必要があります。 クリスタル レポートは、プロジェクト システムに追加できる項目の例です。

通常、プロジェクト項目の実装者は、プロジェクト参照が何であるか、およびアップグレードの決定を行うために他にどのようなプロジェクト プロパティがあるかを知る必要があるため、既に完全にインスタンス化され、アップグレードされたプロジェクトを活用する必要があります。

### <a name="to-get-the-project-upgrade-notification"></a>プロジェクトのアップグレード通知を取得するには

1. プロジェクト項目<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80.SolutionOrProjectUpgrading>の実装でフラグ (vsshell80.idl で定義) を設定します。 これにより、プロジェクト の項目 VSPackage は、Visual Studio シェルがプロジェクト システムがアップグレードの処理中であると判断したときに自動的に読み込まれます。

2. メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade>介してインターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution2.AdviseSolutionEvents%2A>をアドバイスします。

3. この<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade>インターフェイスは、プロジェクト システムの実装がアップグレード操作を完了し、新しいアップグレードされたプロジェクトが作成された後に起動されます。 シナリオに<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade>応じて、インターフェイスは<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A>、 、または メソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>の後に<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A>起動されます。

### <a name="to-upgrade-the-project-item-files"></a>プロジェクト項目ファイルをアップグレードするには

1. プロジェクト項目の実装でファイルバックアッププロセスを慎重に管理する必要があります。 これは特に、`fUpgradeFlag`<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A>メソッドのパラメータが<xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP>に設定されているサイド バイ サイド バックアップに当てはまります。 プロジェクトがアップグレードされたシステム時刻より古いバックアップ ファイルを古いものとして指定できます。 さらに、これを防ぐために特定の手順を実行しない限り、上書きされる可能性があります。

2. プロジェクト項目がプロジェクトのアップグレードの通知を受け取った時点で **、Visual Studio 変換ウィザード**が表示されます。 したがって、ウィザード UI にアップグレード<xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger>メッセージを提供するインターフェイスのメソッドを使用する必要があります。

## <a name="see-also"></a>関連項目

- [プロジェクト](../../extensibility/internals/projects.md)
