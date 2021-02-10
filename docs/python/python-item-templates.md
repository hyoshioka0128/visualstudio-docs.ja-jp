---
title: Python プロジェクトの項目テンプレート
description: Visual Studio の [追加] > [新しい項目] ダイアログから利用できる、Python プロジェクトの項目テンプレートの参照一覧。
ms.date: 12/06/2018
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 23a79d0842592ff3ad68f63c2739a2af9847aaeb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99945163"
---
# <a name="python-item-templates"></a>Python 項目テンプレート

項目テンプレートは、**ソリューション エクスプローラー** のコンテキスト メニューにある **[プロジェクト]** > **[新しい項目の追加]** メニュー コマンドから、または **[追加]** > **[新しい項目]** コマンドから、Python プロジェクト内で利用できます。

![[新しい項目の追加] ダイアログ ボックス](media/project-item-templates.png)

項目に指定した名前を使用して、テンプレートは通常、プロジェクトで現在選択されているフォルダー内に 1 つ以上のファイルとフォルダーを作成します (フォルダーを右クリックしてコンテキスト メニューを開くと、自動的に該当のフォルダーが選択されます)。 項目を追加すると、Visual Studio プロジェクトに組み入れられ、項目が **ソリューション エクスプローラー** に表示されます。

次の表では、Python プロジェクト内の各項目テンプレートの効果を簡単に説明しています。

| テンプレート | テンプレートによって作成されるもの |
| --- | --- |
| **空の Python ファイル** | *.py* 拡張子の空のファイル。 |
| **Python クラス** | 単一の空の Python クラス定義を含む *.py* ファイル。 |
| **Python パッケージ** | *\_\_init\_\_.py* ファイルを含むフォルダー。 |
| **Python 単体テスト** | `unittest` フレームワークに基づく単体テストを 1 つ含む *.py* ファイル。ファイル内のテストを実行するための `unittest.main()` の呼び出しを含みます。 |
| **HTML ページ** | `<head>` および `<body>` 要素で構成される単一のページ構造を備えた *.html* ファイル。 |
| **JavaScript** | 空の *.js* ファイル。 |
| **スタイル シート** | `body` の空のスタイルを含む *.css* ファイル。 |
| **テキスト ファイル** | 空の *.txt* ファイル。 |
| **Django 1.9 アプリ**<br/>**Django 1.4 アプリ** | アプリ名のフォルダー。Django 1.9 の場合は、[「Visual Studio での Django の詳細情報」の手順 2-2](learn-django-in-visual-studio-step-02-create-an-app.md#step-2-1-create-an-app-with-a-default-structure) で説明したように、Django アプリの主要なファイルが含まれます。 Django 1.4 の場合は、*migrations* フォルダー、*admin.py* ファイル、*apps.py* ファイルが含まれません。 |
| **IronPython WPF ウィンドウ** | 2 つの横並びのファイルで構成される WPF ウィンドウ: 空の `<Grid>` 要素で `<Window>` を定義する *.xaml* ファイルと、`wpf` ライブラリを使用して XAML ファイルを読み込む、関連する *.py* ファイル。 通常は、IronPython プロジェクト テンプレートの 1 つを使用して作成されたプロジェクト内で使用されます。 [「Python プロジェクトの管理」の「プロジェクト テンプレート」のセクション](managing-python-projects-in-visual-studio.md#project-templates)をご覧ください。 |
| **Web ロール サポート ファイル** | プロジェクト ルートにある *bin* フォルダー (プロジェクト内で選択されたフォルダーとは関係ありません)。 Azure クラウド サービス Web ロールの既定のデプロイ スクリプトと *web.config* ファイルが格納されています。 また、テンプレートには、詳細を説明する *readme.html* ファイルが含まれています。 |
| **Worker ロールのサポート ファイル** | プロジェクト ルートにある *bin* フォルダー (プロジェクト内で選択されたフォルダーとは関係ありません)。 Azure クラウド サービス Worker ロールの既定のデプロイ スクリプトと *web.config* ファイルが格納されています。 また、テンプレートには、詳細を説明する *readme.html* ファイルが含まれています。 |
| **Azure web.config (FastCGI)** | 受信接続の処理に [WSGI](https://wsgi.readthedocs.io/en/latest/) オブジェクトを使うアプリ用のエントリを含む *web.config* ファイル。 このファイルは通常、IIS を実行している Web サーバーのルートに配置されます。 詳細については、[IIS 用のアプリの構成](configure-web-apps-for-iis-windows.md)に関連するページをご覧ください。 |
| **Azure web.config (HttpPlatformHandler)** | 受信接続のためのソケット上でリッスンするアプリのエントリを含む *web.config* ファイル。 このファイルは通常、Azure App Service などの IIS を実行している Web サーバーのルートにデプロイされます。 詳細については、[IIS 用のアプリの構成](configure-web-apps-for-iis-windows.md)に関連するページをご覧ください。 |
| **Azure 静的ファイルの web.config** | *web.config* ファイル。通常は *static* フォルダー (または、静的な項目を格納する他のフォルダー) に追加されて、そのフォルダーの Python 処理を無効にします。 この構成ファイルは、上記の FastCGI または HttpPlatformHandler 構成ファイルと組み合わせることで、機能します。 詳細については、[IIS 用のアプリの構成](configure-web-apps-for-iis-windows.md)に関連するページをご覧ください。 |
| **Azure リモート デバッグの web.config** | 非推奨です (Windows 用の Azure App Service 上でのリモート デバッグに使用されていましたが、現在ではサポートされていません)。 |

## <a name="see-also"></a>関連項目

- [Python プロジェクトの管理 - プロジェクト テンプレート](managing-python-projects-in-visual-studio.md#project-templates)
- [Python Web プロジェクト テンプレート](python-web-application-project-templates.md)
- [Azure App Service に発行する](publishing-python-web-applications-to-azure-from-visual-studio.md)
