---
title: app.config ファイルをプロジェクトに追加する方法
description: app.config ファイルを C# プロジェクトに追加して、共通言語ランタイムによるアセンブリ ファイルの検索および読み込み方法をカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
helpviewer_keywords:
- app.config files, adding to C# projects
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 282c66acd71d0c68ff5bc3c74db2e8a2517a00d1
ms.sourcegitcommit: d6207a3a590c9ea84e3b25981d39933ad5f19ea3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/24/2020
ms.locfileid: "95597354"
---
# <a name="how-to-add-an-application-configuration-file-to-a-c-project"></a>方法: C# プロジェクトにアプリケーション構成ファイルを追加する

アプリケーション構成ファイル (*app.config* ファイル) を C# プロジェクトに追加すると、共通言語ランタイムがアセンブリ ファイルを検索し読み込む方法をカスタマイズできます。 アプリケーション構成ファイルの詳細については、「[ランタイムがアセンブリを検索する方法 (.NET Framework)](/dotnet/framework/deployment/how-the-runtime-locates-assemblies)」を参照してください。

> [!NOTE]
> UWP アプリには、*app.config* ファイルは含まれていません。

プロジェクトをビルドすると、開発環境が *app.config* ファイルを自動的にコピーして、実行可能ファイルに一致するようにコピーのファイル名を変更し、そのコピーを **bin** ディレクトリに移動します。

## <a name="to-add-an-application-configuration-file-to-a-c-project"></a>C# プロジェクトにアプリケーション構成ファイルを追加するには

1. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

1. **[インストール]**  >  **[Visual C# アイテム]** の順に展開し、 **[アプリケーション構成ファイル]** テンプレートを選択します。

1. **[名前]** ボックスに名前を入力し、**[追加]** ボタンをクリックします。

     *app.config* という名前のファイルがプロジェクトに追加されます。

## <a name="see-also"></a>関連項目

- [アプリケーション設定の管理 (.NET)](../ide/managing-application-settings-dotnet.md)
- [構成ファイル スキーマ (.NET Framework )](/dotnet/framework/configure-apps/file-schema/index)
- [アプリの構成 (.NET Framework)](/dotnet/framework/configure-apps/index)
