---
title: codespace をカスタマイズする (プレビュー)
description: codespace をカスタマイズする方法について説明します。
ms.topic: how-to
ms.date: 09/21/2020
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: f63dc4989a59256a0a3ad59491b2290912ffd2f8
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90862358"
---
# <a name="how-to-customize-a-codespace-preview"></a>codespace をカスタマイズする方法 (プレビュー)

GitHub Codespaces では、クラウド内に完全な開発環境を提供しています。 Visual Studio 2019 を使用した Windows ベースの開発の場合、GitHub Codespaces の既定のインスタンスを出発点として使うことをお勧めしますが、特定のプロジェクトに合わせて環境をカスタマイズすることもできます。

## <a name="installed-software"></a>インストール済みソフトウェア

Windows codespace には、多くのフレームワークとツールが既にインストールされているため、すぐに使い始めることができます。 すべての Windows codespace 環境で使用できるアプリケーションと機能を次の表に示します。

| アプリ                                         | パスの別名 | Version            |
|---------------------------------------------|------------|--------------------|
| .NET                                        | 該当なし        | 4.8                |
| .NET Core ランタイム                           | dotnet     | 2.1、3.1           |
| .NET Core SDK                               | dotnet     | 2.1、3.1.3、3.1.4  |
| Azure CLI                                   | az         | 2.5                |
| Chocolatey                                  | choco      | 0.10.15            |
| CMake                                       | cmake      | 3.17               |
| Git                                         | git        | 2.26               |
| Microsoft build                             | msbuild    | 16.7               |
| Microsoft SQL Server Express Edition 2019   | 該当なし        | 15.0               |
| Ninja                                       | ninja      | 1.8.2              |
| Node.js                                     | node       | 12.16              |
| NPM                                         | npm        | 6.14               |
| Python                                      | Python     | 3.7                |
| VC Package Manager                          | vcpkg      | 2020.02            |
| Windows SDK                                 | 該当なし        | 10.0.18362         |

上記の一覧はすべてを網羅したものではありません。Visual Studio によってインストールされる多くのツール (IISExpress など) が除外されています。 また、上記とは異なるマイナー バージョンまたはパッチ バージョンがコンポーネントに含まれている場合があります。

