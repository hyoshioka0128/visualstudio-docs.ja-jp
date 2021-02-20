---
title: Subversion リポジトリのセットアップ
description: Visual Studio for Mac の一元化されたバージョン コントロール システムとして Subversion をインストールしてセットアップする方法について説明します。
author: jmatthiesen
ms.author: jomatthi
ms.date: 05/06/2018
ms.assetid: 0D58FB37-530E-495B-BED6-FD499477A9B6
ms.topic: how-to
ms.openlocfilehash: b5230958fa1624acf7609d6cad7d885e43c013d0
ms.sourcegitcommit: d577818d3d8e365baa55c6108fa8159c46ed8b43
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2021
ms.locfileid: "97847068"
---
# <a name="set-up-a-subversion-repository"></a>Subversion リポジトリの設定

Subversion は集中管理されている _バージョン管理システム_ です。つまり、すべてのファイルとリビジョンが格納された単一のサーバーが存在し、ユーザーはそこから任意のファイルの任意のバージョンをチェック アウトできます。 ファイルがリモート Subversion リポジトリからチェックアウトされると、ユーザーはその時点のリポジトリのスナップショットを取得します。

Subversion をバージョン管理に使用するには、これをコンピューターにインストールする必要があります。Subversion がコンピューターにインストールされているかどうかを確認するには、ターミナルで次のコマンドを使用します。

```bash
svn --version
```

このコマンドはバージョン番号を返します。

Subversion がまだインストールされていない場合にこれを取得する最も簡単な方法は、_Xcode コマンド ライン ツール_ をインストールする方法です。 Xcode コマンド ライン ツールと Subversion をインストールするには、次のコマンドを使用します。

```bash
xcode-select --install
```

Subversion がコンピューターにインストールされたら、次の手順を使用して、SVN でプロジェクトを発行します。

1. オンラインで無料の SVN リポジトリを作成します。 この例では [Assembla](https://app.assembla.com/) が使用されています。 作成後に、URL が提供されます。これはリポジトリへの接続に使用されます。

    ![SVN URL をコピーします](media/version-control-subversion1-sml.png)

2. Visual Studio for Mac プロジェクトを開くか、作成します。

3. 次のように、プロジェクトを右クリックして、 **[バージョン管理]、[Publish in Version Control...]\(バージョン管理で発行...\)** の順に選択します。

    ![プロジェクトの発行を開始する](media/version-control-subversion2.png)

4. **[リポジトリへの接続]** タブで、上部のドロップダウンから **[Subversion]** を選択します。

5. 手順 1. の URL を入力します。 URL が入力されたら、他のフィールドが既定により設定されます。

    ![[リポジトリの選択] と詳細入力ダイアログ](media/version-control-subversion3.png)

7. **[OK]** をクリックし、 **[発行]** を押して確認します。

7. リポジトリを作成するサイトの資格情報の入力を求められたら、次の図のように入力します。

    ![Subversion リポジトリの資格情報の入力](media/version-control-subversion5.png)

8. これで、使用可能なすべてのバージョン管理コマンドがバージョン管理メニューに表示されます。

## <a name="see-also"></a>参照

- [Subversion の使用](working-with-subversion.md)
