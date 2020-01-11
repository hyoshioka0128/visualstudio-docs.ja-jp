---
title: '方法: プロジェクトのアップグレードに失敗した場合のトラブルシューティング |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: troubleshooting
f1_keywords:
- VisualStudio.SourceControl.CannotOpenFromSourceControlDSW
- vs.UpgradeProjectSolution.8.0
helpviewer_keywords:
- upgrading applications, Visual Studio
- upgrading projects [Visual Studio]
- projects [Visual Studio], upgrading
- Visual Studio Conversion Wizard
- Conversion wizard
ms.assetid: 842fe448-c044-4343-8eae-d81711cf48ba
caps.latest.revision: 31
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 65059e285777e48633da5eb7e8723e3997f37dfa
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75844449"
---
# <a name="how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades"></a>方法: Visual Studio プロジェクトのアップグレードが成功しなかった場合のトラブルシューティング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio が、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の旧バージョンで作成したプロジェクトを完全には変換できない場合があります。 以下のセクションのヒントによって特定の問題が解決されない場合は、TechNet [Wiki: 開発ポータル](https://social.technet.microsoft.com/wiki/contents/articles/706.wiki-development-portal.aspx#Visual_Studio)で詳細を確認できます。

## <a name="the-project-does-not-run-because-files-are-not-found"></a>ファイルが見つからないためプロジェクトを実行できない
 プロジェクト ファイルには、ユーザーによって F5 キーが押されたときに [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がプロジェクトの実行に使用するハード コーディングされたファイル パスが含まれています。 これらのパスには、devenv.exe やその他の必須ファイルの場所などがあります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のアップグレード バージョンでは、これらのファイルのパスが変更されている場合があります。

#### <a name="to-resolve-incorrect-file-paths"></a>ファイル パスの間違いを解決するには

1. プロジェクト ファイルをテキスト エディターで開きます。

2. 間違っている可能性のあるファイル パス、特に [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のバージョン番号を含むパスをスキャンします。

3. 間違っているファイル パスを、新しいターゲットを指すように変更します。

## <a name="the-project-does-not-build-because-references-are-not-valid"></a>参照が有効でないため、プロジェクトがビルドできない
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のアップグレード時に、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] のバージョンもアップグレードすることがあります。 新しい [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] バージョンで継承されない参照がプロジェクトに含まれている場合、これらの参照は正しく解決されない可能性があります。 これは特に、`Microsoft.VisualStudio.Shell.Interop.8.0` などのバージョン番号を含む参照で発生する可能性があります。

 コードに無効な参照が多数ある場合、最も簡単な解決策は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の複数バージョン対応機能を使用して [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] の旧バージョンをターゲットにすることです。

#### <a name="to-resolve-incorrect-references"></a>不適切な参照を解決するには

1. プロジェクト ファイルをテキスト エディターで開きます。

2. プロジェクトのプロパティを開きます。

3. **[対象のフレームワーク]** で適切な値を選択します。 または、プロジェクト ファイルの `<TargetFrameworkVersion>` 要素の値を直接変更することもできます。

   アップグレードされた [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] バージョンでプロジェクトを実行する場合は、そのプロジェクトの参照を更新し、参照を呼び出す `Imports` ステートメントまたは `Using` ステートメントも更新する必要があります。 プロジェクトが IDE で読み込まれる場合は、**ソリューション エクスプローラー**または **[参照マネージャー]** ダイアログ ボックスを使用して参照を更新できます。

## <a name="see-also"></a>参照
 [/Upgrade (devenv.exe)](../ide/reference/upgrade-devenv-exe.md) [を ASP.NET 4 に変換する](https://msdn.microsoft.com/library/790147c6-36c1-41b5-a52d-30b9ccd2bd10)
