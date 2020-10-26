---
title: プロジェクト構成オブジェクト |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80706656"
---
# <a name="project-configuration-object"></a>プロジェクト構成オブジェクト
プロジェクト構成オブジェクトは、UI への構成情報の表示を管理します。

 ![Visual Studio プロジェクトの構成](../../extensibility/internals/media/vsprojectcfg.gif "vsProjectCfg") プロジェクト構成のプロパティページ

 プロジェクト構成プロバイダーは、プロジェクト構成を管理します。 環境およびその他のパッケージは、プロジェクトの構成に関する情報にアクセスして取得するために、プロジェクト構成プロバイダーオブジェクトにアタッチされているインターフェイスを呼び出します。

> [!NOTE]
> プログラムによってソリューション構成ファイルを作成または編集することはできません。 `DTE.SolutionBuilder` を使用する必要があります。 詳細については、「 [ソリューションの構成](../../extensibility/internals/solution-configuration.md) 」を参照してください。

 構成 UI で使用する表示名を発行するには、プロジェクトでを実装する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A> ます。 環境はを呼び出します <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> 。これは、 `IVsCfg` 環境の UI に表示される構成およびプラットフォームの情報の表示名を取得するために使用できるポインターのリストを返します。 アクティブな構成とプラットフォームは、アクティブなソリューション構成に格納されているプロジェクトの構成によって決まります。 メソッドを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager.FindActiveProjectCfg%2A> 、アクティブなプロジェクト構成を取得できます。

 オブジェクトをオブジェクトと共にオブジェクトに実装して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> 正規の <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper> `IVsProjectCfg2` プロジェクト構成名に基づいてオブジェクトを取得できるようにすることもできます。

 プロジェクト構成へのアクセス権を持つ環境や他のプロジェクトを提供するもう1つの方法は、プロジェクトで `IVsCfgProvider2::GetCfgs` 1 つ以上の構成オブジェクトを返すメソッドの実装を提供することです。 プロジェクトは <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> 、を継承するを実装し `IVsProjectCfg` て、 `IVsCfg` 構成固有の情報を提供することもできます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> では、プロジェクト構成を追加、削除、および名前変更するためのプラットフォームと機能がサポートされています。

> [!NOTE]
> Visual Studio は2つの構成の種類に制限されなくなったため、構成を処理するコードは、構成の数についての前提を考慮して記述する必要はありません。また、構成を1つだけ持つプロジェクトは、必ずデバッグまたはリテールのいずれかであるという前提で記述する必要もありません。 これにより、との使用が <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A> 廃止されます。

 `QueryInterface`から返されたオブジェクトに対してを呼び出すと、が取得され `IVsGetCfgProvider::GetCfgProvider` `IVsCfgProvider2` ます。 `IVsGetCfgProvider`プロジェクトオブジェクトでを呼び出すことによってが見つからない場合は、に対して返された `QueryInterface` `IVsProject3` `QueryInterface` オブジェクトの階層ルートブラウザーオブジェクトでを呼び出す `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)` か、に対して返された構成プロバイダーへのポインターを介して、構成プロバイダーオブジェクトにアクセスでき `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)` ます。

 `IVsProjectCfg2` は、主にビルド、デバッグ、および配置管理オブジェクトへのアクセスを提供し、プロジェクトが自由に出力をグループ化できるようにします。 とのメソッドを使用すると、を実装して `IVsProjectCfg` `IVsProjectCfg2` <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> ビルドプロセスを管理でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> ます。また、構成の出力グループへのポインターを実装することもできます。

 グループ内に含まれている出力の数が構成ごとに異なる場合でも、プロジェクトはサポートする構成ごとに同じ数のグループを返す必要があります。 また、グループは、プロジェクト内の構成から構成まで、同じ識別子情報 (正規名、表示名、およびグループ情報) を持っている必要があります。 詳細については、「 [出力のプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)」を参照してください。

 デバッグを有効にするには、構成でを実装する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> ます。 `IVsDebuggableProjectCfg` は、プロジェクトによって実装される省略可能なインターフェイスであり、デバッガーが構成を起動し、とを使用して構成オブジェクトに実装されるようにし `IVsCfg` `IVsProjectCfg` ます。 ユーザーが F5 キーを押してデバッガーを起動することにした場合、環境はこれを呼び出します。

 `ISpecifyPropertyPages` と `IDispatch` は、構成に依存する情報を取得してユーザーに表示するために、プロパティページと組み合わせて使用されます。 詳細については、「 [プロパティページ](../../extensibility/internals/property-pages.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)
- [[プロパティ ページ]](../../extensibility/internals/property-pages.md)
- [ソリューション構成](../../extensibility/internals/solution-configuration.md)
