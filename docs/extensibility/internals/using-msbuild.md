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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704286"
---
# <a name="using-msbuild"></a>MSBuild の使用
MSBuild は、ビルド、ビルドタスク、およびビルド構成を完全に記述するプロジェクト ファイルを作成するための、明確に定義された拡張可能な XML 形式を提供します。

## <a name="general-msbuild-considerations"></a>MSBuild の一般的な考慮事項
 MSBuild プロジェクト ファイル (.csproj[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]ファイルや .vbproj ファイルなど) には、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]ビルド時に使用されるデータが含まれますが、デザイン時に使用されるデータを含めることもできます。 ビルド時のデータは、[項目要素 (MSBuild)](../../msbuild/item-element-msbuild.md)およびプロパティ要素[(MSBuild)](../../msbuild/property-element-msbuild.md)を含む MSBuild プリミティブを使用して格納されます。 デザイン時データは、プロジェクトタイプおよび関連するプロジェクトのサブタイプに固有のデータであり、そのデータ用に予約された自由形式 XML に格納されます。

 MSBuild には、構成オブジェクトのネイティブ サポートはありませんが、構成固有のデータを指定するための条件付き属性が用意されています。 次に例を示します。

```xml
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>
```

 条件付き属性の詳細については、「[条件付きコンストラクト](../../msbuild/msbuild-conditional-constructs.md)」を参照してください。

### <a name="extending-msbuild-for-your-project-type"></a>プロジェクトの種類に合わせて MSBuild を拡張する
 MSBuild インターフェイスと API は、今後の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]バージョンで変更される可能性があります。 したがって、変更から保護するため、管理パッケージ フレームワーク (MPF) クラスを使用することが賢明です。

 プロジェクト用管理パッケージ フレームワーク (MPFProj) には、新しいプロジェクト システムを作成および管理するためのヘルパー クラスが用意されています。 ソース コードとコンパイル手順については、[プロジェクトの MPF - Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10)を参照してください。

 プロジェクト固有の MPF クラスは次のとおりです。

|クラス|実装|
|-----------|--------------------|
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|

 `Microsoft.VisualStudio.Package.ProjectElement`クラスは、MSBuild 項目のラッパーです。

#### <a name="single-file-generators-vs-msbuild-tasks"></a>単一ファイル ジェネレーターと MSBuild タスク
 単一ファイル ジェネレーターはデザイン時にのみアクセスできますが、MSBuild タスクはデザイン時およびビルド時に使用できます。 したがって、柔軟性を最大限に高めるために、MSBuild タスクを使用してコードを変換および生成します。 詳細については、「[カスタム ツール](../../extensibility/internals/custom-tools.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [MSBuild リファレンス](../../msbuild/msbuild-reference.md)
- [MSBuild](../../msbuild/msbuild.md)
- [カスタム ツール](../../extensibility/internals/custom-tools.md)
