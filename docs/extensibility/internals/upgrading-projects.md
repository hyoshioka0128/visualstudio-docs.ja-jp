---
title: プロジェクトのアップグレード |Microsoft Docs
description: プロジェクトで upgrade support を実装するために Visual Studio SDK が提供するインターフェイスについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 5d42a912761f04fb122551dc14ec077f1869f6bf
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487583"
---
# <a name="upgrading-projects"></a>プロジェクトのアップグレード

あるバージョンの Visual Studio から次のバージョンにプロジェクトモデルを変更すると、新しいバージョンで実行できるように、プロジェクトとソリューションをアップグレードすることが必要になる場合があります。 には、 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 独自のプロジェクトで upgrade support を実装するために使用できるインターフェイスが用意されています。

## <a name="upgrade-strategies"></a>アップグレード戦略

アップグレードをサポートするには、プロジェクトシステムの実装で、アップグレード戦略を定義して実装する必要があります。 戦略を決定する際には、サイドバイサイド (SxS) バックアップ、コピーバックアップ、またはその両方をサポートすることを選択できます。

- SxS バックアップとは、プロジェクトでは、アップグレードが必要なファイルのみをコピーし、適切なファイル名サフィックスを追加することを意味します。たとえば、".old" のようになります。

- コピーバックアップとは、プロジェクトがすべてのプロジェクト項目をユーザー指定のバックアップの場所にコピーすることを意味します。 その後、元のプロジェクトの場所にある関連ファイルがアップグレードされます。

## <a name="how-upgrade-works"></a>アップグレードのしくみ

以前のバージョンの Visual Studio で作成されたソリューションを新しいバージョンで開くと、IDE はソリューションファイルをチェックして、アップグレードが必要かどうかを判断します。 アップグレードが必要な場合は、アップグレード **ウィザード** が自動的に起動して、アップグレードプロセスをユーザーに案内します。

ソリューションをアップグレードする必要がある場合は、各プロジェクトファクトリに対して、アップグレードの戦略についてクエリを行います。 この戦略では、プロジェクトファクトリがコピーバックアップと SxS バックアップのどちらをサポートするかを決定します。 この情報は **アップグレードウィザード** に送信され、バックアップに必要な情報が収集され、該当するオプションがユーザーに提示されます。

### <a name="multi-project-solutions"></a>複数のプロジェクトから成るソリューション

ソリューションに複数のプロジェクトが含まれており、アップグレード戦略が異なる場合 (たとえば、SxS バックアップのみをサポートする C++ プロジェクトや、コピーバックアップのみをサポートする Web プロジェクトの場合など)、プロジェクトファクトリはアップグレード戦略をネゴシエートする必要があります。

ソリューションは、の各プロジェクトファクトリに対してクエリを <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 行います。 次に、を呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly%2A> グローバルプロジェクトファイルのアップグレードが必要かどうかを確認し、サポートされているアップグレード方法を確認します。 次に、 **アップグレードウィザード** が呼び出されます。

ユーザーがウィザードを完了すると、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 各プロジェクトファクトリでが呼び出され、実際のアップグレードが実行されます。 バックアップを容易にするために、IVsProjectUpgradeViaFactory メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> アップグレードプロセスの詳細をログに記録するサービスを提供します。 このサービスをキャッシュすることはできません。

関連するすべてのグローバルファイルを更新した後、プロジェクトファクトリはプロジェクトのインスタンスを選択できます。 プロジェクトの実装では、をサポートする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A>次に、メソッドを呼び出して、関連するすべてのプロジェクト項目をアップグレードします。

> [!NOTE]
> メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> SVsUpgradeLogger サービスを提供しません。 このサービスは、を呼び出すことによって取得でき <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> ます。

## <a name="best-practices"></a>推奨する運用方法

サービスを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> ファイルを編集する前に編集できるかどうかを確認し、保存する前に保存しておくことができます。 これにより、バックアップとアップグレードの実装で、ソース管理下のプロジェクトファイル、十分なアクセス許可のないファイルなどを処理できます。

<xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger>アップグレードプロセスの成功または失敗に関する情報を提供するために、バックアップとアップグレードのすべてのフェーズでサービスを使用します。

プロジェクトのバックアップとアップグレードの詳細については、vsshell2 での IVsProjectUpgrade に関するコメントを参照してください。

## <a name="upgrading-custom-projects"></a><a name="upgrading-custom-projects"></a> カスタムプロジェクトのアップグレード

プロジェクト ファイルに永続化されている情報を、ご使用の製品の異なる Visual Studio バージョン間で変更する場合、プロジェクト ファイルの旧バージョンから新しいバージョンへのアップグレードをサポートする必要があります。 **Visual Studio 変換ウィザード** に参加できるようにするためのアップグレードをサポートするには、インターフェイスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> ます。 このインターフェイスにはコピーのアップグレードに使用できる機能しか含まれていません。 プロジェクトのアップグレードは、ソリューションを開くことの一部として行われます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスはプロジェクト ファクトリによって実装されます。あるいは、少なくともプロジェクト ファクトリから取得できる必要があります。

<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> インターフェイスを使用する従来の機能は引き続きサポートされますが、概念上はプロジェクトを開くことの一部としてプロジェクト システムをアップグレードします。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>このインターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスが呼び出されるか実装されている場合でも、Visual Studio 環境によって呼び出されます。 この方法なら、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> を使用してプロジェクトのコピーとアップグレードの部分だけを実装できます。そして、残りの作業を <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> インターフェイスが一括 (通常は新しい場所) で実行するよう委任できます。

