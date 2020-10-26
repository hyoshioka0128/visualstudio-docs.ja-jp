---
title: スタート ページのカスタマイズ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.startpage
- VS.StartPage.HowDoI
- vs.ToolsOptionsPages.Startup
helpviewer_keywords:
- Start Page [Visual Studio]
- customizing Start Page [Visual Studio]
- Visual Studio Start page
ms.assetid: 925d42eb-ec34-426e-ad81-19db8630e536
caps.latest.revision: 48
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f1c3dfb145e70665156c921cc9a6f740539bc4e6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665851"
---
# <a name="customizing-the-start-page-for-visual-studio"></a>Visual Studio のスタート ページのカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のスタート ページは、既定のさまざまな方法でカスタマイズできます。**[プロジェクトを開く]** ダイアログ ボックスを表示することも、最後に読み込まれたソリューションを開くこともできます。 また、カスタム スタート ページを表示することもできます。これは、ツール ウィンドウで実行される Windows Presentation Foundation (WPF) の XAML ページで、Visual Studio 内のコマンドを実行できます。

## <a name="customizing-the-default-start-page"></a>既定のスタート ページのカスタマイズ

1. メニューバーで、[ **ツール**]、[ **オプション**] の順に選択します。

2. **[環境]** を展開し、 **[スタートアップ]** を選びます。

3. **[スタートアップ時]** の一覧で、カスタマイズ対象の項目を選びます。

## <a name="show-a-custom-start-page"></a>カスタム スタート ページの表示

1. 次のいずれかの方法でカスタム スタート ページをインストールします。

    - [Visual Studio Marketplace](https://marketplace.visualstudio.com/)、別の Web サイト、またはローカル イントラネット上のページからインストールします。

        > [!NOTE]
        > Visual Studio の旧バージョンを対象とするページの場合、Visual Studio SDK を使用してページをアップグレードできます。 「[方法: Visual Studio のカスタム スタート ページをアップグレードする](../misc/how-to-upgrade-a-visual-studio-custom-start-page.md)」を参照してください。

         カスタム スタート ページを含む .vsix ファイルを開くか、スタート ページ ファイルをコピーしてコンピューターの **%USERPROFILE% \My Documents\Visual Studio 2015\StartPages** フォルダーに貼り付けます。

    - Visual Studio SDK をインストールしている場合は独自のスタート ページを作成できます。

         「[Creating Your Own Start Page (独自のスタート ページの作成)](../misc/creating-your-own-start-page.md)」をご覧ください。

2. メニューバーで、[ **ツール**]、[ **オプション**] の順に選択します。

3. **[環境]** を展開し、**[スタートアップ]** を選びます。

4. **[スタート ページのカスタマイズ]** の一覧で、使用するページを選択します。

> [!NOTE]
> カスタム スタート ページのエラーによって Visual Studio がクラッシュする場合、セーフ モードで Visual Studio を起動し、既定のスタート ページを使用するように設定します。 「[/SafeMode (devenv.exe)](../ide/reference/safemode-devenv-exe.md)」をご覧ください。

## <a name="see-also"></a>参照
 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3) [独自のスタート ページの作成](../misc/creating-your-own-start-page.md)
