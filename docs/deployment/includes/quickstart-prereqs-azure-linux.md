---
ms.openlocfilehash: b2f9327da5e195c50bd074a468e1f9e57ece94ea
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101750938"
---
## <a name="prerequisites"></a>前提条件

::: moniker range=">=vs-2019"

* 選択した言語に適したワークロードでインストールされた [Visual Studio 2019](https://visualstudio.microsoft.com/downloads):
  * ASP.NET: **ASP.NET と Web 開発**
::: moniker-end
::: moniker range="vs-2017"
* 選択した言語に適したワークロードでインストールされた [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download):
  * ASP.NET: **ASP.NET と Web 開発**
::: moniker-end

* Azure サブスクリプション。 サブスクリプションがまだない場合は、[無料でサインアップ](https://azure.microsoft.com/free/dotnet/)します。これには、30 日間の $200 のクレジットと、12 か月間の人気の無料サービスが含まれます。

* ASP.NET Core: 「[クイック スタート: Visual Studio を使用して初めての ASP.NET Core Web アプリを作成する](../../ide/quickstart-aspnet-core.md)」に従うか、以下の手順に従います。
  ::: moniker range=">=vs-2019"
  Visual Studio 2019 で、スタート ウィンドウの **[新しいプロジェクトの作成]** を選択します。 スタート ウィンドウが開いていない場合は、 **[ファイル]**  >  **[スタート ウィンドウ]** を選択します。 検索ボックスに「**Web アプリ**」と入力し、言語として **C#** を選択してから、 **[ASP.NET Core Web Application (Model-View-Controller)]\(ASP.NET Core Web アプリケーション (Model-View-Controller)\)** を選択した後、 **[次へ]** を選択します。 次の画面で、プロジェクトに「**MyASPApp**」という名前を指定し、 **[次へ]** を選択します。

  推奨されるターゲット フレームワーク (.NET Core 3.1) または .NET 5 を選択し、 **[作成]** を選択します。
  ::: moniker-end
  ::: moniker range="vs-2017"
  Visual Studio 2017 で、 **[ファイル]**  >  **[新しいプロジェクト]** を選択し、 **[Visual C#]**  >  **[.NET Core]** を選択してから、 **[ASP.NET Core Web アプリケーション]** を選択します。 プロンプトが表示されたら、**[Web アプリケーション (モデル ビュー コントローラー)]** テンプレートを選び、**[認証なし]** が選択されていることを確認してから、**[OK]** を選択します。
  ::: moniker-end

* 配置手順を行う前に、必ず、**[ビルド] > [ビルド ソリューション]** メニュー コマンドを使用してプロジェクトをビルドしてください。