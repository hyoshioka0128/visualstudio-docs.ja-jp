---
title: MSBuild .targets ファイル | Microsoft Docs
ms.date: 02/24/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- .targets files
- MSBuild, .targets files
ms.assetid: f6d98eb4-d2fa-49b7-8e3c-bae1ca3cf596
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4dc5df9c4eba4195400b6a41fa50a5c88257d70e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75566554"
---
# <a name="msbuild-targets-files"></a>MSBuild .targets ファイル
[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] には、項目、プロパティ、ターゲット、および一般的なシナリオ用のタスクが含まれているいくつかの *.targets* ファイルが含まれます。 これらのファイルはほぼすべて [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロジェクト ファイル自動的にインポートされ、これによってメンテナンスが簡素化されて読みやすさが向上します。

 通常、プロジェクトでは、ビルド プロセスを定義するために、1 つ以上の *.targets* ファイルをインポートします。 たとえば、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって作成された [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] プロジェクトは、*Microsoft.Common.targets* をインポートする *Microsoft.CSharp.targets* をインポートします。 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] プロジェクト自体はそのプロジェクトに固有の項目とプロパティを定義しますが、[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] プロジェクトの標準のビルド規則は、インポートされた *.targets* ファイルで定義されます。

 `$(MSBuildToolsPath)` 値によって、これらの共通 *.targets* ファイルのパスが指定されます。 `ToolsVersion` が 4.0 の場合、ファイルは次の場所にあります。 *\<WindowsInstallationPath>\Microsoft.NET\Framework\v4.0.30319\\*

> [!NOTE]
> 独自のターゲットを作成する方法については、[ターゲット](../msbuild/msbuild-targets.md)に関する記事を参照してください。 `Import` 要素を使用してプロジェクト ファイルを他のプロジェクト ファイルに挿入する方法については、「[Import 要素 (MSBuild)](../msbuild/import-element-msbuild.md)」と「[方法:複数のプロジェクト ファイルで同じターゲットを使用する](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)」を参照してください。

## <a name="common-targets-files"></a>共通 .Targets ファイル

| *.targets* ファイル | 説明 |
|---------------------------------| - |
| *Microsoft.Common.targets* | [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] プロジェクトおよび [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] プロジェクトの標準ビルド プロセスの手順を定義します。<br /><br /> 次のステートメントが含まれている *Microsoft.CSharp.targets* や *Microsoft.VisualBasic.targets* ファイルによってインポートされます: `<Import Project="Microsoft.Common.targets" />` |
| *Microsoft.CSharp.targets* | Visual C# プロジェクトの標準ビルド プロセスの手順を定義します。<br /><br /> 次のステートメントが含まれている Visual C# プロジェクト ファイル ( *.csproj*) によってインポートされます: `<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />` |
| *Microsoft.VisualBasic.targets* | Visual Basic プロジェクトの標準ビルド プロセスの手順を定義します。<br /><br /> 次のステートメントが含まれている Visual Basic プロジェクト ファイル ( *.vbproj*) によってインポートされます: `<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />` |

## <a name="directorybuildtargets"></a>Directory.Build.targets
*Directory.Build.targets* は、ディレクトリの下のプロジェクトをカスタマイズできるようにする、ユーザー定義のファイルです。 **ImportDirectoryBuildTargets** プロパティを **false** に設定しない限り、このファイルは *Microsoft.Common.targets* から自動的にインポートされます。 詳細については、「[ビルドのカスタマイズ](customize-your-build.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Import 要素 (MSBuild)](../msbuild/import-element-msbuild.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [MSBuild](../msbuild/msbuild.md)
