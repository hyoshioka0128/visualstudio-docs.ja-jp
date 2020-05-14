---
title: '手順 4: ASP.NET Core アプリから Web API を公開する'
description: このビデオ チュートリアルとステップ バイ ステップの手順に従って、ASP.NET Core Web アプリに Web API を追加します。
ms.custom: get-started
ms.date: 02/13/2020
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
ms.openlocfilehash: 5ea9468bdf86986ab542fb1cabc873c9aeb75fd6
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "77580041"
---
# <a name="step-4-expose-a-web-api-from-your-aspnet-core-app"></a>手順 4: ASP.NET Core アプリから Web API を公開する

次の手順に従って、既存の ASP.NET Core アプリに Web API を追加します。

_このビデオをご覧になり、手順に従って初めての ASP.NET Core アプリに Web API のサポートを追加します。_

> [!VIDEO https://www.youtube.com/embed/o_fYPOsAXts]

## <a name="open-your-project"></a>プロジェクトを開く

Visual Studio 2019 で ASP.NET Core アプリを開きます。 アプリは、[このチュートリアル シリーズの手順 3](tutorial-aspnet-core-ef-step-03.md) で構成したように、EF Core を使用してモデルの種類を管理します。

## <a name="add-an-api-controller"></a>API コントローラーを追加する

プロジェクトを右クリックし、*Api* という名前の新しいフォルダーを追加します。 次に、このフォルダーを右クリックし、 **[追加]**  >  **[新規スキャフォールディング アイテム]** を選択します。 **[Entity Framework を使用したアクションがある API コントローラー]** を選択します。 次に、既存のモデル クラスを選択し、 **[追加]** をクリックします。

![Visual Studio 2019 ASP.NET Core のスキャフォールディングされた API コントローラー](media/vs-2019/vs2019-add-scaffold-api.png)

## <a name="reviewing-the-generated-controller"></a>生成されたコントローラーを確認する

生成されたコードには、新しいコントローラー クラスが含まれています。 クラス定義の上部に、2 つの属性があります。

```csharp
[Route("api/[controller]")]
[ApiController]
public class GamesController : ControllerBase
```

最初のものは、このコントローラー内のアクションのルートが `api/[controller]` になるように指定します。つまり、コントローラーに `GamesController` という名前が付けられた場合、そのルートは `api/Games` になります。

2 番目の属性である `[ApiController]` は、いくつかの有用な検証を追加します。たとえば、すべてのアクション メソッドに独自の `[Route]` 属性が含まれていることを確認します。

```csharp
public class GamesController : ControllerBase
{
    private readonly AppDbContext _context;

    public GamesController(AppDbContext context)
    {
        _context = context;
    }
```

このコントローラーでは、そのコンス トラクターに渡された既存の `AppDbContext` が使用されます。 各アクションは、このフィールドを使用して、アプリケーションのデータを操作します。

```csharp
// GET: api/Games
[HttpGet]
public IEnumerable<Game> GetGame()
{
    return _context.Game;
}
```

最初のメソッドは単純な GET 要求であり、`[HttpGet]` 属性を使用するように指定されています。 パラメーターは使用されず、データベース内のすべてのゲームの一覧が返されます。

```csharp
// GET: api/Games/5
[HttpGet("{id}")]
public async Task<IActionResult> GetGame([FromRoute] int id)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    var game = await _context.Game.FindAsync(id);

    if (game == null)
    {
        return NotFound();
    }

    return Ok(game);
}
```

次のメソッドで `{id}` がルートに指定され、それが `/` の後ろに追加されます。これにより、上部のコメントに示されているように、完全なルートは `api/Games/5` のようになります。 `id` の入力は、メソッドの `id` パラメーターにマップされます。 メソッド内では、モデルが無効な場合は `BadRequest` 結果が返されます。 それ以外の場合は、EF によって、提供された `id` と一致するレコードの検出が試行されます。 検出できない場合は `NotFound` 結果が返され、それ以外の場合は適切な `Game` レコードが返されます。

```csharp
// PUT: api/Games/5
[HttpPut("{id}")]
public async Task<IActionResult> PutGame([FromRoute] int id, [FromBody] Game game)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    if (id != game.Id)
    {
        return BadRequest();
    }

    _context.Entry(game).State = EntityState.Modified;

    try
    {
        await _context.SaveChangesAsync();
    }
    catch (DbUpdateConcurrencyException)
    {
        if (!GameExists(id))
        {
            return NotFound();
        }
        else
        {
            throw;
        }
    }

    return NoContent();
}
```

次に、API に対して行われた `[HttpPut]` 要求を使用して、更新プログラムが実行されます。 要求の本文に新しい `Game` レコードが提供されます。 いくつかの検証とリモート チェックが実行され、すべてが成功した場合は、要求の本文内に提供された値を使用してデータベース内のレコードが更新されます。 それ以外の場合は、適切なエラー応答が返されます。

```csharp
// POST: api/Games
[HttpPost]
public async Task<IActionResult> PostGame([FromBody] Game game)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    _context.Game.Add(game);
    await _context.SaveChangesAsync();

    return CreatedAtAction("GetGame", new { id = game.Id }, game);
}
```

`[HttpPost]` 要求を使用して、システムに新しいレコードが追加されます。 `[HttpPut]` と同じように、レコードが要求の本文に追加されます。 有効な場合は、EF Core によってデータベースにレコードが追加され、更新されたレコード (そのデータベースで生成された ID 付き) とレコードへのリンクがアクションによって API に返されます。

```csharp
// DELETE: api/Games/5
[HttpDelete("{id}")]
public async Task<IActionResult> DeleteGame([FromRoute] int id)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    var game = await _context.Game.FindAsync(id);
    if (game == null)
    {
        return NotFound();
    }

    _context.Game.Remove(game);
    await _context.SaveChangesAsync();

    return Ok(game);
}
```

最後に、`[HttpDelete]` ルートと ID を使用して、レコードが削除されます。 要求が有効であり、指定された ID のレコードが存在する場合は、EF Core によってデータベースからそれが削除されます。

## <a name="adding-swagger"></a>Swagger の追加

Swagger は API のドキュメンテーションとテストを行うためのツールであり、サービスとミドルウェアのセットとして ASP.NET Core アプリに追加できます。 これを行うには、プロジェクトを右クリックし、 **[NuGet パッケージの管理]** をクリックします。 次に、 **[参照]** をクリックし、`Swashbuckle.AspNetCore` を検索して、4.0.1 バージョンをインストールします。

![Visual Studio 2019 - Nuget から Swashbuckle を追加する](media/vs-2019/vs2019-nuget-swashbuckle.png)

インストールされたら、`Startup.cs` を開き、`ConfigureServices` メソッドの末尾に以下を追加します。

```csharp
services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new Info { Title = "My API", Version = "v1" });
});
```

ファイルの先頭に `using Swashbuckle.AspNetCore.Swagger;` も追加する必要があります。

次に、`Configure` メソッドの `UseMvc` の直前に、以下を追加します。

```csharp
// Enable middleware to serve generated Swagger as a JSON endpoint.
app.UseSwagger();

// Enable middleware to serve swagger-ui (HTML, JS, CSS, etc.), 
// specifying the Swagger JSON endpoint.
app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
});
```

これで、アプリをビルドして実行できます。 ブラウザーのアドレス バーを使用して `/swagger` に移動します。 自分のアプリの API エンドポイントとモデルの一覧が表示されます。 

![Visual Studio 2019 - ブラウザーに表示された Swagger ページ](media/vs-2019/vs2019-swagger-browser.png)

Games の下のエンドポイント、`Try it out``Execute` の順にクリックして 異なるエンドポイントがどのように動作するかを確認します。

## <a name="next-steps"></a>次の手順

次のビデオで、アプリを Azure にデプロイする方法を学習します。

[手順 5:Azure に ASP.NET Core アプリをデプロイする](tutorial-aspnet-core-ef-step-05.md)

## <a name="see-also"></a>関連項目

- [Swashbuckle と ASP.NET Core の概要](/aspnet/core/tutorials/getting-started-with-swashbuckle?view=aspnetcore-2.2&tabs=visual-studio)
- [Swagger/OpenAPI を使用する ASP.NET Core Web API のヘルプ ページ](/aspnet/core/tutorials/web-api-help-pages-using-swagger?view=aspnetcore-2.2)