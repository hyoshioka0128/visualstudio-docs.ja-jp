---
title: プロジェクトおよびソリューション
description: このドキュメントでは、Visual Studio for Mac のプロジェクトとソリューションの概要について説明します。
ms.topic: overview
author: heiligerdankgesang
ms.author: dominicn
ms.date: 11/09/2020
ms.assetid: 8254505D-D96E-48BD-8A5E-CF6A917897EA
ms.openlocfilehash: c52b8513937505b40d17f7cd9fc05d9cf6a47941
ms.sourcegitcommit: 2cf3a03044592367191b836b9d19028768141470
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94493401"
---
# <a name="projects-and-solutions-in-visual-studio-for-mac"></a>Visual Studio for Mac のプロジェクトとソリューション

この記事では、Visual Studio for Mac での "*プロジェクト*" と "*ソリューション*" の概念について概要を説明します。

> [!NOTE] 
> このトピックは、Visual Studio for Mac に適用されます。 Windows 用 Visual Studio については、「[Visual Studio のソリューションおよびプロジェクト](/visualstudio/ide/solutions-and-projects-in-visual-studio)」を参照してください。

## <a name="projects"></a>プロジェクト

新しいアプリケーションや Web サイトなどを Visual Studio for Mac で作成する場合は、プロジェクトから始めます。 プロジェクトには、実行可能ファイル、ライブラリ、または Web サイトをコンパイルするために必要なすべての必須ファイル (ソース コード、イメージ、データ ファイルなど) が含まれています。

プロジェクトは、ファイルとフォルダー階層、ファイルへのパス、およびプロジェクト固有の設定 (ビルド設定など) を定義する xml が含まれているファイル (たとえば、C# プロジェクトの場合は `.csproj`) によって定義されます。

Visual Studio for Mac によってプロジェクトが読み込まれると、[ソリューション] ウィンドウには、プロジェクト ファイルを使用してご利用のプロジェクト内のファイルとフォルダーが表示されます。 コンパイル時に、MSBuild によってプロジェクト ファイルから設定が読み取られ、実行可能ファイルが作成されます。

## <a name="solutions"></a>解決策

"*ソリューション*" とは、1 つまたは複数の関連するプロジェクトをグループ化する論理コンテナーです。 ソリューションは独自の形式を持つテキスト ファイル (拡張子: `.sln`) で記述され、手動での編集を意図していません。

## <a name="managing-projects-in-the-solution-window"></a>[ソリューション] ウィンドウでのプロジェクトの管理

プロジェクトが作成されたら、または読み込まれたら、[ソリューション] ウィンドウを使用してプロジェクトまたはソリューションとその中に含まれるファイルを表示および管理できます。 次の図に、2 つのプロジェクトを含む .NET Core ソリューションが表示された [ソリューション] ウィンドウを示します。

![複数のプロジェクトを含むサンプル ソリューション](media/solution-example.png)

プロジェクトとソリューションの両方のプロパティを管理するには、プロジェクトまたはソリューションの名前をダブルクリックするか、右クリックして **[オプション]** を選択します。

これらのオプションの詳細については、「[ソリューションとプロジェクト プロパティの管理](managing-solutions-and-project-properties.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio のソリューションおよびプロジェクト (Windows)](/visualstudio/ide/solutions-and-projects-in-visual-studio)
