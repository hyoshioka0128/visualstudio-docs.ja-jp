---
title: Subversion の使用
description: Visual Studio for Mac の Subversion を使用します。
author: jmatthiesen
ms.author: jomatthi
ms.date: 05/06/2018
ms.assetid: 2400ED9C-6236-4C0A-A3AB-9D7CBE1F0CF4
ms.openlocfilehash: 909da0bcb1ad3ca080d6bf4ba4e5184c1c2da98f
ms.sourcegitcommit: 703c68667261df5985a73282c1cbb0541118989c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402640"
---
# <a name="working-with-subversion"></a>Subversion の使用

Subversion は、集中管理されているバージョン コントロール システムであり、集中管理されているデータの単一のメイン コピーをチェックアウトすることができます。 Git とは対照的に、Subversion リポジトリのチェックアウトではリポジトリ全体は複製されず、その時点のスナップショットのみを取得します。

Subversion では、コピー-変更-マージ モデルを使用して、ユーザーが同時に同じリポジトリで作業できるようにします。 つまり、各ユーザーは、集中管理されているデータのローカル (作業) コピーを作成し、独立して操作できます。 ユーザーの作業コピーへの変更は時系列的にマージされます。

たとえば、ユーザー A とユーザー B の両方がリモート リポジトリからコピーをチェックアウトし、それぞれファイルを変更するとします。 ユーザー A は、変更を終了し、それらをリモートでコミットします。 ユーザー B が作業をコミットする前に、リモートからの変更で作業コピーを更新することで、ユーザー A の変更をマージする必要があります。

以下のセクションでは、Visual Studio for Mac のバージョン コントロールに Subversion を使用する方法について説明します。

次の図は、Visual Studio for Mac の [バージョン コントロール] メニュー項目で提供されるオプションを示しています。

![[バージョン コントロール] メニュー項目](media/version-control-svnVersionControlMenu.png)

## <a name="checkout"></a>チェックアウト

リモートの Subversion リポジトリの使用を始める前に、リポジトリをチェックアウトして、ローカル コンピューターにそのディレクトリの作業コピーを作成します。

Visual Studio for Mac の**チェックアウト**機能の使用方法については、「[Setting up a Subversion repository](set-up-subversion-repository.md)」(Subversion リポジトリのセットアップ) の手順に従ってください。

## <a name="update-solution"></a>ソリューションの更新

リモート リポジトリを使用する場合は、他のユーザーがファイルを変更したために自分の作業コピーが古くなる可能性がある点に注意してください。 競合を想定して、作業を開始する前のコミットする前に、リポジトリからすべての変更をソリューションにプルすることを常にお勧めします。 変更をプルするには、 **[バージョン コントロール] > [ソリューションの更新]** メニュー項目を選択します。

## <a name="review-solution-and-commit"></a>ソリューションの確認とコミット

ファイルの変更を確認するには、次の図のように、各ドキュメントの [変更]、[変更履歴]、[ログ]、[マージ] タブを使用します。

![[バージョン コントロール] タブ](media/version-control-vcTabs.png)

**[バージョン コントロール] > [ソリューションの確認とコミット]** メニュー項目を参照して、プロジェクトのすべての変更を確認します。

![ソリューションの確認](media/version-control-vcStatus.png)

これにより、プロジェクトの各ファイルのすべての変更を表示し、[元に戻す]、[修正プログラムの作成]、[コミット] のオプション選択できます。

リモート リポジトリに対してファイルをコミットするには、[コミット] を押し、コミット メッセージを入力して、[コミット] ボタンで確認します。

![ファイルをコミットする](media/version-control-svnCommit.png)

これにより、変更がリポジトリに送信され、すべての変更の新しいリビジョンが作成されます。

## <a name="see-also"></a>参照

- [Subversion リポジトリの設定](set-up-subversion-repository.md)
