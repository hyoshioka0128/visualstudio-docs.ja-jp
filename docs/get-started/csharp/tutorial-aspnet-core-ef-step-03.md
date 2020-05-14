---
title: '手順 3: ASP.NET Core アプリでのデータの処理'
description: このビデオ チュートリアルおよびステップ バイ ステップの手順に従い、ASP.NET Core Web アプリ内で Entity Framework Core を使用して、データの処理を開始します。
ms.custom: get-started
ms.date: 03/31/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
monikerRange: vs-2019
ms.topic: tutorial
ms.devlang: CSharp
author: ardalis
ms.author: ornella
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: cef0db7e5615d08fb5b22c38604a24124c853ebd
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "77580067"
---
# <a name="step-3-work-with-data-using-entity-framework"></a>手順 3: Entity Framework を使用してデータを処理する

ASP.NET Core Web アプリ内で Entity Framework Core を使用してデータの処理を開始するには、以下の手順に従います。

_最初の ASP.NET Core アプリにデータを追加するには、このビデオをご覧になり、手順を理解してください。_

> [!VIDEO https://www.youtube.com/embed/dulJCwNrqhM]

## <a name="open-your-project"></a>プロジェクトを開く

このビデオの内容を理解している場合は、前のセクションで作成した Web アプリケーション プロジェクトを開きます。 ここから開始する場合は、新しいプロジェクトを作成し、 **[ASP.NET Web アプリケーション]** 、 **[Web アプリケーション]** の順に選択する必要があります。 残りのオプションは既定のままにします。

## <a name="add-your-model"></a>モデルを追加する

ASP.NET Core アプリケーションでデータを処理するには、最初にデータの外観を記述する必要があります。 これは、解決を試みる問題に含まれる物事の "*モデル*" 化と呼ばれます。 実際のアプリケーションでは、これらのモデルにカスタム ビジネス ロジックを追加し、モデルが特定の方法で動作したり、タスクを自動化したりできるようにします。 このサンプルでは、ボード ゲームを追跡するためのシンプルなシステムを作成します。 ゲームを表すと共に、ゲームについて記録すべきプロパティ (例: サポートできるプレーヤー数) を含むクラスが必要です。 このクラスは、Web プロジェクトのルートに作成する *Models* という新しいフォルダー内に格納されます。

```csharp
public class Game
{
    public int Id { get; set; }
    public string Title { get; set; }
    public int PublicationYear { get; set; }
    public int MinimumPlayers { get; set; }
    public int MaximumPlayers { get; set; }
}
```

## <a name="create-the-pages-to-manage-your-game-library"></a>ゲーム ライブラリを管理するページを作成する

ゲーム ライブラリ管理用のページを作成する準備が整いました。 これは難しそうに思えるかもしれませんが、実際には驚くほど簡単です。 最初に、アプリ内のどこに、この機能を配置するかを決定する必要があります。 Web プロジェクト内の Pages フォルダーを開き、この場所に新しいフォルダーを追加します。 このフォルダーの名前は、*Games* に設定します。

[Games] を右クリックし、 **[追加]**  >  **[新規スキャフォールディング アイテム]** を選択します。 **Entity Framework (CRUD)** を使用する Razor ページのオプションを選択します。 CRUD は "Create (作成)、Read (読み取り)、Update (更新)、Delete (削除)" を意味します。このテンプレートにより、これらの各操作のページが作成されます ([list all]\(すべてリスト\) ページおよび [view details of one item]\(1 つの項目の詳細を表示\) ページを含む)。

![Visual Studio 2019 ASP.NET Core のスキャフォールディングされたページの追加](media/vs-2019/vs2019-add-scaffold.png)

Game モデル クラスを選択し、[+] アイコンを使用して、新しい Data コンテキスト クラスを追加します。 これに `AppDbContext` という名前を付けます。 残りは既定のままにして、 **[追加]** をクリックします。

以下の Razor Pages が Games フォルダーに追加されます。

- Create.cshtml
- Delete.cshtml
- Details.cshtml
- Edit.cshtml
- Index.cshtml

![Visual Studio 2019 ASP.NET Core のスキャフォールディングされたページ](media/vs-2019/vs2019-scaffolded-pages.png)

スキャフォールディング操作により、*Games* フォルダー内にページが追加されるだけではなく、*Startup.cs* クラスにコードが追加されました。 このクラス内にある `ConfigureServices` メソッドの中を見ると、以下のコードが追加されていることがわかります。

```csharp
services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("AppDbContext")));
```

また、プロジェクトの *appsettings.json* ファイルに接続文字列 `AppDbContext` が追加されていることもわかります。

データベースがまだ作成されていないため、ここでアプリを実行しても失敗する可能性があります。 必要に応じて自動的にデータベースを作成するようにアプリを構成するには、[Program.cs にコードを追加](/aspnet/core/data/ef-rp/intro?view=aspnetcore-2.1&tabs=visual-studio#update-main)します。

```csharp
public static void Main(string[] args)
{
    var host = CreateWebHostBuilder(args).Build();

    using (var scope = host.Services.CreateScope())
    {
        var services = scope.ServiceProvider;

        try
        {
            var context = services.GetRequiredService<AppDbContext>();
            context.Database.EnsureCreated();
        }
        catch (Exception ex)
        {
            var logger = services.GetRequiredService<ILogger<Program>>();
            logger.LogError(ex, "An error occurred creating the DB.");
        }
    }

    host.Run();
}
```

前のコードの typenames を解決するには、次の using ステートメントを *Program.cs* の既存の using ステートメント ブロックの末尾に追加します。

```csharp
using Microsoft.Extensions.DependencyInjection;
using WebApplication1.Models;
```

コードでは、WebApplication1 の代わりに実際のプロジェクト名を使ってください。

コードの大部分は、エラー処理用のコードで、アプリの実行前に EF Core `AppDbContext` にアクセスできるようにするためのものです。 重要な行は、`context.Database.EnsureCreated()` が記述されている行です。この行により、データベースがまだ存在していない場合にデータベースが作成されます。 これで、アプリを実行する準備が整いました。

## <a name="test-it-out"></a>テスト

アプリケーションを実行し、アドレス バー内の `/Games` に移動します。 空のリスト ページが表示されます。 **[新規作成]** をクリックし、新しい `Game` をコレクションに追加します。 フォームに入力し、 **[作成]** をクリックします。 これは、リスト ビューに表示されます。 **[詳細]** をクリックすると、単一レコードの詳細が表示されます。

別のレコードを追加します。 レコードの詳細を変更するには、 *[編集]* をクリックします。レコードを削除するには、 **[削除]** をクリックします。[削除] をクリックした場合は、レコードを実際に削除する前に確認が求められます。

![Visual Studio 2019 ASP.NET Core のブラウザー内のスキャフォールディングされたページ](media/vs-2019/vs2019-game-list.png)

以上で、EF Core および Visual Studio 2019 を使用して ASP.NET Core アプリ内のデータの処理を開始できるようになりました。

## <a name="next-steps"></a>次の手順

次のビデオでは、アプリに Web API サポートを追加する方法を学びます。

[手順 4:ASP.NET Core アプリから Web API を公開する](tutorial-aspnet-core-ef-step-04.md)

## <a name="see-also"></a>関連項目

- [ASP.NET Core での Entity Framework Core を使用した Razor Pages](/aspnet/core/data/ef-rp/intro?view=aspnetcore-2.1&tabs=visual-studio)
- [ASP.NET Core Razor Pages と EF Core](/aspnet/core/data/?view=aspnetcore-2.1)
