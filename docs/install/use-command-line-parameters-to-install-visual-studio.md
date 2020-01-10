---
title: コマンド ライン パラメーターを使用して Visual Studio をインストールする
titleSuffix: ''
description: コマンド ライン パラメーターを使用して、Visual Studio のインストールを制御またはカスタマイズする方法を説明します。
ms.date: 10/22/2019
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- command-line parameters
- switches
- command prompt
ms.assetid: 480f3cb4-d873-434e-a8bf-82cff7401cf2
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 6d985266679d70f24ca2b40077549b5c3354b7f4
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590944"
---
# <a name="use-command-line-parameters-to-install-visual-studio"></a>コマンド ライン パラメーターを使用して Visual Studio をインストールする

コマンド プロンプトから Visual Studio をインストールする場合、さまざまなコマンド ライン パラメーターを使用してインストールを管理またはカスタマイズすることができます。 コマンド ラインから、次の操作を行うことができます。

- 特定のオプションをあらかじめ選択してインストールする。
- インストール プロセスを自動化する。
- 後で使用できるようにインストール ファイルのキャッシュ (レイアウト) を作成する。

コマンド ライン オプションは、セットアップ ブートストラップという、ダウンロード プロセスを開始する小さなファイル (1 MB) と組み合わせて使用されます。 ブートストラップは、Visual Studio サイトからダウンロードしたときに起動される最初の実行可能ファイルです。

::: moniker range="vs-2017"

