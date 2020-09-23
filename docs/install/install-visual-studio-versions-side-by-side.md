---
title: 複数バージョンの Visual Studio をインストールする
ms.date: 07/24/2019
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: conceptual
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.openlocfilehash: b0e5a2d09cad35266bacc73580b2284f66bd32f5
ms.sourcegitcommit: d97d72308ef306e7f28c3a76913caee4ff450bbb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2020
ms.locfileid: "90713465"
---
# <a name="install-visual-studio-versions-side-by-side"></a>複数バージョンの Visual Studio をインストールする

Visual Studio は、以前のバージョンまたは最新バージョンの Visual Studio が既にインストールされたコンピューターにもインストールできます。

::: moniker range="vs-2017"

複数のバージョンを並行してインストールする前に、次の条件を確認してください。

* Visual Studio 2015 で作成されたソリューションを Visual Studio 2017 を使用して開く場合、Visual Studio 2017 に固有の機能が実装されていない限り、後で以前のバージョンのソリューションを開き、再度変更することができます。

* Visual Studio 2015 以前のバージョンで作成されたソリューションを Visual Studio 2017 を使用して開こうとする場合、ご利用のプロジェクトとファイルを Visual Studio 2017 に対応するように変更することが必要な場合があります。 詳細については、[Visual Studio プロジェクトの移植、移行、およびアップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017)に関するページを参照してください。

::: moniker-end

::: moniker range=">= vs-2019"

複数のバージョンを並行してインストールする前に、次の条件を確認してください。

* Visual Studio 2017 で作成されたソリューションを Visual Studio 2019 を使用して開く場合、Visual Studio 2019 に固有の機能が実装されていない限り、後で以前のバージョンのソリューションを開き、再度変更することができます。

* Visual Studio 2017 以前のバージョンで作成されたソリューションを Visual Studio 2019 を使用して開こうとする場合、ご利用のプロジェクトとファイルを Visual Studio 2019 に対応するように変更することが必要な場合があります。 詳細については、[Visual Studio プロジェクトの移植、移行、およびアップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md)に関するページを参照してください。

::: moniker-end

* 複数のバージョンの Visual Studio がコンピューターにインストールされている場合、そのうちの 1 つのバージョンをアンインストールすると、すべてのバージョンの Visual Studio のファイルの関連付けが削除されます。

* すべての拡張機能に互換性があるわけではないので、Visual Studio は拡張機能を自動的にアップグレードしません。 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) またはソフトウェア発行者から入手した拡張機能を再インストールする必要があります。

## <a name="install-minor-visual-studio-versions-side-by-side"></a>複数のマイナー バージョンの Visual Studio をサイドバイサイドでインストールする

Visual Studio のあるマイナー バージョンから次のバージョンにアップグレードする場合、既定では、Visual Studio インストーラーによって、現在のインストールがそのチャネルの次のバージョンに更新されます。 たとえば、16.6.4 Preview をインストールすると、インストーラーでは現在の 16.6.3 Preview のインストールの置き換えが試行されます。これは、両方のバージョンが 16.6 Preview チャネルにあるためです。 これにより、古いバージョンの Visual Studio がマシンの領域を確実に占有しないようにすることができます。 場合によっては、複数のマイナー リリースをサイドバイサイドでインストールすると役立つ場合があります。 この例では、これは同じマシン上に 16.6.3 と 16.6.4 の両方が存在することを意味します。

1. 既存のバージョンの Visual Studio と共にサイドバイサイドでインストールするマイナー バージョンの [Visual Studio ブートストラップ ファイル](/visualstudio/releases/2019/history#installing-an-earlier-release)をダウンロードします。
2. 管理者モードでコマンド プロンプトを開きます。 これを行うには、Windows のスタート メニューを開き、「cmd」と入力し、コマンド プロンプトの検索結果を右クリックし、 **[管理者として実行]** を選択します。 コマンド プロンプトで、Visual Studio ブートストラップ ファイルが配置されているフォルダーにディレクトリを変更します。
3. 次のコマンドを実行して、インストール場所に新しいフォルダーのパスを指定し、.exe ファイル名を、インストールするバージョンの Visual Studio の適切なブートストラップ名に置き換えます。 .exe ファイル名は、以下のファイルと同じか、同様の名前にすることをお勧めします。
   * Visual Studio Community の場合は vs_community.exe
   * Visual Studio Professional の場合は vs_professional.exe
   * Visual Studio Enterprise の場合は vs_enterprise.exe

   ```
   vs_Enterprise.exe --installPath "C:\Program Files (x86)\Microsoft Visual Studio\<2019 AddNewPath>"
   ```

4. インストーラーのダイアログに従って、インストールに必要なコンポーネントを選択します。 詳細については、「[Visual Studio のインストール](install-visual-studio.md#step-4---choose-workloads)」を参照してください。

## <a name="net-framework-versions-and-side-by-side-installations"></a>.NET Framework のバージョンと複数バージョンのインストール

Visual Basic、Visual C#、および Visual F# のプロジェクトでは、**プロジェクト デザイナー** の **[ターゲット フレームワーク]** オプションを使用して、プロジェクトで使用する .NET Framework のバージョンを指定します。 C++ プロジェクトでは、.vcxproj ファイルを変更すると、ターゲット フレームワークを手動で変更できます。 詳細については、「[.NET Framework のバージョンの互換性](/dotnet/framework/migration-guide/version-compatibility)」ページを参照してください。

プロジェクトを作成するときは、プロジェクトが対象とする .NET Framework のバージョンを **[新しいプロジェクト]** ダイアログ ボックスの **[.NET Framework]** の一覧で指定できます。

言語固有の情報については、次の表の適切なトピックを参照してください。

::: moniker range="vs-2017"

| 言語 | トピック |
|--------------|-----------|
| Visual Basic | [[アプリケーション] ページ (プロジェクト デザイナー)](../ide/reference/application-page-project-designer-visual-basic.md?view=vs-2017) |
| Visual C# | [[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md?view=vs-2017) |
| Visual F# | [Visual Studio で Visual F# を使用して開発する](../ide/fsharp-visual-studio.md?view=vs-2017) |
|C++ | [方法: ターゲット フレームワークおよびプラットフォームのツールセットを変更する](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/) |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md?view=vs-2017)
* [Visual Studio プロジェクトのポート、移行、アップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017)
* [C/C++ 分離アプリケーションおよび side-by-side アセンブリのビルド](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end

::: moniker range=">= vs-2019"

| 言語 | トピック |
|--------------|-----------|
| Visual Basic | [[アプリケーション] ページ (プロジェクト デザイナー)](../ide/reference/application-page-project-designer-visual-basic.md) |
| Visual C# | [[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md) |
| Visual F# | [Visual Studio で Visual F# を使用して開発する](../ide/fsharp-visual-studio.md) |
| C++ | [方法: ターゲット フレームワークおよびプラットフォームのツールセットを変更する](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/) |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [Visual Studio プロジェクトのポート、移行、アップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
* [C/C++ 分離アプリケーションおよび side-by-side アセンブリのビルド](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end