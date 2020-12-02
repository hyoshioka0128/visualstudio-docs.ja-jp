---
title: Visual Basic 開発者設定を使用してビルド構成を管理する
description: Visual Studio 開発者設定が適用される場合に非表示となるビルド構成の詳細オプションについて、およびこれらのビルド設定を手動で有効にする方法について説明します。
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- advanced build configurations
- building with Visual Basic developer settings (Visual Studio)
- debug builds
- release builds
ms.assetid: eaea6e0b-6c61-4869-8d63-d372c745a23c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bd13c0a9f64ce484d9ba4e3193f7da94d0b1e446
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96189291"
---
# <a name="how-to-manage-build-configurations-with-visual-basic-developer-settings-applied"></a>方法 : Visual Basic 開発者設定が適用されたビルド構成を管理する

既定では、Visual Studio 開発者設定が適用されると、すべてのビルド構成の詳細オプションが非表示になります。 この記事では、これらのビルド設定を手動で有効にする方法について説明します。

## <a name="enable-advanced-build-configurations"></a>ビルド構成の詳細を有効にする

既定では、**[構成マネージャー]** ダイアログ ボックスおよび [プロジェクト デザイナー](../ide/reference/application-page-project-designer-visual-basic.md)の **[構成]** 一覧と **[プラットフォーム]** 一覧を開くためのオプションは、Visual Basic 開発者設定によって非表示になっています。

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[プロジェクトおよびソリューション]** を展開し、**[全般]** をクリックします。

3. **[ビルド構成の詳細を表示]** をクリックします。

4. **[OK]** をクリックします。

     **[ビルド]** メニューで **[構成マネージャー]** を使用できるようになり、**[構成]** 一覧と **[プラットフォーム]** 一覧が **プロジェクト デザイナー** に表示されるようになります。

## <a name="see-also"></a>関連項目

- [ビルド構成について](../ide/understanding-build-configurations.md)
- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
- [環境設定](../ide/environment-settings.md)
