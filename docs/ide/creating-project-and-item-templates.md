---
title: プロジェクトとファイルのテンプレート
description: プロジェクトおよび項目テンプレートに、基本的なコードや構造をユーザーに提供する再利用可能なスタブが用意されているしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 01/02/2018
ms.topic: conceptual
helpviewer_keywords:
- templates [Visual Studio], project
- templates [Visual Studio], item
- item templates [Visual Studio]
- project templates [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: e5a3a555a9c0674c70e93ec557416c05d282fbcf
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99956816"
---
# <a name="project-and-item-templates"></a>プロジェクト テンプレートと項目テンプレート

プロジェクト テンプレートおよび項目テンプレートには、基本的なコードや構造をユーザーに提供する再使用可能なスタブが用意されており、ユーザーは独自の目的に合わせてそれをカスタマイズできます。

## <a name="visual-studio-templates"></a>Visual Studio のテンプレート

Visual Studio では、複数の定義済みのプロジェクト テンプレートおよび項目テンプレートがインストールされます。 これらのテンプレート (**ASP.NET Web アプリケーション** テンプレートや **クラス ライブラリ** テンプレートなど) は、新しいプロジェクトを作成する際に選択できます。 項目テンプレート (コード ファイル、XML ファイル、HTML ページ、スタイル シートなど) は、**[新しい項目の追加]** ウィンドウに表示されます。

これらのテンプレートは、ユーザーがプロジェクトの作成を開始したり、既存プロジェクトを拡張したりするための開始点を提供します。 プロジェクト テンプレートには、特定の種類のプロジェクトで必要になるファイルが用意されており、標準のアセンブリ参照が含まれています。また、ここで既定のプロパティとコンパイラ オプションが設定されます。 項目テンプレートの複雑さは、特定のファイル拡張子を持つ 1 つの空のファイルから、スタブ コードを含む複数のソース コード ファイル、デザイナー情報ファイル、埋め込みリソースまで、さまざまです。

インストール済みテンプレートを使用したり、独自のカスタム テンプレートを作成したり、コミュニティで作成されたテンプレートをダウンロードして使用したりできます。 詳細については、「[方法: プロジェクト テンプレートを作成する](../ide/how-to-create-project-templates.md)」および「[方法: 項目テンプレートを作成する](../ide/how-to-create-item-templates.md)」を参照してください。

## <a name="contents-of-a-template"></a>テンプレートの内容

すべてのプロジェクト テンプレートと項目テンプレートは、Visual Studio でインストールされたものも、自分で作成したものも、同じ原則で機能し、似た内容から構成されます。 すべてのテンプレートには次の項目が含まれます。

- テンプレートを使用すると作成されるファイル。 これらのファイルには、ソース コード ファイル、埋め込みリソース、プロジェクト ファイルなどが含まれます。

::: moniker range="vs-2017"

- *.vstemplate* ファイル。テンプレートからプロジェクトや項目を作成するため、また **[新しいプロジェクト]** ウィンドウと **[新しい項目の追加]** ウィンドウにテンプレートを表示するために必要なメタデータが含まれます。

::: moniker-end

::: moniker range=">=vs-2019"

- *.vstemplate* ファイル。テンプレートからプロジェクトや項目を作成するため、また **[新しいプロジェクトの作成]** ページまたは **[新しい項目の追加]** ダイアログ ボックスにテンプレートを表示するために必要なメタデータが含まれます。

::: moniker-end

   *.vstemplate* ファイルについて詳しくは、[テンプレート タグ](template-tags.md)に関するページと「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

これらのファイルが *.zip* ファイルに圧縮されて適切なフォルダーに配置されると、Visual Studio はそれを次の場所に自動的に表示します。

::: moniker range="vs-2017"

- プロジェクト テンプレートは、**[新しいプロジェクト]** ウィンドウに表示されます。

::: moniker-end

::: moniker range=">=vs-2019"

- プロジェクト テンプレートは、**[新しいプロジェクトの作成]** ページに表示されます。

::: moniker-end

- 項目テンプレートは、**[新しい項目の追加]** ウィンドウに表示されます。

テンプレート フォルダーについては、「[方法: テンプレートを配置して整理する](../ide/how-to-locate-and-organize-project-and-item-templates.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: プロジェクト テンプレートを作成する](../ide/how-to-create-project-templates.md)
- [方法: 項目テンプレートを作成する](../ide/how-to-create-item-templates.md)
- [テンプレート タグ](template-tags.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [テンプレートのカスタマイズ](../ide/customizing-project-and-item-templates.md)
- [Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)
