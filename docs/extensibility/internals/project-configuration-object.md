---
title: プロジェクト構成オブジェクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, object
- objects, project configuration
ms.assetid: 877756c9-4261-43d9-9f32-51bf06b4219f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 001509b56e3bac6a8fd585eb0efe0bd57018acea
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706656"
---
# <a name="project-configuration-object"></a>プロジェクト構成オブジェクト
プロジェクト構成オブジェクトは、UI に対する構成情報の表示を管理します。

 ![ビジュアル スタジオ プロジェクトの構成](../../extensibility/internals/media/vsprojectcfg.gif "を行う")プロジェクト構成のプロパティ ページ

 プロジェクト構成プロバイダーは、プロジェクト構成を管理します。 環境およびその他のパッケージは、プロジェクトの構成に関する情報にアクセスして取得するには、プロジェクト構成プロバイダー オブジェクトにアタッチされたインターフェイスを呼び出します。

> [!NOTE]
> ソリューション構成ファイルをプログラムで作成または編集することはできません。 `DTE.SolutionBuilder` を使用する必要があります。 詳細については、「[ソリューション構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

 構成 UI で使用する表示名を公開するには、プロジェクトで を実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A>する必要があります。 環境呼び<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>出しは、環境の`IVsCfg`UI に表示される構成およびプラットフォーム情報の表示名を取得するために使用できるポインターのリストを返します。 アクティブな構成とプラットフォームは、アクティブなソリューション構成に格納されているプロジェクトの構成によって決まります。 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager.FindActiveProjectCfg%2A>メソッドを使用して、アクティブなプロジェクト構成を取得できます。

 オブジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>にオブジェクトを実装して、正規の<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper>プロジェクト構成名に基づいてオブジェクトを`IVsProjectCfg2`取得できるように、オブジェクトを任意で実装できます。

 環境や他のプロジェクトにプロジェクト構成へのアクセスを提供するもう 1 つの方法は、1`IVsCfgProvider2::GetCfgs`つ以上の構成オブジェクトを返すメソッドの実装をプロジェクトに提供することです。 プロジェクトは、 から<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>継承`IVsProjectCfg`し、それによって`IVsCfg`から継承する を実装して、構成固有の情報を提供することもできます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>は、プラットフォーム、およびプロジェクト構成の追加、削除、および名前変更の機能をサポートしています。

> [!NOTE]
> Visual Studio は 2 つの構成の種類に制限されなくなったため、構成を処理するコードは構成の数に関する前提で記述しないでください。 これにより、使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A>され、<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A>時代遅れになります。

 から返されたオブジェクトを呼び出`IVsCfgProvider2`す`QueryInterface``IVsGetCfgProvider::GetCfgProvider` `IVsProject3`プロジェクト`IVsGetCfgProvider`オブジェクトを呼び`QueryInterface`出して見つからない場合は、 に返されたオブジェクトの階層`QueryInterface`ルート ブラウザ オブジェクトを呼び出すか`IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)`、または に返された構成プロバイダーへのポインタを通`IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)`じて、構成プロバイダ オブジェクトにアクセスできます。

 `IVsProjectCfg2`主に、ビルド、デバッグ、および配置管理オブジェクトへのアクセスを提供し、プロジェクトが出力をグループ化する自由を可能にします。 ビルド プロセス`IVsProjectCfg`を`IVsProjectCfg2`管理するために実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>するために使用できるメソッドと<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup>、構成の出力グループのポインター。

 プロジェクトは、グループ内に含まれる出力の数が構成によって異なる場合でも、サポートする構成ごとに同じ数のグループを返す必要があります。 また、グループは、プロジェクト内の構成から構成まで、同じ識別子情報 (正規名、表示名、およびグループ情報) を持つ必要があります。 詳細については、「[出力用のプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)」を参照してください。

 デバッグを有効にするには、構成で<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>を実装する必要があります。 `IVsDebuggableProjectCfg`は、プロジェクトによって実装されたオプションのインターフェイスで、デバッガが構成を起動できるようにし、 と`IVsCfg``IVsProjectCfg`の構成オブジェクトに実装されます。 ユーザーが F5 キーを押してデバッガーを起動することを選択すると、環境が呼び出されます。

 `ISpecifyPropertyPages`を`IDispatch`プロパティ ページと組み合わせて使用し、構成に依存する情報を取得してユーザーに表示します。 詳細については、「[プロパティ ページ](../../extensibility/internals/property-pages.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)
- [プロパティ ページ](../../extensibility/internals/property-pages.md)
- [ソリューション構成](../../extensibility/internals/solution-configuration.md)
