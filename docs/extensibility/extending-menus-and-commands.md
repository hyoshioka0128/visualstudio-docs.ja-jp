---
title: メニューとコマンドの拡張 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, common tasks
- VSPackages, menu tasks
- .vsct files, common menu tasks
ms.assetid: 7b2be4b9-e3fe-4412-874f-ae72ebc84c4b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dfcedd3f1b4cb48631541f1726556dab766402ab
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711801"
---
# <a name="extend-menus-and-commands"></a>メニューとコマンドの拡張
コマンドは、アクションとプロセスを Visual Studio に追加する方法です。 ほとんどの場合、コマンドはメニューまたはツールバーに表示されます。 VSPackage プロジェクト テンプレートは、非常に基本的なコマンドを実装する方法を示しています。 少し長いが、まだ基本的な実装については、[メニュー コマンドを使用して拡張機能を作成するを](../extensibility/creating-an-extension-with-a-menu-command.md)参照してください。

 Visual Studio のコマンド、メニュー、およびツール バーの詳細については、「[コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

 コマンド、メニュー、およびツール バーは、VSPackage プロジェクトの一部である *.vsct*ファイルで定義されます。 Visual Studio IDE と *.vsct*ファイルに関する情報は[、「VSPackage がユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

 次のトピックでは、さまざまな種類のコマンド、メニュー、およびツールバーを追加する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [メニューを Visual Studio のメニュー バーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)Visual Studio の上部のメニュー バーにメニューを追加する方法について説明します。

- [キーボード ショートカットをメニュー項目にバインドする](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)メニュー項目にキーボード ショートカット (Ctrl + 3 など) を追加する方法について説明します。

- [メニューにサブメニューを追加する](../extensibility/adding-a-submenu-to-a-menu.md)トップ メニューにサブメニューを追加する方法について説明します。

- [最近使用したリストをサブメニューに追加する](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md)最近使用したリストを追加する方法について説明します。

- [再利用可能なボタンのグループを作成する](../extensibility/creating-reusable-groups-of-buttons.md)複数のメニューに含めることができるように、コマンド項目をグループ化する方法について説明します。

- [メニュー コマンドにアイコンを追加する](../extensibility/adding-icons-to-menu-commands.md)ツール バーとメニューの両方のコマンドにアイコンを追加する方法について説明します。

- [メニュー コマンドのテキストを変更する](../extensibility/changing-the-text-of-a-menu-command.md)`TextChanges`メニュー項目を動的に変更できるようにするためのフラグの使用方法について説明します。

- [コマンドの外観を変更する](../extensibility/changing-the-appearance-of-a-command.md)コマンドを動的に有効または無効にする方法について説明します。

- [ユーザー インターフェイスを更新する](../extensibility/updating-the-user-interface.md)ユーザー インターフェイスを更新して最新の変更を反映させる方法について説明します。

- [ローカライズ メニュー コマンド](../extensibility/localizing-menu-commands.md)メニュー コマンドをローカライズする方法について説明します。
