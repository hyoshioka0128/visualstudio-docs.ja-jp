---
title: Python 用 Django Web プロジェクト テンプレート
description: Visual Studio では、Python で Django Web アプリケーションを短期間で作成するための包括的なテンプレートを提供します。
ms.date: 11/12/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 462c66229b6f28d281bf03650e4d22d0d1dab64f
ms.sourcegitcommit: f1dff6c4532c43b0444aa12ea57e90bb7dba6fba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104806044"
---
# <a name="django-web-project-template"></a>Django Web プロジェクト テンプレート
::: moniker range="vs-2017"
[Django](https://www.djangoproject.com/) は、高速、安全、スケーラブルな Web 開発用に設計されたハイレベルの Python フレームワークです。 Visual Studio の Python サポートには、Django ベースの Web アプリケーションの構造を設定するためのプロジェクト テンプレートがいくつか用意されています。 Visual Studio でテンプレートを使用するには、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択し、"Django" を探し、 **[空の Django Web プロジェクト]** 、 **[Django Web プロジェクト]** 、および **[ポーリング Django Web プロジェクト]** テンプレートから選択します。 すべてのテンプレートのチュートリアルについては、[Django チュートリアルの概要](learn-django-in-visual-studio-step-01-project-and-solution.md)に関するページを参照してください。
::: moniker-end
::: moniker range=">=vs-2019"
[Django](https://www.djangoproject.com/) は、高速、安全、スケーラブルな Web 開発用に設計されたハイレベルの Python フレームワークです。 Visual Studio の Python サポートには、Django ベースの Web アプリケーションの構造を設定するためのプロジェクト テンプレートがいくつか用意されています。 Visual Studio でテンプレートを使用するには、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択し、"Django" を探し、 **[空の Django Web プロジェクト]** または **[Django Web プロジェクト]** のいずれかのテンプレートを選択します。 すべてのテンプレートのチュートリアルについては、[Django チュートリアルの概要](learn-django-in-visual-studio-step-01-project-and-solution.md)に関するページを参照してください。
::: moniker-end
Visual Studio は、Django プロジェクトの完全な IntelliSense を提供します。

- テンプレートに渡されるコンテキスト変数:

    ![コンテキスト変数用の IntelliSense](media/template-django-intellisense.png)

- 組み込みとユーザー定義両方のタグ付けとフィルター処理:

    ![タグとフィルターの IntelliSense](media/template-django-intellisense-filter.png)

- 埋め込みの CSS と JavaScript の構文の色分け表示:

    ![CSS Intellisense](media/template-django-intellisense-css.png)

    ![JavaScript IntelliSense](media/template-django-intellisense-js.png)

また、Visual Studio は Django プロジェクトの完全な[デバッグ サポート](debugging-python-in-visual-studio.md)も提供します。

![ブレークポイント](media/template-django-debugging.png)

Django プロジェクトは *manage.py* ファイルで管理するのが一般的であり、Visual Studio でもそのようになっています。 エントリ ポイントとしてそのファイルの使用を止めると、基本的にプロジェクト ファイルは壊れます。 その場合は、Django プロジェクトにしないで、[既存のファイルからプロジェクトを作成しなおす](managing-python-projects-in-visual-studio.md#create-a-project-from-existing-files)必要があります。

## <a name="django-management-console"></a>Django 管理コンソール

Django 管理コンソールには、 **[プロジェクト]** メニューのさまざまなコマンドを使用するか、**ソリューション エクスプローラー** でプロジェクトを右クリックしてアクセスします。

- **[Django シェルを開く]** : モデルを操作できるアプリケーション コンテキストでシェルを起動します。

    ![[Django シェルを開く] コマンドの結果](media/template-django-console-shell.png)

- **[Django Sync DB]**: `manage.py syncdb` を **対話型** ウィンドウで実行します。

    ![[Django Sync DB] コマンドの結果](media/template-django-console-sync-db.png)

- **[静的ファイルの収集]**: `manage.py collectstatic --noinput` を実行して、*settings.py* の `STATIC_ROOT` で指定されたパスにすべての統計ファイルをコピーします。

    ![[静的ファイルの収集] コマンドの結果](media/template-django-console-collect-static.png)

- **[検証]**: *settings.py* の `INSTALLED_APPS` で指定されたインストール済みのモデルで検証エラーをレポートする `manage.py validate` を実行します。

    ![[検証] コマンドの結果](media/template-django-console-validate.png)

## <a name="see-also"></a>関連項目

- [Django チュートリアルの概要](learn-django-in-visual-studio-step-01-project-and-solution.md)
- [Azure App Service に発行する](publishing-python-web-applications-to-azure-from-visual-studio.md)