の実装例につい <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> ては、「 [Vssdk のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)」を参照してください。

プロジェクトのアップグレードに伴って次の状況が発生します。

- プロジェクトがサポートできるものよりもファイルの形式が新しい場合、そのことを示すエラーを返す必要があります。 これは、古いバージョンの製品にバージョンを確認するコードが含まれていることを前提としています。

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

プロジェクトシステムがを実装している場合は <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 、 **Visual Studio 変換ウィザード** に参加できません。 ただし、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスを実装しても、ファイルのアップグレードを <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> の実装に委任することはできます。

#### <a name="to-implement-ivsprojectupgrade"></a>IVsProjectUpgrade を実装するには

1. ユーザーがプロジェクトを開こうとするときには、プロジェクトが開かれてから、プロジェクト上で他の何らかのユーザー アクションが実行できるようになるまでの間に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> メソッドが環境によって呼び出されます。 既にユーザーに対してソリューションをアップグレードするよう促すダイアログが表示された場合、<xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> フラグが `grfUpgradeFlags` のパラメーターで渡されます。 [ **既存プロジェクトの追加** ] コマンドを使用するなどして、ユーザーがプロジェクトを直接開いた場合、 <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> フラグは渡されず、プロジェクトはアップグレードするようにユーザーに要求する必要があります。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> の呼び出しに応じて、プロジェクトはプロジェクト ファイルがアップグレードされているかどうかを評価する必要があります。 プロジェクトがプロジェクトの種類を新しいバージョンにアップグレードする必要がない場合は、単に <xref:Microsoft.VisualStudio.VSConstants.S_OK> フラグを返すことができます。

3. プロジェクトがプロジェクトの種類を新しいバージョンにアップグレードする必要がある場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> メソッドを呼び出し、`rgfQueryEdit` パラメーターに値 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> を渡して、プロジェクト ファイルを変更できるかどうかを確認する必要があります。 次いでプロジェクトは次の操作を行う必要があります。

    - `pfEditCanceled` パラメーターで返される `VSQueryEditResult` 値が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditOK> である場合、プロジェクト ファイルに書き込みができるので、アップグレードを続けることができます。

    - `pfEditCanceled` パラメーターで返される `VSQueryEditResult` 値が <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> であり、`VSQueryEditResult` 値に <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyNotUnderScc> のビットが設定されている場合、ユーザーがアクセス許可の問題を自分で解決する必要があるため、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> はエラーを返す必要があります。 次いでプロジェクトは次の操作を行う必要があります。

         を呼び出してエラーをユーザーに報告 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> し、 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED> エラーコードをに返し <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> ます。

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

- 独自のプロジェクト再度読み込みを処理しない場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_HandlesOwnReload>) で `false` を返してください。 この場合、(QEF_ForceEdit_NoPrompting、QEF_DisallowInMemoryEdits) が返される前に、次のように、環境によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> プロジェクトの新しいインスタンス (Project2 など) が作成されます。

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

を実装していないプロジェクトシステム内の項目を追加または管理する場合は、プロジェクトのアップグレードプロセスに参加する必要があります。 Crystal Reports は、プロジェクトシステムに追加できるアイテムの例です。

通常、プロジェクト項目の実装者は、既に完全にインスタンス化され、アップグレードされたプロジェクトを活用する必要があります。これは、プロジェクトが参照している内容と、アップグレードを決定するためにどのようなプロジェクトプロパティがあるかを把握する必要があるためです。

### <a name="to-get-the-project-upgrade-notification"></a>プロジェクトのアップグレード通知を取得するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80.SolutionOrProjectUpgrading>プロジェクト項目の実装でフラグ (vsshell80 で定義) を設定します。 これにより、Visual Studio シェルによってプロジェクトシステムがアップグレード中であると判断されたときに、プロジェクト項目 VSPackage が自動読み込みされます。

2. メソッドを使用してインターフェイスをアドバイスし <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution2.AdviseSolutionEvents%2A> ます。

3. この <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> インターフェイスは、プロジェクトシステムの実装がアップグレード操作を完了し、アップグレードされた新しいプロジェクトが作成された後に発生します。 シナリオによっては、、、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> またはメソッドの後にインターフェイスが起動され <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A> ます。

### <a name="to-upgrade-the-project-item-files"></a>プロジェクト項目ファイルをアップグレードするには

1. プロジェクト項目の実装では、ファイルのバックアッププロセスを慎重に管理する必要があります。 これは、並列バックアップの場合に特に当てはまります。この場合、 `fUpgradeFlag` <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP> バックアップされたファイルは、".old" として指定されたファイルに従って配置されます。 プロジェクトをアップグレードしたときのシステム時刻より古いバックアップファイルは、古いものとして指定できます。 また、これを回避する特定の手順を実行しない限り、上書きされる可能性があります。

2. プロジェクト項目がプロジェクトのアップグレードの通知を受け取ると、 **Visual Studio 変換ウィザード** が引き続き表示されます。 したがって、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> ウィザードの UI にアップグレードメッセージを提供するには、インターフェイスのメソッドを使用する必要があります。

## <a name="see-also"></a>こちらもご覧ください

- [プロジェクト](../../extensibility/internals/projects.md)
