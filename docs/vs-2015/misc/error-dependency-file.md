---
title: 'エラー: プロジェクト &#39;&#39; プロジェクトの依存関係 &#39;ファイル&#39; は、依存関係 &#39;ファイル&#39; と競合するため、実行ディレクトリにコピーできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
f1_keywords:
- vs.tasklisterror.copy_version_conflict
ms.assetid: cd7de1eb-7d58-4e2c-9811-a7201f7817be
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5d4fd45741585aaf82c82257999b40d6257e82d9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656049"
---
# <a name="error-the-dependency-39file39-in-project-39project39-cannot-be-copied-to-the-run-directory-because-it-would-conflict-with-dependency-39file39"></a>エラー: プロジェクト &#39;&#39; プロジェクトの依存関係 &#39;ファイル&#39; は、依存関係 &#39;ファイルと競合するため、実行ディレクトリにコピーできません&#39;
参照間で競合が発生しています。アプリケーションが実行される bin ディレクトリに、ファイル名が同じ複数の依存関係がコピーされようとしています。 どの依存関係もプライマリ参照ではないため、実行ディレクトリは競合を解決できません。

 このエラーが発生すると、ビルドが失敗します。

 このタスク一覧の項目をダブルクリックすると、競合が発生しているプロジェクトの参照ノードが表示されます。

 **このエラーを解決するには**

- アセンブリのいずれかをプロジェクトの直接参照にします。 この方法で考えられる欠点は、選択するアセンブリが、他のバージョンの参照アセンブリを要求するアセンブリと共に動作することが保証されない点です。

     \- または

- 両方のアセンブリ コピーが厳密に命名され、グローバル アセンブリ キャッシュに存在することを確認します。 これにより、アセンブリを bin ディレクトリにコピーする必要がなくなります。

## <a name="see-also"></a>参照
 [プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)[グローバルアセンブリキャッシュ](https://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202)の[厳密な名前付きアセンブリ](https://msdn.microsoft.com/library/d4a80263-f3e0-4d81-9b61-f0cbeae3797b)[アセンブリのバージョン管理](https://msdn.microsoft.com/library/775ad4fb-914f-453c-98ef-ce1089b6f903)[方法: プロジェクトの依存関係を作成および削除する](../ide/how-to-create-and-remove-project-dependencies.md)