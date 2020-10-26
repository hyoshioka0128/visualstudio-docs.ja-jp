---
title: メニューとコマンドの拡張 |Microsoft Docs
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
ms.openlocfilehash: c344d996c70012ef1516fa2bebe52394739bea35
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85768587"
---
# <a name="extend-menus-and-commands"></a>メニューとコマンドを拡張する
コマンドは、Visual Studio にアクションとプロセスを追加する方法です。 ほとんどの場合、コマンドはメニューまたはツールバーに表示されます。 VSPackage プロジェクトテンプレートは、非常に基本的なコマンドを実装する方法を示しています。 少し時間がかかりながら基本的な実装については、「 [メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

 Visual Studio のコマンド、メニュー、およびツールバーの詳細については、「 [コマンド、メニュー、およびツール](../extensibility/internals/commands-menus-and-toolbars.md)バー」を参照してください。

 コマンド、メニュー、およびツールバーは、VSPackage プロジェクトの一部である *vsct* ファイルで定義されています。 詳細については、「 [How vspackage add user interface elements](../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照して*ください*。

 次のトピックでは、さまざまな種類のコマンド、メニュー、およびツールバーを追加する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [メニューを Visual Studio のメニューバーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md) Visual Studio のトップメニューバーにメニューを追加する方法について説明します。

- [メニュー項目にキーボードショートカットをバインドする](../extensibility/binding-keyboard-shortcuts-to-menu-items.md) ショートカットキー (CTRL + 3 など) をメニュー項目に追加する方法について説明します。

- [メニューにサブメニューを追加する](../extensibility/adding-a-submenu-to-a-menu.md) トップメニューにサブメニューを追加する方法について説明します。

- [最近使用した一覧をサブメニューに追加する](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md) 最近使用した一覧を追加する方法について説明します。

- [再利用可能なボタンのグループを作成する](../extensibility/creating-reusable-groups-of-buttons.md) コマンド項目を複数のメニューに含めることができるようにグループ化する方法について説明します。

- [メニューコマンドにアイコンを追加する](../extensibility/adding-icons-to-menu-commands.md) ツールバーとメニューの両方でコマンドにアイコンを追加する方法について説明します。

- [メニューコマンドのテキストを変更する](../extensibility/changing-the-text-of-a-menu-command.md) メニュー項目を動的に変更できるようにするためのフラグの使用について説明し `TextChanges` ます。

- [コマンドの外観を変更する](../extensibility/changing-the-appearance-of-a-command.md) コマンドを動的に有効または無効にする方法について説明します。

- [ユーザーインターフェイスを更新する](../extensibility/updating-the-user-interface.md) ユーザーインターフェイスを強制的に更新して最新の変更を反映する方法について説明します。

- [メニューコマンドのローカライズ](../extensibility/localizing-menu-commands.md) メニューコマンドをローカライズする方法について説明します。
