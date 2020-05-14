---
ms.openlocfilehash: 6c210537c671ef6960d3f767c740dee5c1538fac
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "70197153"
---
## <a name="prerequisites"></a>必須コンポーネント

::: moniker range=">=vs-2019"

* 選択した言語に適したワークロードでインストールされた [Visual Studio 2019](https://visualstudio.microsoft.com/downloads):
  * ASP.NET:**ASP.NET と Web 開発**
  * Node.js: **Node.js 開発**
::: moniker-end
::: moniker range="vs-2017"
* 選択した言語に適したワークロードでインストールされた [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download):
  * ASP.NET:**ASP.NET と Web 開発**
  * Node.js: **Node.js 開発**
::: moniker-end

* Azure サブスクリプション。 サブスクリプションがまだない場合は、[無料でサインアップ](https://azure.microsoft.com/free/dotnet/)します。これには、30 日間の $200 のクレジットと、12 か月間の人気の無料サービスが含まれます。

* ASP.NET、ASP.NET Core、.NET Core、または Node.js プロジェクト。 プロジェクトがまだない場合は、以下のオプションを選択します。
  * ASP.NET Core:[「クイック スタート: Visual Studio を使用して初めての ASP.NET Core Web アプリを作成する](../../ide/quickstart-aspnet-core.md)」に従って進めるか、 **[ファイル]** 、 **[新しいプロジェクト]** 、 **[Visual C#]** 、 **[.NET Core]** の順に選択してから **[ASP.NET Core Web アプリケーション]** を選択します。 プロンプトが表示されたら、 **[Web アプリケーション (モデル ビュー コントローラー)]** テンプレートを選び、 **[認証なし]** が選択されていることを確認してから、 **[OK]** を選択します。
  * Node.js: [「クイック スタート: Visual Studio を使用して初めての Node.js アプリを作成する](../../ide/quickstart-nodejs.md)」に従って進めるか、 **[ファイル]** 、 **[新しいプロジェクト]** 、 **[JavaScript]** の順に選択してから **[空白の Node.js Web アプリケーション]** を選択します。

* 配置手順を行う前に、必ず、 **[ビルド] > [ビルド ソリューション]** メニュー コマンドを使用してプロジェクトをビルドしてください。