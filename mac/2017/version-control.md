---
title: バージョン コントロール
description: Visual Studio for Mac で Git および Subversion を使用します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: 49917483-28AA-4598-A847-71F1F2E0DCB5
ms.topic: overview
ms.openlocfilehash: 33fdfe3ef6d292dded34a3b468ed9d60d0f6c318
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2020
ms.locfileid: "85938428"
---
# <a name="version-control"></a>バージョン管理

バージョン管理は、ファイルの多くの異なるバージョンを管理するためのシステムであり、ソフトウェア開発では、一般に多くの開発者が関与します。 バージョン管理システム (_VCS_) の主な目的は、すべてのユーザーがコードベースで同時に作業できるソリューションを見つけることです。

すべてのバージョン管理システムの中心にあるのは "_リポジトリ_" であり、リポジトリは、ファイル サーバーと同様に、すべての異なるファイルに対する中央データ ストアとして機能します。 ただし、ファイル サーバーとは異なり、リポジトリにはプロジェクトの履歴全体と行われたすべての改訂が含まれます。

リポジトリが中央のデータ ストアである場合、各ユーザーがデータのローカル ストアを保持して作業することが理にかなっています。 これは "_作業コピー_" と呼ばれます。 Visual Studio for Mac では、作業コピーはコンピューター上の他のローカル ディレクトリと同じように表示され、ファイルを読み取ったり書き込んだりすることができます。 ただし、Visual Studio for Mac にはバージョン コントロール システムが統合されているため、IDE を離れることなく Subversion や Git を利用できます。

Subversion は集中管理されているバージョン コントロール システムです。つまり、すべてのファイルとリビジョンが格納された単一のサーバーが存在し、ユーザーはそこから任意のファイルの任意のバージョンをチェック アウトできます。 ファイルがリモート Subversion リポジトリからチェックアウトされると、ユーザーはその時点のリポジトリのスナップショットを取得します。

Git は、チームが同じドキュメントで同時に作業できるようにする分散型バージョン管理システムです。 Git には、すべてのファイルを含む単一のサーバーが存在する場合がありますが、この中央のソースからリポジトリがチェック アウトされるたびに、リポジトリ全体がローカルのコンピューターに複製されます。

## <a name="basic-concepts"></a>基本的な概念

Visual Studio for Mac は、Git と Subversion の両方のバージョン管理システムに対応しています。 Visual Studio for Mac で Git および Subversion のリポジトリをセットアップする方法、および変更のレビュー、コミット、プッシュなどの簡単な機能の説明については、次の記事を参照してください。

* [Git リポジトリのセットアップ](set-up-git-repository.md)
* [Git の使用](working-with-git.md)
* [Subversion リポジトリのセットアップ](set-up-subversion-repository.md)
* [Subversion の使用](working-with-subversion.md)

## <a name="see-also"></a>関連項目

* [Visual Studio でのバージョン コントロール (Windows)](/visualstudio/version-control/)