Visual Studio 2017 のブートストラップを取得するには、その方法の詳細について、[**以前のバージョンの Visual Studio**](https://visualstudio.microsoft.com/vs/older-downloads/) のダウンロード ページを参照してください。

::: moniker-end

::: moniker range="vs-2019"

次のリンクから、インストールする製品エディションに応じた最新リリースのブートストラップを直接取得できます。

- [Visual Studio 2019 Enterprise](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019+rc)
- [Visual Studio 2019 Professional](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019+rc)
- [Visual Studio 2019 Community](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019+rc)

::: moniker-end


ブートストラップ ファイルは、次のいずれかのファイル名と一致しているか、似たものであるはずです。

* vs_enterprise.exe
* vs_professional.exe
* vs_community.exe

>[!TIP]
>前にブートストラップ ファイルをダウンロードしてあり、そのバージョンを確認したい場合は、次のようにします。 Windows でエクスプローラーを開き、ブートストラップ ファイルを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを選択し、 **[製品バージョン]** の値を表示します。 この値に対する Visual Studio のリリースを調べるには、「[Visual Studio のビルド番号とリリース日](visual-studio-build-numbers-and-release-dates.md)」ページを参照してください。

## <a name="command-line-parameters"></a>コマンド ライン パラメーター

 Visual Studio のコマンド ライン パラメーターでは、大文字と小文字は区別されません。

> 構文: `vs_enterprise.exe [command] <options>...`

`vs_enterprise.exe` は、必要に応じてインストールする製品エディションに置き換えてください。 (または、`vs_installer.exe` を使用することができます。)

>[!TIP]
> コマンド ラインを使用して Visual Studio をインストールする方法の他の例については、[コマンド ライン パラメーターの例](command-line-parameter-examples.md)に関するページをご覧ください。

::: moniker range="vs-2017"

| **コマンド** | **説明** |
| ----------------------- | --------------- |
| (空白) | 製品をインストールします。 |
| `modify` | インストールされている製品を変更します。 |
| `update` | インストールされている製品を更新します。 |
| `repair` | インストールされている製品を修復します。 |
| `uninstall` | インストールされている製品をアンインストールします。 |
| `export` | **バージョン 15.9 の新機能**:インストールの選択をインストール構成ファイルにエクスポートします。 **注**:vs_installer.exe でのみ使用できます。 |

::: moniker-end

::: moniker range="vs-2019"

| **コマンド** | **説明** |
| ----------------------- | --------------- |
| (空白) | 製品をインストールします。 |
| `modify` | インストールされている製品を変更します。 |
| `update` | インストールされている製品を更新します。 |
| `repair` | インストールされている製品を修復します。 |
| `uninstall` | インストールされている製品をアンインストールします。 |
| `export` | インストールの選択をインストール構成ファイルにエクスポートします。 **注**:vs_installer.exe でのみ使用できます。 |

::: moniker-end

## <a name="install-options"></a>インストール オプション

::: moniker range="vs-2017"

| **インストール オプション** | **説明** |
| ----------------------- | --------------- |
| `--installPath <dir>` | 操作するインスタンスのインストール ディレクトリです。 インストール コマンドの場合、これは**省略可能**で、インスタンスがインストールされる場所になります。 その他のコマンドではこれは**必須**で、以前にインストール済みのインスタンスがインストールされた場所になります。 |
| `--addProductLang <language-locale>` | **省略可能**:インストールまたは変更操作時に、製品にインストールされる UI 言語パックを決定します。 コマンド ラインに複数回指定して複数の言語パックを追加できます。 指定しない場合、インストール時にはコンピューターのロケールが使用されます。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--removeProductLang <language-locale>` | **省略可能**:インストールまたは変更操作時に、製品から削除される UI 言語パックを決定します。 コマンド ラインに複数回指定して複数の言語パックを追加できます。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--add <one or more workload or component IDs>` | **省略可能**:1 つ以上のワークロード ID またはコンポーネント ID を追加します。 成果物の必須のコンポーネントはインストールされますが、推奨されるコンポーネントまたは省略可能なコンポーネントはインストールされません。 `--includeRecommended` や `--includeOptional` を使用して、他のコンポーネントをグローバルに制御できます。 複数のワークロードやコンポーネントを含める場合、`--add` コマンドを繰り返します (例: `--add Workload1 --add Workload2`)。 詳細に制御するために、ID に `;includeRecommended` または `;includeOptional` を追加できます (例: `--add Workload1;includeRecommended` または `--add Workload2;includeRecommended;includeOptional`)。 詳しくは、[ワークロード ID とコンポーネント ID](workload-and-component-ids.md) に関するページをご覧ください。 必要に応じて、このオプションを繰り返すことができます。|
| `--remove <one or more workload or component IDs>` | **省略可能**:1 つ以上のワークロード ID またはコンポーネント ID を削除します。 詳しくは、[ワークロード ID とコンポーネント ID](workload-and-component-ids.md) に関するページをご覧ください。 必要に応じて、このオプションを繰り返すことができます。|
| `--in <path>` | **省略可能**:応答ファイルへの URI またはパスです。  |
| `--all` | **省略可能**:製品のすべてのワークロードおよびコンポーネントをインストールするかどうかを指定します。 |
| `--allWorkloads` | **省略可能**:すべてのワークロードとコンポーネントをインストールし、推奨されるコンポーネントと省略可能なコンポーネントはインストールしません。 |
| `--includeRecommended` | **省略可能**:インストールされているワークロードの推奨されるコンポーネントを含めますが、オプションのコンポーネントは含めません。 ワークロードは、`--allWorkloads` または `--add` のいずれかで指定されます。 |
| `--includeOptional` | **省略可能**:インストールされているワークロードのオプションのコンポーネントを含めますが、推奨されるコンポーネントは含めません。 ワークロードは、`--allWorkloads` または `--add` のいずれかで指定されます。  |
| `--quiet, -q` | **省略可能**:インストールの実行中にユーザー インターフェイスを表示しません。 |
| `--passive, -p` | **省略可能**:ユーザー インターフェイスを表示しますが、ユーザーに対話式操作を要求することはありません。 |
| `--norestart` | **省略可能**:指定した場合、`--passive` または `--quiet` が含まれるコマンドでは、コンピューターは自動的に再起動されません (必要な場合)。  `--passive` または `--quiet` のどちらも指定されていない場合は、無視されます。  |
| `--nickname <name>` | **省略可能**:インストールされている製品に割り当てるニックネームを定義します。 ニックネームは 10 文字を超えることはできません。  |
| `--productKey` | **省略可能**:インストールされる製品に使用するプロダクト キーを定義します。 `xxxxx-xxxxx-xxxxx-xxxxx-xxxxx` または `xxxxxxxxxxxxxxxxxxxxxxxxx` のいずれかの形式の英数字 25 文字で構成されます。 |
| `--help, --?, -h, -?` | このページのオフライン バージョンを表示します。 |
| `--config <path>` | **省略可能**および **15.9 の新機能**:インストールまたは変更の操作中に、以前に保存したインストール構成ファイルに基づいて、追加するワークロードおよびコンポーネントを決定します。 この操作は追加式で、ワークロードやコンポーネントがファイル内に存在しない場合、削除されることはありません。 また、製品に適用されない項目は追加されません。 エクスポート操作中に、インストール構成ファイルの保存場所を決定します。 |

::: moniker-end

::: moniker range="vs-2019"

| **インストール オプション** | **説明** |
| ----------------------- | --------------- |
| `--installPath <dir>` | 操作するインスタンスのインストール ディレクトリです。 インストール コマンドの場合、これは**省略可能**で、インスタンスがインストールされる場所になります。 その他のコマンドではこれは**必須**で、以前にインストール済みのインスタンスがインストールされた場所になります。 |
| `--addProductLang <language-locale>` | **省略可能**:インストールまたは変更操作時に、製品にインストールされる UI 言語パックを決定します。 コマンド ラインに複数回指定して複数の言語パックを追加できます。 指定しない場合、インストール時にはコンピューターのロケールが使用されます。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--removeProductLang <language-locale>` | **省略可能**:インストールまたは変更操作時に、製品から削除される UI 言語パックを決定します。 コマンド ラインに複数回指定して複数の言語パックを追加できます。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--add <one or more workload or component IDs>` | **省略可能**:1 つ以上のワークロード ID またはコンポーネント ID を追加します。 成果物の必須のコンポーネントはインストールされますが、推奨されるコンポーネントまたは省略可能なコンポーネントはインストールされません。 `--includeRecommended` や `--includeOptional` を使用して、他のコンポーネントをグローバルに制御できます。 複数のワークロードやコンポーネントを含める場合、`--add` コマンドを繰り返します (例: `--add Workload1 --add Workload2`)。 詳細に制御するために、ID に `;includeRecommended` または `;includeOptional` を追加できます (例: `--add Workload1;includeRecommended` または `--add Workload2;includeRecommended;includeOptional`)。 詳しくは、[ワークロード ID とコンポーネント ID](workload-and-component-ids.md) に関するページをご覧ください。 必要に応じて、このオプションを繰り返すことができます。|
| `--remove <one or more workload or component IDs>` | **省略可能**:1 つ以上のワークロード ID またはコンポーネント ID を削除します。 詳しくは、[ワークロード ID とコンポーネント ID](workload-and-component-ids.md) に関するページをご覧ください。 必要に応じて、このオプションを繰り返すことができます。|
| `--in <path>` | **省略可能**:応答ファイルへの URI またはパスです。  |
| `--all` | **省略可能**:製品のすべてのワークロードおよびコンポーネントをインストールするかどうかを指定します。 |
| `--allWorkloads` | **省略可能**:すべてのワークロードとコンポーネントをインストールし、推奨されるコンポーネントと省略可能なコンポーネントはインストールしません。 |
| `--includeRecommended` | **省略可能**:インストールされているワークロードの推奨されるコンポーネントを含めますが、オプションのコンポーネントは含めません。 ワークロードは、`--allWorkloads` または `--add` のいずれかで指定されます。 |
| `--includeOptional` | **省略可能**:インストールされているワークロードのオプションのコンポーネントを含めますが、推奨されるコンポーネントは含めません。 ワークロードは、`--allWorkloads` または `--add` のいずれかで指定されます。  |
| `--quiet, -q` | **省略可能**:インストールの実行中にユーザー インターフェイスを表示しません。 |
| `--passive, -p` | **省略可能**:ユーザー インターフェイスを表示しますが、ユーザーに対話式操作を要求することはありません。 |
| `--norestart` | **省略可能**:指定した場合、`--passive` または `--quiet` が含まれるコマンドでは、コンピューターは自動的に再起動されません (必要な場合)。  `--passive` または `--quiet` のどちらも指定されていない場合は、無視されます。  |
| `--nickname <name>` | **省略可能**:インストールされている製品に割り当てるニックネームを定義します。 ニックネームは 10 文字を超えることはできません。  |
| `--productKey` | **省略可能**:インストールされる製品に使用するプロダクト キーを定義します。 `xxxxx-xxxxx-xxxxx-xxxxx-xxxxx` または `xxxxxxxxxxxxxxxxxxxxxxxxx` のいずれかの形式の英数字 25 文字で構成されます。 |
| `--help, --?, -h, -?` | このページのオフライン バージョンを表示します。 |
| `--config <path>` | **省略可能**:インストールまたは変更の操作中に、以前に保存したインストール構成ファイルに基づいて、追加するワークロードおよびコンポーネントを決定します。 この操作は追加式で、ワークロードやコンポーネントがファイル内に存在しない場合、削除されることはありません。 また、製品に適用されない項目は追加されません。 エクスポート操作中に、インストール構成ファイルの保存場所を決定します。 |

::: moniker-end

> [!IMPORTANT]
> 複数のワークロードとコンポーネントを指定する場合、項目ごとに `--add` または `--remove` コマンド ライン スイッチを繰り返す必要があります。

## <a name="layout-options"></a>レイアウト オプション

::: moniker range="vs-2017"

| **レイアウト オプション** | **説明** |
| ----------------------- | --------------- |
| `--layout <dir>` | オフライン インストールのキャッシュを作成するディレクトリを指定します。 詳細については、「[Visual Studio のネットワーク ベース インストールを作成する](create-a-network-installation-of-visual-studio.md)」をご覧ください。|
| `--lang <one or more language-locales>` | **省略可能**:`--layout` とともに使用して、指定した言語でのリソース パッケージによるオフライン インストール キャッシュを準備します。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--add <one or more workload or component IDs>` | **省略可能**:1 つ以上のワークロード ID またはコンポーネント ID を追加します。 成果物の必須のコンポーネントはインストールされますが、推奨されるコンポーネントまたは省略可能なコンポーネントはインストールされません。 `--includeRecommended` や `--includeOptional` を使用して、他のコンポーネントをグローバルに制御できます。 詳細に制御するために、ID に `;includeRecommended` または `;includeOptional` を追加できます (例: `--add Workload1;includeRecommended` または `--add Workload2;includeOptional`)。 詳しくは、[ワークロード ID とコンポーネント ID](workload-and-component-ids.md) に関するページをご覧ください。 <br/>**注**:`--add` を使用する場合、指定したワークロードとコンポーネント、およびその依存関係のみがダウンロードされます。 `--add` を指定しない場合は、すべてのワークロードとコンポーネントがレイアウトにダウンロードされます。|
| `--includeRecommended` | **省略可能**:インストールされているワークロードの推奨されるコンポーネントを含めますが、オプションのコンポーネントは含めません。 ワークロードは、`--allWorkloads` または `--add` のいずれかで指定されます。 |
| `--includeOptional` | **省略可能**:レイアウトに含まれるワークロードに、推奨*および*省略可能なコンポーネントが含まれます。 ワークロードは、`--add` で指定されます。  |
| `--keepLayoutVersion` | **15.3 の新機能、省略可能**:レイアウトのバージョンを更新することなく、レイアウトに変更を適用します。 |
| `--verify` | **15.3 の新機能、省略可能**:レイアウトの内容を確認します。 破損または欠落しているすべてのファイルが一覧に表示されます。 |
| `--fix` | **15.3 の新機能、省略可能**:レイアウトの内容を確認します。 いずれかのファイルが破損または欠落している場合は、再ダウンロードします。 レイアウトを修正するには、インターネットへのアクセスが必要です。 |
| `--clean <one or more paths to catalogs>` | **15.3 の新機能、省略可能**:新しいバージョンに更新されたレイアウトから古いバージョンのコンポーネントを削除します。 |

| **高度なインストール オプション** | **説明** |
| ----------------------- | --------------- |
| `--channelId <id>` | **省略可能**:インストールするインスタンスのチャネル ID です。 インストール コマンドでは必須です。`--installPath` が指定されている場合、他のコマンドでは無視されます。 |
| `--channelUri <uri>` | **省略可能**:チャネル マニフェストの URI です。 更新が不要な場合、`--channelUri` で存在しないファイル (たとえば、--channelUri C:\doesntExist.chman) を指定できます。 インストール コマンドに使用できます。その他のコマンドでは無視されます。 |
| `--installChannelUri <uri>` | **省略可能**:インストールに使用するチャネル マニフェストの URI です。 `--channelUri` で指定された URI (`--installChannelUri` を指定した場合は必ず指定する必要があります) は、更新プログラムを検出するために使用されます。 インストール コマンドに使用できます。その他のコマンドでは無視されます。 |
| `--installCatalogUri <uri>` | **省略可能**:インストールに使用するカタログ マニフェストの URI です。 これを指定すると、チャネル マネージャーは、インストール チャネル マニフェストの URI を使用する前に、この URI からカタログ マニフェストをダウンロードしようとします。 このパラメーターは、レイアウトのキャッシュが既にダウンロードされている製品カタログで作成される、オフライン インストールをサポートするために使用されます。 インストール コマンドに使用できます。その他のコマンドでは無視されます。 |
| `--productId <id>` | **省略可能**: インストールされるインスタンスの製品 ID です。 これは、通常のインストール条件では事前に設定されています。 |
| `--wait` | **省略可能**:インストールが完了し、終了コードが返されるまでプロセスは待機します。 このオプションは、インストールが完了するまで待ってから、そのインストールからのリターン コードを処理する必要があるインストールの自動化に役立ちます。 |
| `--locale <language-locale>` | **省略可能**:インストーラー自体のユーザー インターフェイスの表示言語を変更します。 設定は保持されます。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--cache` | **15.2 の新機能、省略可能**:指定した場合、インストールされた後、その後の修復用にパッケージが保持されます。 このオプションでは、その後のインストール、修復、または修正に使用されるグローバル ポリシー設定がオーバーライドされます。 既定のポリシーでは、パッケージをキャッシュします。 アンインストール コマンドでは、これは無視されます。 詳細については、「[disable or move the package cache](disable-or-move-the-package-cache.md)」 (パッケージ キャッシュの無効化または移動) を参照してください。 |
| `--nocache` | **15.2 の新機能、省略可能**:指定した場合、パッケージはインストールまたは修復された後、削除されます。 必要な場合にのみ、もう一度ダウンロードされ、使用後はもう一度削除されます。 このオプションでは、その後のインストール、修復、または修正に使用されるグローバル ポリシー設定がオーバーライドされます。 既定のポリシーでは、パッケージをキャッシュします。 アンインストール コマンドでは、これは無視されます。 詳細については、「[disable or move the package cache](disable-or-move-the-package-cache.md)」 (パッケージ キャッシュの無効化または移動) を参照してください。 |
| `--noUpdateInstaller` | **15.2 の新機能、省略可能**:指定した場合、quiet が指定されていると、インストーラーはインストーラー自体を更新しません。 インストーラーの更新が必要な場合に、noUpdateInstaller と quiet の両方が指定されていると、インストーラーはコマンドを失敗させて、0 以外の終了コードを返します。 |
| `--noWeb` | **15.3 の新機能、省略可能**:Visual Studio のセットアップでは、(存在する場合) レイアウト ディレクトリにあるファイルを使って Visual Studio がインストールされます。 ユーザーがレイアウトに含まれないコンポーネントをインストールしようとした場合、セットアップは失敗します。  詳細については、「[ネットワーク インストールから展開する](create-a-network-installation-of-visual-studio.md)」をご覧ください。 <br/><br/> **重要**: この切り替えによって、Visual Studio のセットアップで更新プログラムのチェックが行われなくなることはありません。 詳細については、「[ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)」をご覧ください。 |
| `--path <name>=<path>` | **15.7 の新機能、省略可能**:インストール用のカスタム インストール パスを指定するために使用します。 サポートされているパス名は、shared、cache、および install です。 |
| `--path cache=<path>` | **15.7 の新機能、省略可能**:指定した場所を使用してインストール ファイルをダウンロードします。 この場所は、Visual Studio を初めてインストールするときにのみ設定することができます。 例 : `--path cache="C:\VS\cache"` |
| `--path shared=<path>` | **15.7 の新機能、省略可能**:Visual Studio のサイド バイ サイド インストール用の共有ファイルが含まれています。 ツールおよび SDK については、このドライブ上の場所にインストールされるものもあれば、この設定をオーバーライドして、別のドライブにインストールされるものもあります。 例 : `--path shared="C:\VS\shared"` <br><br>重要 : これは Visual Studio を初めてインストールするときに 1 回のみ設定できます。 |
| `--path install=<path>` | **15.7 の新機能、省略可能**:これは、`–-installPath` に相当します。 具体的には、`--installPath "C:\VS"` と `--path install="C:\VS"` が等価です。 これらのコマンドは、一度に 1 つしか使用できません。 |

::: moniker-end

::: moniker range="vs-2019"

| **レイアウト オプション** | **説明** |
| ----------------------- | --------------- |
| `--layout <dir>` | オフライン インストールのキャッシュを作成するディレクトリを指定します。 詳細については、「[Visual Studio のネットワーク ベース インストールを作成する](create-a-network-installation-of-visual-studio.md)」をご覧ください。|
| `--lang <one or more language-locales>` | **省略可能**:`--layout` とともに使用して、指定した言語でのリソース パッケージによるオフライン インストール キャッシュを準備します。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--add <one or more workload or component IDs>` | **省略可能**:1 つ以上のワークロード ID またはコンポーネント ID を追加します。 成果物の必須のコンポーネントはインストールされますが、推奨されるコンポーネントまたは省略可能なコンポーネントはインストールされません。 `--includeRecommended` や `--includeOptional` を使用して、他のコンポーネントをグローバルに制御できます。 詳細に制御するために、ID に `;includeRecommended` または `;includeOptional` を追加できます (例: `--add Workload1;includeRecommended` または `--add Workload2;includeOptional`)。 詳しくは、[ワークロード ID とコンポーネント ID](workload-and-component-ids.md) に関するページをご覧ください。 <br/>**注**:`--add` を使用する場合、指定したワークロードとコンポーネント、およびその依存関係のみがダウンロードされます。 `--add` を指定しない場合は、すべてのワークロードとコンポーネントがレイアウトにダウンロードされます。|
| `--includeRecommended` | **省略可能**:インストールされているワークロードの推奨されるコンポーネントを含めますが、オプションのコンポーネントは含めません。 ワークロードは、`--allWorkloads` または `--add` のいずれかで指定されます。 |
| `--includeOptional` | **省略可能**:レイアウトに含まれるワークロードに、推奨*および*省略可能なコンポーネントが含まれます。 ワークロードは、`--add` で指定されます。  |
| `--keepLayoutVersion` | **省略可能**:レイアウトのバージョンを更新することなく、レイアウトに変更を適用します。 |
| `--verify` | **省略可能**:レイアウトの内容を確認します。 破損または欠落しているすべてのファイルが一覧に表示されます。 |
| `--fix` | **省略可能**:レイアウトの内容を確認します。  いずれかのファイルが破損または欠落している場合は、再ダウンロードします。 レイアウトを修正するには、インターネットへのアクセスが必要です。 |
| `--clean <one or more paths to catalogs>` | **省略可能**:新しいバージョンに更新されたレイアウトから古いバージョンのコンポーネントを削除します。 |

| **高度なインストール オプション** | **説明** |
| ----------------------- | --------------- |
| `--channelId <id>` | **省略可能**:インストールするインスタンスのチャネル ID です。 インストール コマンドでは必須です。`--installPath` が指定されている場合、他のコマンドでは無視されます。 |
| `--channelUri <uri>` | **省略可能**:チャネル マニフェストの URI です。 更新が不要な場合、`--channelUri` で存在しないファイル (たとえば、--channelUri C:\doesntExist.chman) を指定できます。 インストール コマンドに使用できます。その他のコマンドでは無視されます。 |
| `--installChannelUri <uri>` | **省略可能**:インストールに使用するチャネル マニフェストの URI です。 `--channelUri` で指定された URI (`--installChannelUri` を指定した場合は必ず指定する必要があります) は、更新プログラムを検出するために使用されます。 インストール コマンドに使用できます。その他のコマンドでは無視されます。 |
| `--installCatalogUri <uri>` | **省略可能**:インストールに使用するカタログ マニフェストの URI です。 これを指定すると、チャネル マネージャーは、インストール チャネル マニフェストの URI を使用する前に、この URI からカタログ マニフェストをダウンロードしようとします。 このパラメーターは、レイアウトのキャッシュが既にダウンロードされている製品カタログで作成される、オフライン インストールをサポートするために使用されます。 インストール コマンドに使用できます。その他のコマンドでは無視されます。 |
| `--productId <id>` | **省略可能**: インストールされるインスタンスの製品 ID です。 これは、通常のインストール条件では事前に設定されています。 |
| `--wait` | **省略可能**:インストールが完了し、終了コードが返されるまでプロセスは待機します。 このオプションは、インストールが完了するまで待ってから、そのインストールからのリターン コードを処理する必要があるインストールの自動化に役立ちます。 |
| `--locale <language-locale>` | **省略可能**:インストーラー自体のユーザー インターフェイスの表示言語を変更します。 設定は保持されます。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--cache` | **省略可能**:指定した場合、インストールされた後、その後の修復用にパッケージが保持されます。 このオプションでは、その後のインストール、修復、または修正に使用されるグローバル ポリシー設定がオーバーライドされます。 既定のポリシーでは、パッケージをキャッシュします。 アンインストール コマンドでは、これは無視されます。 詳細については、「[disable or move the package cache](disable-or-move-the-package-cache.md)」 (パッケージ キャッシュの無効化または移動) を参照してください。 |
| `--nocache` | **省略可能**:指定した場合、パッケージはインストールまたは修復された後、削除されます。 必要な場合にのみ、もう一度ダウンロードされ、使用後はもう一度削除されます。 このオプションでは、その後のインストール、修復、または修正に使用されるグローバル ポリシー設定がオーバーライドされます。 既定のポリシーでは、パッケージをキャッシュします。 アンインストール コマンドでは、これは無視されます。 詳細については、「[disable or move the package cache](disable-or-move-the-package-cache.md)」 (パッケージ キャッシュの無効化または移動) を参照してください。 |
| `--noUpdateInstaller` | **省略可能**:指定した場合、quiet が指定されていると、インストーラーはインストーラー自体を更新しません。 インストーラーの更新が必要な場合に、noUpdateInstaller と quiet の両方が指定されていると、インストーラーはコマンドを失敗させて、0 以外の終了コードを返します。 |
| `--noWeb` | **省略可能**:Visual Studio のセットアップでは、(存在する場合) レイアウト ディレクトリにあるファイルを使って Visual Studio がインストールされます。 ユーザーがレイアウトに含まれないコンポーネントをインストールしようとした場合、セットアップは失敗します。  詳細については、「[ネットワーク インストールから展開する](create-a-network-installation-of-visual-studio.md)」をご覧ください。 <br/><br/> **重要**: この切り替えによって、Visual Studio のセットアップで更新プログラムのチェックが行われなくなることはありません。 詳細については、「[ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)」をご覧ください。 **16.3.5 の新機能**: このスイッチにより、エラーが発生しなくなり、オフライン インストールや更新のパフォーマンスが向上します。|
| `--path <name>=<path>` | **省略可能**:インストール用のカスタム インストール パスを指定するために使用します。 サポートされているパス名は、shared、cache、および install です。 |
| `--path cache=<path>` | **省略可能**:指定した場所を使用してインストール ファイルをダウンロードします。 この場所は、Visual Studio を初めてインストールするときにのみ設定することができます。 例 : `--path cache="C:\VS\cache"` |
| `--path shared=<path>` | **省略可能**:Visual Studio のサイド バイ サイド インストール用の共有ファイルが含まれています。 ツールおよび SDK については、このドライブ上の場所にインストールされるものもあれば、この設定をオーバーライドして、別のドライブにインストールされるものもあります。 例 : `--path shared="C:\VS\shared"` <br><br>重要 : これは Visual Studio を初めてインストールするときに 1 回のみ設定できます。 |
| `--path install=<path>` | **省略可能**:これは、`–-installPath` に相当します。 具体的には、`--installPath "C:\VS"` と `--path install="C:\VS"` が等価です。 これらのコマンドは、一度に 1 つしか使用できません。 |

::: moniker-end

## <a name="list-of-workload-ids-and-component-ids"></a>ワークロード ID とコンポーネント ID の一覧

Visual Studio 製品ごとに並べられているワークロード ID とコンポーネント ID の一覧については、「[Visual Studio のワークロードとコンポーネント ID](workload-and-component-ids.md)」のページをご覧ください。

## <a name="list-of-language-locales"></a>言語ロケールの一覧

| **言語ロケール** | **Language** |
| ----------------------- | --------------- |
| Cs-cz | チェコ語 |
| De-de | ドイツ語 |
| En-us | 英語 |
| Es-es | スペイン語 |
| Fr-fr | フランス語 |
| It-it | イタリア語 |
| Ja-jp | 日本語 |
| Ko-kr | 韓国語 |
| Pl-pl | ポーランド語 |
| Pt-br | ポルトガル語 - ブラジル |
| Ru-ru | ロシア語 |
| Tr-tr | トルコ語 |
| Zh-cn | 中国語 - 簡体字 |
| Zh-tw | 中国語 - 繁体字 |

## <a name="error-codes"></a>エラー コード

操作の結果に応じて、`%ERRORLEVEL%` 環境変数は、次のいずれかの値に設定されます。

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

操作ごとに、インストールの進行状況を示す複数のログ ファイルが `%TEMP%` ディレクトリに生成されます。 フォルダーを日付で並べ替え、`dd_bootstrapper`、`dd_client`、`dd_setup` で始まるファイルを探します (それぞれブートストラップ、インストーラー アプリ、セットアップ エンジンを表します)。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

- [Visual Studio のインストールに使用するコマンド ライン パラメーターの例](command-line-parameter-examples.md)
- [Visual Studio のオフライン インストールを作成する](create-an-offline-installation-of-visual-studio.md)
- [応答ファイルで Visual Studio インストールを自動化する](automated-installation-with-response-file.md)
- [Visual Studio のワークロードとコンポーネント ID](workload-and-component-ids.md)
