---
title: MSBuild の使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a1ad59e6d8f4cb88004629b0dfd2cdf0631a7824
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297672"
---
# <a name="using-msbuild"></a>MSBuild の使用
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

MSBuild には、ビルドするプロジェクト項目、ビルドタスク、およびビルド構成を完全に記述したプロジェクトファイルを作成するための、適切に定義された拡張可能な XML 形式が用意されています。  
  
 MSBuild に基づく言語プロジェクトシステムのエンドツーエンドのサンプルについては、「[Vssdk](../../misc/vssdk-samples.md)のサンプル」の IronPython サンプルを参照してください。  
  
## <a name="general-msbuild-considerations"></a>MSBuild に関する一般的な考慮事項  
 MSBuild プロジェクトファイル ([!INCLUDE[csprcs](../../includes/csprcs-md.md)] .csproj ファイル、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .vbproj ファイルなど) には、ビルド時に使用されるデータが含まれますが、デザイン時に使用されるデータを含めることもできます。 ビルド時のデータは、 [Item 要素 (msbuild)](../../msbuild/item-element-msbuild.md)や[Property 要素 (msbuild)](../../msbuild/property-element-msbuild.md)などの msbuild プリミティブを使用して格納されます。 デザイン時データは、プロジェクトの種類および関連するプロジェクトのサブタイプに固有のデータであり、そのために予約された自由形式の XML に格納されます。  
  
 MSBuild には構成オブジェクトのネイティブサポートはありませんが、構成固有のデータを指定するための条件付き属性が用意されています。 例 :  
  
```  
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>  
```  
  
 条件付き属性の詳細については、「[条件付き構成体](../../msbuild/msbuild-conditional-constructs.md)」を参照してください。  
  
### <a name="extending-msbuild-for-your-project-type"></a>プロジェクトの種類の MSBuild の拡張  
 MSBuild のインターフェイスと Api は、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]の将来のバージョンで変更される可能性があります。 そのため、managed package framework (MPF) クラスを使用することをお勧めします。これは、変更によってシールドが提供されるためです。  
  
 プロジェクト用の Managed Package Framework (MPFProj) には、新しいプロジェクトシステムを作成および管理するためのヘルパークラスが用意されています。 ソースコードとコンパイルの手順については、「 [MPF For Projects-Visual Studio 2013](https://archive.codeplex.com/?p=mpfproj12)」を参照してください。  
  
 プロジェクト固有の MPF クラスは次のとおりです。  
  
|インスタンス|実装|  
|-----------|--------------------|  
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|  
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|  
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|  
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|  
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|  
  
 `Microsoft.VisualStudio.Package.ProjectElement` クラスは、MSBuild 項目のラッパーです。  
  
#### <a name="single-file-generators-vs-msbuild-tasks"></a>単一ファイルジェネレーターと MSBuild タスク  
 1つのファイルジェネレーターにはデザイン時にのみアクセスできますが、MSBuild タスクはデザイン時およびビルド時に使用できます。 そのため、柔軟性を最大限に高めるために、MSBuild タスクを使用してコードを変換および生成します。 詳細については、「[カスタムツール](../../extensibility/internals/custom-tools.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [MSBuild リファレンス](../../msbuild/msbuild-reference.md)   
 [MSBuild](https://msdn.microsoft.com/7c49aba1-ee6c-47d8-9de1-6f29a906e20b)   
 [カスタム ツール](../../extensibility/internals/custom-tools.md)
