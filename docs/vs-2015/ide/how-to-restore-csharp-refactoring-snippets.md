---
title: '方法 : C# リファクタリング スニペットを復元する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- unsafe expansion
- expansions, unsafe
ms.assetid: 12114273-7f2f-43d0-abcb-2d4711a3a68d
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6ae3f1d74a482192d3782aaa87baa816694abcf4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670786"
---
# <a name="how-to-restore-c-refactoring-snippets"></a>方法 : C# リファクタリング スニペットを復元する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C# リファクタリング操作は、次のディレクトリにあるコード スニペットに依存しています。

 *インストール ディレクトリ*\Microsoft Visual Studio 14.0\VC#\Snippets\\*言語 ID*\Refactoring

 この Refactoring ディレクトリまたはこのディレクトリ内のファイルを削除または破損すると、IDE では、C# リファクタリング操作が機能しない場合があります。 次の手順は、C# リファクタリング コード スニペットを復元する場合に役立ちます。

### <a name="to-verify-c-refactoring-snippets-are-available-through-the-code-snippet-manager"></a>C# リファクタリング スニペットをコード スニペット マネージャーで使用できることを確認するには

1. **[ツール]** メニューの **[コード スニペット マネージャー]** を選びます。

2. **[コード スニペット マネージャー]** ダイアログ ボックスで、 **[言語]** ボックスの一覧の **[Visual C#]** を選びます。

     **[リファクタリング]** フォルダーがツリー ビューのフォルダーの一覧に表示されます。

### <a name="to-restore-refactoring-see-comment-in-code-snippet-manager"></a>コード スニペット マネージャーでリファクタリングの see コメントを復元するには

1. コード スニペット マネージャーのツリー ビューのフォルダーの一覧に **[リファクタリング]** フォルダーが表示されない場合は、次の手順を使って、リファクタリング スニペットをコード スニペット マネージャーに追加します。

2. **[ツール]** メニューの **[コード スニペット マネージャー]** を選びます。

3. **[コード スニペット マネージャー]** ダイアログ ボックスで、 **[言語]** ボックスの一覧の **[Visual C#]** を選びます。

4. **[追加]** をクリックします。 **[コード スニペット ディレクトリ]** ダイアログ ボックスが表示されます。このダイアログ ボックスを使って、コード スニペット マネージャーに追加するディレクトリを検索および指定します。

5. 次のディレクトリ パスにある **Refactoring** フォルダーに移動します。

     *インストール ディレクトリ*\Microsoft Visual Studio 14.0\VC#\Snippets\\*言語 ID*\Refactoring

     既定のインストールでは、実際のパスは次のようになります。

     C:\Program Files\Microsoft Visual Studio 14.0\VC#\Snippets\1033\Refactoring

6. **[コード スニペット ディレクトリ]** ダイアログ ボックスの **[開く]** をクリックし、コード スニペット マネージャーの **[OK]** をクリックします。

## <a name="see-also"></a>関連項目
 [ビジュアルC#コードスニペット](../ide/visual-csharp-code-snippets.md)[リファクタリング (C#)](../csharp-ide/refactoring-csharp.md) [コードスニペット](../ide/code-snippets.md)
