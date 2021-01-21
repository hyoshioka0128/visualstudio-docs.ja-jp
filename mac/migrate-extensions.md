---
title: トラブルシューティング:既存の拡張機能の新しいバージョンをリリースする方法
description: 公開ワークフローを使用した既存の拡張機能の更新に関するガイド。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 12/14/2020
ms.technology: vs-ide-general
ms.assetid: 5DA76197-7859-421f-AC45-401F22F5D794
ms.topic: troubleshooting
ms.openlocfilehash: 862ae404571da44d9ca28db2c94d2ebeb39ce79f
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97488543"
---
# <a name="troubleshooting-how-do-i-release-a-new-version-of-my-existing-extension"></a>トラブルシューティング:既存の拡張機能の新しいバージョンをリリースする方法

> [!IMPORTANT]
> 現在、新しい拡張機能の作成は Visual Studio 2019 for Mac では正式にサポートされていません。

Visual Studio for Mac 拡張機能リポジトリ サーバーは、2021 年 1 月 15 日に移行します。 この移行は、お客様の拡張機能を既にダウンロードしているユーザーには影響しませんが、この日以降に拡張機能の新しいリリースを公開する方法が変更されます。

既存の拡張機能の作成者は、今後の更新プログラムをリリースするために別のワークフローに従う必要があります。 このプロセスは次のもので構成されます。
- 拡張機能ごとにパブリック GitHub リポジトリを設定する
- [拡張機能公開メーリング リスト](mailto:vsmextpub@microsoft.com)を使用して Visual Studio for Mac チームにリポジトリ URL を共有する
- GitHub のリリース機能を使用して拡張機能を更新する


## <a name="initial-setup"></a>初期セットアップ 

拡張機能に対する更新プログラムの公開を続行するには、パブリック GitHub リポジトリを作成する必要があります。 複数の拡張機能を公開する場合は、それぞれにつき個別のリポジトリを用意する必要があります。ただし、それらを常に一緒にバージョン管理して公開する場合は、1 つのリポジトリを使用できます。

> [!NOTE]
> 拡張機能用の GitHub リポジトリはパブリックである必要がありますが、そこでコードをホストする必要はありません。 このプロセスに従うために、コードを GitHub に配置する必要はありません。


## <a name="share-the-location-of-your-repository"></a>リポジトリの場所を共有する

リポジトリを設定したら、[拡張機能公開メーリング リスト](mailto:vsmextpub@microsoft.com)に URL が記載されたメールを送信します。


## <a name="release-a-new-version"></a>新しいバージョンをリリースする

リポジトリのメイン ページにある "新しいリリースの作成" リンクを使用して、拡張機能の更新プロセスを開始します。 このリンクを選択したら、次の手順を実行します。

1. リリースの **タグ バージョン** に、次の形式で情報を追加します。

    > v\<releaseVersion>\-vsm\<targetVersion>

    条件:
     - **&lt;releaseVersion&gt;** は拡張機能のバージョン番号です
     - **&lt;targetVersion&gt;** は、拡張機能がターゲットとしている Visual Studio for Mac の最小バージョンです

2. (省略可能) **タイトル** と **説明** のフィールドには、任意の情報を入力できます。このワークフローでは、これらのフィールド内の情報は使用されません。

3. **プレリリース** のチェックボックスがオフになっていることを確認します。 オンになっている場合、リリースはこの公開プロセスによって取得されなくなります。

4. 拡張機能を実装する **.mpack** ファイルを **バイナリ** のセクションに添付します。 1 つのリリースで、複数の **.mpack** ファイルを添付することができます。

Visual Studio for Mac には、その拡張機能リポジトリへのアクセスに使用された Visual Studio for Mac インストールと互換性のある、最新バージョンの拡張機能が表示されます。

GitHub リポジトリを Visual Studio for Mac チームに登録している限り、お客様の拡張機能リリースは 24 時間以内に Visual Studio for Mac によって取得されます。

## <a name="additional-information"></a>関連情報

- 上記の要件に準拠していないリリースは公開されません。 
- 2021 年 1 月 15 日以降、拡張機能の更新プログラムは Visual Studio for Mac 8.0 以降にのみ表示されます。
- 既存の拡張機能については、お客様が操作しなくても引き続き Visual Studio for Mac ユーザーが使用できます。 2021 年 1 月 15 日以降に新しいバージョンを公開する場合にのみ、このガイドの手順に従う必要があります。
