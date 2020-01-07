---
title: Visual Studio 2015 のアンインストール | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
f1_keywords:
- uninstalling
- uninstalling visual studio
- uninstall
- uninstall Visual Studio
ms.assetid: 0e445255-b796-426d-ad93-a4d8e36da2c5
caps.latest.revision: 9
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: ed9d33501644c6fa7252dffa758f92c0919653b1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546903"
---
# <a name="uninstall-visual-studio"></a>Visual Studio のアンインストール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio に関する最新のドキュメントについては、「[Visual Studio のアンインストール](/visualstudio/install/uninstall-visual-studio)」をご覧ください。

このページでは、開発者向け生産性向上ツールの統合スイートの以前のバージョンである、Visual Studio 2015 のアンインストールについて説明します。

## <a name="uninstall-visual-studio-by-using-the-standard-uninstallation-method"></a>"標準" アンインストール方法を使った Visual Studio のアンインストール

1. **[コントロール パネル]** の **[プログラムと機能]** ページで、アンインストールする製品のエディションを選択し、**[変更]** を選択します。

2. セットアップ ウィザードで、**[アンインストール]**、**[はい]** の順に選択し、ウィザードの残りの指示に従います。

   この標準または既定の方法では、最初に Visual Studio をインストールしたときにインストールされていた項目がいくつか残ります (たとえば、Microsoft .NET Framework、Microsoft Visual C++ 再頒布可能パッケージ、Microsoft SQL Server など)。   これらは、他の多くのアプリケーションが依存しているため、インストールされたままになります。 ただし、これらも削除したい場合は、**[プログラムと機能]** でそのエントリを選択してから、それぞれを個別に削除します。

## <a name="uninstall-visual-studio-and-all-other-related-files-that-is-to-uninstall-almost-everything"></a>Visual Studio および他のすべての関連ファイルをアンインストールする (つまり、ほぼすべてをアンインストールする)

1. Visual Studio の .exe ファイルを見つけます (たとえば、"vs_enterprise.exe" を見つけます)。

    > [!NOTE]
    > ファイルは、"%ProgramData%\Package Cache" のサブフォルダー内にあるはずです。例: C:\ProgramData\Package Cache\\{37e19555-e88d-4aed-9d42-82d0784d2b79}\vs_enterprise.exe

2. /uninstall /force コマンド ライン パラメーターを使って .exe ファイルを実行します。

     たとえば、```vs_enterprise.exe /uninstall /force``` を実行します。これにより、Visual Studio と、既定のアンインストールでは残されるコア コンポーネントのほとんどが削除されます。 ただし、これによって Visual Studio のアドオンや拡張機能でインストールできるすべての追加コンテンツが削除されるわけではありません (たとえば、Visual Studio 更新プログラムや、その他の省略可能なコンポーネント)。

    > [!TIP]
    > 代わりに、"**全体アンインストーラー**" ツールを使って、Visual Studio または Visual Studio の更新プログラムによりインストールされた可能性のあるものをすべて削除できます。 つまり、Visual Studio 2013 以降のすべてのバージョンです。 詳細については、GitHub 上の [Visual Studio アンインストーラー ツール](https://github.com/Microsoft/VisualStudioUninstaller/releases)に関するページをご覧ください。

## <a name="uninstall-visual-studio-in-silent-or-passive-modes-that-is-to-uninstall-from-source"></a>サイレントまたはパッシブ モードで Visual Studio をアンインストールする (つまり、ソースからアンインストールする)

1. Visual Studio がインストールされているコンピューターで、Windows コマンド プロンプトを開きます。

2. 次のパラメーターを入力します。

     *DVDRoot* \\<インストール ファイル\> \</quiet&#124;/passive> [/norestart]/uninstall

## <a name="roll-back-to-a-previous-version-or-release-of--visual-studio"></a>以前のバージョンまたはリリースの Visual Studio に戻す

1. このトピックに記載された方法のいずれかを使って Visual Studio をアンインストールします。

   > [!WARNING]
   > 現在のリリースの Visual Studio (または Visual Studio 更新プログラム) をアンインストールしてから、以前のリリースをインストールしても、想定どおりに動作しないことがあります。
   >
   > インストールした Visual Studio のバージョンまたはリリース、インストールしたそのコンポーネントのバージョン、インストールした Visual Studio のリリースまたはそのコンポーネントに依存する製品、そして最後にインストールまたは再インストールすることを計画している以前の Visual Studio のバージョンに応じて、結果は異なります。  これらすべてのばらつきのため、多くの場合、標準アンインストールでは Visual Studio の以前のバージョンまたはリリースでは動作しないことがあるコンポーネントが残されます。
   >
   > そのため、最適な結果を得るには、[Visual Studio アンインストーラー ツール](https://github.com/Microsoft/VisualStudioUninstaller/releases)を使うことをお勧めします。

2. 使用する Visual Studio の以前のバージョンをインストールまたは再インストールします。

   以前のバージョンの Visual Studio をインストールする場合でも、セットアップ プログラムでは、利用可能なら新しいバージョンまたはリリースを使おうとする場合があります。 詳細については、「[How to: Install a Specific Release of Visual Studio (方法: Visual Studio の特定のリリースをインストールする)](../install/how-to-install-a-specific-release-of-visual-studio.md)」のトピックをご覧ください。

## <a name="see-also"></a>関連項目

- [Visual Studio のインストール](https://msdn.microsoft.com/library/e2h7fzkw.aspx)