---
ms.openlocfilehash: a33871a9a80dfcb6260f57e504c72ae2f72077bd
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101750880"
---
## <a name="prerequisites"></a>前提条件

::: moniker range=">=vs-2019"

* 選択した言語に適したワークロードでインストールされた [Visual Studio 2019](https://visualstudio.microsoft.com/downloads):
  * ASP.NET: **ASP.NET と Web 開発**
  * Python: **Python 開発**
  * Node.js: **Node.js 開発**
::: moniker-end
::: moniker range="vs-2017"
* 選択した言語に適したワークロードでインストールされた [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download):
  * ASP.NET: **ASP.NET と Web 開発**
  * Python: **Python 開発**
  * Node.js: **Node.js 開発**
::: moniker-end

* ASP.NET、.NET Core、Python、または Node.js プロジェクト。 プロジェクトがまだない場合は、以下のオプションを選択します。
  * ASP.NET Core: 「[クイック スタート: Visual Studio を使用して初めての ASP.NET Core Web アプリを作成する](../../ide/quickstart-aspnet-core.md)」に従うか、以下の手順に従います。
    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で、スタート ウィンドウの **[新しいプロジェクトの作成]** を選択します。 スタート ウィンドウが開いていない場合は、 **[ファイル]**  >  **[スタート ウィンドウ]** を選択します。 検索ボックスに「**Web アプリ**」と入力し、言語として **C#** を選択してから、 **[ASP.NET Core Web Application (Model-View-Controller)]\(ASP.NET Core Web アプリケーション (Model-View-Controller)\)** を選択した後、 **[次へ]** を選択します。 次の画面で、プロジェクトに「**MyASPApp**」という名前を指定し、 **[次へ]** を選択します。

    推奨されるターゲット フレームワーク (.NET Core 3.1) または .NET 5 を選択し、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 で、 **[ファイル]**  >  **[新しいプロジェクト]** を選択し、 **[Visual C#]**  >  **[.NET Core]** を選択してから、 **[ASP.NET Core Web アプリケーション]** を選択します。 プロンプトが表示されたら、**[Web アプリケーション (モデル ビュー コントローラー)]** テンプレートを選び、**[認証なし]** が選択されていることを確認してから、**[OK]** を選択します。
    ::: moniker-end
  * Python: 「[クイック スタート: Visual Studio を使用して初めての Python Web アプリを作成する](../../ide/quickstart-python.md)」に従うか、**[ファイル]** > **[新しいプロジェクト]** を使用して、**[Python]** を選択してから、**[Flask Web プロジェクト]** を選択します。
  * Node.js: 「[クイック スタート: Visual Studio を使用して初めての Node.js アプリを作成する](../../ide/quickstart-nodejs.md)」に従うか、**[ファイル]** > **[新しいプロジェクト]** を使用して、**[JavaScript]** を選択してから、**[空白の Node.js Web アプリケーション]** を選択します。

* 配置手順を行う前に、必ず、**[ビルド] > [ビルド ソリューション]** メニュー コマンドを使用してプロジェクトをビルドしてください。