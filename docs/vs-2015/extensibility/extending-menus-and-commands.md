---
title: メニューとコマンドの拡張 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, common tasks
- VSPackages, menu tasks
- .vsct files, common menu tasks
ms.assetid: 7b2be4b9-e3fe-4412-874f-ae72ebc84c4b
caps.latest.revision: 50
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 83d9dc45863f1ed1b5e11c17b9e922b62b0186dc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204534"
---
# <a name="extending-menus-and-commands"></a>メニューとコマンドの拡張
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コマンドは、Visual Studio にアクションとプロセスを追加する方法です。 ほとんどの場合、コマンドはメニューまたはツールバーに表示されます。 VSPackage プロジェクトテンプレートは、非常に基本的なコマンドを実装する方法を示しています。 少し時間がかかりながら基本的な実装については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。  
  
 Visual Studio のコマンド、メニュー、およびツールバーの詳細については、「 [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。  
  
 コマンド、メニュー、およびツールバーは、VSPackage プロジェクトの一部である vsct ファイルで定義されています。 詳細については、「 [How Vspackage Add User Interface Elements](../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。  
  
 次のトピックでは、さまざまな種類のコマンド、メニュー、およびツールバーを追加する方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Visual Studio のメニュー バーへのメニューの追加](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)  
 Visual Studio のトップメニューバーにメニューを追加する方法について説明します。  
  
 [キーボード ショートカットのメニュー項目へのバインド](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)  
 ショートカットキー (CTRL + 3 など) をメニュー項目に追加する方法について説明します。  
  
 [サブメニューのメニューへの追加](../extensibility/adding-a-submenu-to-a-menu.md)  
 トップメニューにサブメニューを追加する方法について説明します。  
  
 [最近使用した一覧のサブメニューへの追加](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md)  
 最近使用した一覧を追加する方法について説明します。  
  
 [再利用可能なボタンのグループの作成](../extensibility/creating-reusable-groups-of-buttons.md)  
 コマンド項目を複数のメニューに含めることができるようにグループ化する方法について説明します。  
  
 [メニュー コマンドへのアイコンの追加](../extensibility/adding-icons-to-menu-commands.md)  
 ツールバーとメニューの両方でコマンドにアイコンを追加する方法について説明します。  
  
 [メニュー コマンドのテキストの変更](../extensibility/changing-the-text-of-a-menu-command.md)  
 メニュー項目を動的に変更できるようにするためのフラグの使用について説明し `TextChanges` ます。  
  
 [コマンドの外観の変更](../extensibility/changing-the-appearance-of-a-command.md)  
 コマンドを動的に有効または無効にする方法について説明します。  
  
 [ユーザー インターフェイスの更新](../extensibility/updating-the-user-interface.md)  
 ユーザーインターフェイスを強制的に更新して最新の変更を反映する方法について説明します。  
  
 [メニュー コマンドのローカライズ](../extensibility/localizing-menu-commands.md)  
 メニューコマンドをローカライズする方法について説明します。  
  
## <a name="related-sections"></a>関連項目
