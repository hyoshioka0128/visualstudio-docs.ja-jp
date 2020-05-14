---
title: '方法 : Visual Basic 開発者設定が適用されたビルド構成を管理する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, building with Visual Basic settings
- MSBuild, debug build
- advanced build configurations
- building with Visual Basic developer settings
- debug builds
- MSBuild, release build
- release builds
ms.assetid: eaea6e0b-6c61-4869-8d63-d372c745a23c
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a5f8568edc636955558ec93b55c0aedebf0065d3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651834"
---
# <a name="how-to-manage-build-configurations-with-visual-basic-developer-settings-applied"></a>方法 : Visual Basic 開発者設定が適用されたビルド構成を管理する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

既定では、すべてのビルド構成の詳細オプションは [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 開発者設定が適用されて非表示になっています。 このトピックでは、これらの設定を手動で有効にする方法について説明します。

## <a name="enabling-advanced-build-configurations"></a>ビルド構成の詳細を有効にする
 既定では、 **[構成マネージャー]** ダイアログ ボックスおよび[プロジェクト デザイナー](https://msdn.microsoft.com/898dd854-c98d-430c-ba1b-a913ce3c73d7)の **[構成]** 一覧と **[プラットフォーム]** 一覧を開くためのオプションは、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 開発者設定によって非表示になっています。

#### <a name="to-enable-advanced-build-configurations"></a>ビルド構成の詳細を有効にするには

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[プロジェクトおよびソリューション]** を展開し、 **[全般]** をクリックします。

    > [!NOTE]
    > **[全般]** ノードは、 **[すべての設定を表示]** オプションがオフになっている場合でも表示されます。 使用可能なすべてのオプションを表示する場合は、 **[すべての設定を表示]** をクリックします。

3. **[ビルド構成の詳細を表示]** をクリックします。

4. **[OK]** をクリックします。

     **[ビルド]** メニューで **[構成マネージャー]** を使用できるようになり、 **[構成]** 一覧と **[プラットフォーム]** 一覧がプロジェクト デザイナーに表示されるようになります。

## <a name="see-also"></a>関連項目
 [ビルド構成につい](../ide/understanding-build-configurations.md)[てのコンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