プレインストールされているフレームワークとツールにの詳細については、後述する「[インストールされているソフトウェアの詳細](#installed-software-specifics)」セクションを参照してください。

## <a name="modifications-to-a-codespace"></a>codespace に対する変更
 
codespace を作成すると、GitHub Codespaces で codespace インスタンスを使用できる間は、その特定の codespace に対する変更が保持されます。 追加のリポジトリをクローンし、ツールとアプリケーション ジェネレーターをインストールし、他の開発資産を追加することができます。これらの変更は、codespace が一時停止されている場合でも保持されます。 ただし、codespace を削除すると、変更はすべて失われます。

> [!NOTE]
> codespace を削除すると、codespace 内のローカル リポジトリ (保留中またはコミット済み) に対する変更は失われます。 codespace を削除する前に、必ずリポジトリに対する変更をリモートの場所にプッシュしてください。

Visual Studio を使用して codespace に接続している間は、Visual Studio ターミナルを使用してコマンドライン ツールを実行できます。 ローカルの管理者アカウントで、PowerShell または Windows の管理者特権のコマンド プロンプトを使用できます。 Visual Studio ターミナルの詳細については、[Visual Studio ターミナルに関するお知らせのブログ](https://devblogs.microsoft.com/visualstudio/say-hello-to-the-new-visual-studio-terminal/)を参照してください。

## <a name="customize-a-codespace"></a>Codespace をカスタマイズする

GitHub Codespaces の真価は、自分だけでなくチームの作業に合わせてカスタマイズされた、再現可能な独自の開発環境をクラウドに作成できるようになったときに発揮されます。 既定の GitHub Codespaces インスタンスを基に構築することで、新しい codespace を作成するときにインストールおよび構成する内容をカスタマイズできます。

次のセクションでは、 *.devcontainer.json* および *.devinit.json* ファイルを使用した 2 つの codespace の構成方法について説明します。 これらのファイルを使用すると、codespace のインストール フレームワークとツールを構成できます。また、リポジトリに追加すると、そのリポジトリに基づいて codespace を作成した誰もが同じリモート開発環境を持ちます。

## <a name="customize-with-devcontainerjson"></a>devcontainer.json を使用してカスタマイズする

codespace が作成されると、GitHub Codespaces では、リポジトリのルートにある [*devcontainers.json*](https://code.visualstudio.com/docs/remote/devcontainerjson-reference) ファイルが検索され、その設定が使用され、codespace またはそれに接続しているクライアント インスタンス (ブラウザーベースのエディター、Visual Studio、または Visual Studio Code) がカスタマイズされます。 ほとんどの *devcontainer.json* 設定は Linux ベースの codespace または他の 2 つのクライアントに適用されますが、一部は Windows codespace と Visual Studio に使用できます。

*devcontainer.json* ファイルは、次に示すリポジトリ内の 2 つの場所のいずれかに配置できます。

1. *{repository-root}/.devcontainer.json*
2. *{repository-root}/.devcontainer/devcontainer.json*

GitHub Codespaces は、次の *devcontainer.json* プロパティをサポートしています。 Visual Studio Code 固有の一部のプロパティは、Visual Studio に加えて他のクライアントを使用して codespace に接続する場合に役立ちます。 

* `extensions` - インストールする必要がある [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/vscode) 拡張機能の配列。
* `settings` - 適用する一連の [Visual Studio Code 設定](https://code.visualstudio.com/docs/getstarted/settings)。
* `forwardPorts` - codespace の実行時にローカルに自動的に転送されるポートまたはポートの配列。
* `postCreateCommand` - codespace の作成後に実行するコマンド文字列またはコマンド引数の一覧。

> [!NOTE]
> **devcontainer.json** ファイルは、Visual Studio Code の[リモート開発](https://code.visualstudio.com/docs/remote/remote-overview)をサポートするためにも使用され、このドキュメントでは説明されていない他のプロパティがあります。 このような他のプロパティをファイルに追加しても問題ありませんが、Codespaces では無視されます。 詳細については、code.visualstudio.com の [devcontainer.json リファレンス](https://code.visualstudio.com/docs/remote/devcontainerjson-reference)を参照してください。

## <a name="customize-with-devinit"></a>devinit を使用してカスタマイズする

[devinit](../../devinit/getting-started-with-devinit.md) は Windows codespace に含まれているコマンドライン ツールであり、フレームワークとツールを環境にインストールすることができます。 コマンド プロンプトから手動で実行できますが (`devinit -t require-dotnetcoresdk`)、その真価は、codespace を作成するたびに同様の codespace を構成できるカスタムの [ *.devinit.json* ](../../devinit/devinit-json.md) ファイルを作成することにあります。

`devinit` には、SQL Server や Azure CLI などの特定の項目をインストールし、chocolatey、npm、vcpkg などの一般的なパッケージ マネージャーを実行するための一連のツールが含まれています。 `devinit` ツールの詳細な一覧については、「[利用できるツール](../../devinit/devinit-tool-list.md)」のドキュメントを参照してください。

### <a name="devinitjson"></a>devinit.json

`devinit` コマンド ラインを直接実行することもできますが、実行する一連の `devinit` ツールを記述した [*devinit.json*](../../devinit/devinit-json.md) 構成ファイルを作成することをお勧めします。 

たとえば、[.NET Core SDK](https://docs.microsoft.com/dotnet/core/sdk) をインストールする場合、 *.devinit.json* は次のようになります。

```json
{
    "run": [
        {
            "comments": "We need the .NET Core SDK."
            "tool": "require-dotnetcoresdk"
        }
    ]
}
```

プロジェクトのルートで *.devinit.json* ファイルを作成すると、`devinit init` を実行したときに使用されます。 既定では、`devinit.exe` によって次の場所にあるファイルが検索されます。

1. *{current-directory}\\.devinit.json*
2. *{current-directory}\\.devinit\devinit.json*

### <a name="running-devinit-when-creating-a-codespace"></a>codespace の作成時に devinit を実行する

*devcontainers.json* ファイルの `postCreateCommand` プロパティを使用して、codespace の作成後に `devinit` を実行するように GitHub Codespaces に指示することができます。 前述のように、GitHub Codespaces では、codespace またはクライアント インスタンスをカスタマイズするために、クローンされたリポジトリ内にある *devcontainer.json* ファイルが検索され、`postCreateCommand` プロパティに記述されているコマンドが実行されます。

`devinit init` を指定すると、*devinit.json* 構成を使用して `devinit` が実行されます。

```json
{
  "postCreateCommand": "devinit init"
}
```

### <a name="an-example"></a>例

.NET Core Entity Framework コマンドライン ツール `dotnet-ef` をインストールする簡単な例を次に示します。

**devcontainer.json**

リポジトリのルートにある *.devinit.json* ファイルの内容。 

```json
{
  "postCreateCommand": "devinit init"
}
```

**devinit.json**

*.devinit.json* ファイルの内容。 このファイルは、 *.devcontainer.json* と同じフォルダーに存在する必要があります。

```json
{
    "run": [
        {
            "comments": "Install the Entity Framework tools",
            "tool": "dotnet-toolinstall",
            "input": "dotnet-ef",
        }
     ]
}
```

その他の `devinit` の例については、`devinit` の「[サンプル リスト](../../devinit/sample-readme.md)」を参照してください。

## <a name="port-forwarding"></a>ポート フォワーディング

GitHub Codespaces では、ポート フォワーディングによって、リモート環境で実行されているアプリケーションとサービスにアクセスできます。 既定では、セキュリティ上の理由からポートは転送されません。 ただし、特定のポートを指定して codespace で開くことができます。

### <a name="configure-port-forwarding"></a>ポート転送の構成

特定のリポジトリに対して既定で転送する必要があるポートが 1 つ以上ある場合は、*devcontainer.json* で `forwardPorts` プロパティを使用して構成することができます。

* `forwardPorts` - 環境の実行時にローカルに自動的に転送されるポートまたはポートの配列。

## <a name="installed-software-specifics"></a>インストールされているソフトウェアの詳細

### <a name="microsoft-sql-server"></a>Microsoft SQL Server

Microsoft SQL Server 2019 Express Edition は、Windows codespace 環境でローカル サービス (localdb) として使用可能であり、動作しています。 現在のユーザー (アプリと Visual Studio ターミナルの実行に使用しているもの) には、SQL サーバーに対する SQL 管理者権限があります。 サーバーを管理するには、Visual Studio ターミナルで PowerShell を使用するか、`dotnet-ef` などの他のコマンドライン ツールを使用する必要があります。 現在、SQL Server Management Studio やその他のリモート管理ツールは使用できません。

#### <a name="example-connection-string"></a>接続文字列の例

ローカルの MS SQL サーバーに接続する接続文字列の例を次に示します。

```csharp
"Server=(LocalDB);Integrated Security=true;"
```

### <a name="azure-cli"></a>Azure CLI

Azure CLI はすべての Windows codespace 環境にインストールされてあり、パスで `az` と指定して使用できます。

#### <a name="using-azure-resources"></a>Azure リソースの使用

Azure Active Directory ID を使用して、Azure リソースに対してアプリケーションを認証する場合は、最初に Visual Studio ターミナルから Azure にサインインする必要があります。 サインインするには、Azure CLI `login` コマンドをデバイスのサインイン フローで使用します (次の例を参照してください)。 サインインすると、アプリケーションとターミナル セッションでその ID を使用できるようになります。

```powershell
> az login --use-device-code
```

詳細については、Azure CLI [ドキュメント](/cli/azure/reference-index#az_login)の `az login` コマンドに関する説明を参照してください。

## <a name="see-also"></a>関連項目

- [GitHub Codespaces とは](codespaces-overview.md)
- [codespace で Visual Studio を使用する方法](use-visual-studio-with-codespaces.md)