---
title: Visual Studio を修復します
titleSuffix: ''
description: Visual Studio 2017 のインストールを修復する方法について説明します
ms.date: 07/31/2019
ms.custom: seodec18
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 368ca6619a2fcff48cc3bcc7eb70913247b631b2
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76114735"
---
# <a name="repair-visual-studio"></a>Visual Studio を修復します

::: moniker range="vs-2017"

Visual Studio のインストールが損傷したり、破損したりすることがあります。 修復により、これを修正できます。

1. コンピューター上の **Visual Studio インストーラー**を見つけます。

     たとえば、Windows 10 Anniversary Update 以降を実行しているコンピューター上では、 **[スタート]** を選択し、**Visual Studio インストーラー**としてリスト表示される **V** の文字までスクロールします。

   > [!NOTE]
   > 一部のコンピューターでは、Visual Studio インストーラーが **Microsoft Visual Studio インストーラー**として **"M"** の項に表示される場合があります。
   >
   > Visual Studio インストーラーは `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe` にもあります。

1. インストーラーを開き、 **[その他]** を選択した後、 **[修復]** を選択します。

    ![Visual Studio インストーラーから Visual Studio を修復する](media/repair-visual-studio.png "Visual Studio インストーラーから Visual Studio を修復する")

   > [!NOTE]
   > Visual Studio を修復すると、環境がリセットされます。 昇格なしでインストールした、ユーザーごとの拡張機能などのローカル カスタマイズや、ユーザー設定、およびプロファイルが削除されます。 テーマ、色、キー バインドなど、同期された設定が復元されます。
   >

   > [!TIP]
   > **[修復]** オプションは、インストールされている Visual Studio のインスタンスに対してのみ表示されます。 **[修復]** オプションが表示されない場合は、Visual Studio インストーラーに "インストール済み" ではなく "使用可能" と表示されているバージョンで **[その他]** を選択した可能性があります。

::: moniker-end

::: moniker range="vs-2019"

1. コンピューター上で Visual Studio インストーラーを見つけます。

     たとえば、Windows 10 を実行しているコンピューター上で、 **[スタート]** を選択し、**Visual Studio インストーラー**としてリスト表示される **V** の文字までスクロールします。

     ![Visual Studio インストーラーを開く](media/vs-2019/vs-installer-windows-start.png "Visual Studio インストーラーを開く")

     > [!NOTE]
     > また、Visual Studio インストーラーは次の場所にもあります。
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    続行する前に、インストーラーの更新が必要な場合があります。 その場合は、画面の指示に従います。

1. インストーラーで、インストールした Visual Studio のエディションを探します。 次に、 **[その他]** を選択した後、 **[修復]** を選択します。

     ![Visual Studio 2019 を修復する](media/vs-2019/vs-installer-repair.png "Visual Studio 2019 を修復する")

   > [!NOTE]
   > Visual Studio を修復すると、環境がリセットされます。 昇格なしでインストールした、ユーザーごとの拡張機能などのローカル カスタマイズや、ユーザー設定、およびプロファイルが削除されます。 テーマ、色、キー バインドなど、同期された設定が復元されます。
   >

   > [!TIP]
   > **[修復]** オプションは、インストールされている Visual Studio のインスタンスに対してのみ表示されます。 **[修復]** オプションが表示されない場合は、Visual Studio インストーラーに "インストール済み" ではなく "使用可能" と表示されているバージョンで **[その他]** を選択した可能性があります。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [Visual Studio の更新](update-visual-studio.md)
* [Visual Studio のアンインストール](uninstall-visual-studio.md)
* [Visual Studio のインストールとアップグレードの問題のトラブルシューティング](troubleshooting-installation-issues.md)
