---
title: MSBuild の使用 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f961249ff584f7767dc2505bb20b1fb0961b7dd3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80704286"
---
# <a name="using-msbuild"></a>MSBuild の使用
MSBuild には、ビルドするプロジェクト項目、ビルドタスク、およびビルド構成を完全に記述したプロジェクトファイルを作成するための、適切に定義された拡張可能な XML 形式が用意されています。

## <a name="general-msbuild-considerations"></a>MSBuild に関する一般的な考慮事項
 MSBuild プロジェクトファイル (.csproj、.vbproj ファイルなど) に [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] は、 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ビルド時に使用されるデータが含まれますが、デザイン時に使用されるデータを含めることもできます。 ビルド時のデータは、 [Item 要素 (msbuild)](../../msbuild/item-element-msbuild.md) や [Property 要素 (msbuild)](../../msbuild/property-element-msbuild.md)などの msbuild プリミティブを使用して格納されます。 デザイン時データは、プロジェクトの種類および関連するプロジェクトのサブタイプに固有のデータであり、そのために予約された自由形式の XML に格納されます。

 MSBuild には構成オブジェクトのネイティブサポートはありませんが、構成固有のデータを指定するための条件付き属性が用意されています。 次に例を示します。

```xml
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>
```

 条件付き属性の詳細については、「 [条件付き構成体](../../msbuild/msbuild-conditional-constructs.md)」を参照してください。

### <a name="extending-msbuild-for-your-project-type"></a>プロジェクトの種類の MSBuild の拡張
 MSBuild のインターフェイスと Api は、将来のバージョンので変更される可能性が [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] あります。 そのため、managed package framework (MPF) クラスを使用することをお勧めします。これは、変更によってシールドが提供されるためです。

 プロジェクト用の Managed Package Framework (MPFProj) には、新しいプロジェクトシステムを作成および管理するためのヘルパークラスが用意されています。 ソースコードとコンパイルの手順については、「 [MPF For Projects-Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10)」を参照してください。

 プロジェクト固有の MPF クラスは次のとおりです。

|クラス|実装|
|-----------|--------------------|
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|

 `Microsoft.VisualStudio.Package.ProjectElement` クラスは、MSBuild 項目のラッパーです。

#### <a name="single-file-generators-vs-msbuild-tasks"></a>単一ファイルジェネレーターと MSBuild タスク
 1つのファイルジェネレーターにはデザイン時にのみアクセスできますが、MSBuild タスクはデザイン時およびビルド時に使用できます。 そのため、柔軟性を最大限に高めるために、MSBuild タスクを使用してコードを変換および生成します。 詳細については、「 [カスタムツール](../../extensibility/internals/custom-tools.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [MSBuild リファレンス](../../msbuild/msbuild-reference.md)
- [MSBuild](../../msbuild/msbuild.md)
- [カスタムツール](../../extensibility/internals/custom-tools.md)
