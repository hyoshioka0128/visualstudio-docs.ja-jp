---
title: プロジェクトを構成して複数の対象プラットフォームを設定する
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- projects [Visual Studio], targeting platforms
- platforms, changing target platforms
ms.assetid: affa2392-7aed-45ac-9ffa-1d8e0496d590
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2643e7f413a68d820780db80c87818dd0b8b9c03
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90036510"
---
# <a name="how-to-configure-projects-to-target-multiple-platforms"></a>方法: プロジェクトを構成して複数の対象プラットフォームを設定する

Visual Studio では、ソリューションは同時に複数の異なる CPU アーキテクチャまたはプラットフォームを対象にすることができます。 これを設定するプロパティには、 **[構成マネージャー]** ダイアログ ボックスからアクセスします。

## <a name="target-a-platform"></a>対象プラットフォームを設定する

**[構成マネージャー]** ダイアログ ボックスでは、ソリューション レベルおよびプロジェクト レベルの構成とプラットフォームを作成して設定できます。 ソリューション レベルの構成とターゲットの各組み合わせには一意のプロパティ セットが関連付けられており、簡単に切り替えることができます。たとえば、[!INCLUDE[vcprx64](../extensibility/internals/includes/vcprx64_md.md)] プラットフォームを対象とするリリース構成、x86 プラットフォームを対象とするリリース構成、x86 プラットフォームを対象とするデバッグ構成などです。

1. **[ビルド]** メニューの **[構成マネージャー]** をクリックします。

2. **[アクティブ ソリューション プラットフォーム]** ボックスでソリューションの対象にするプラットフォームを選ぶか、 **\<New>** を選んで新しいプラットフォームを作成します。 Visual Studio は、 **[構成マネージャー]** ダイアログ ボックスでアクティブ プラットフォームとして設定されているプラットフォームを対象とするようにアプリケーションをコンパイルします。

## <a name="remove-a-platform"></a>プラットフォームを削除する

対象とする必要がなくなったプラットフォームは、 **[構成マネージャー]** ダイアログ ボックスを使って削除できます。 その構成と対象の組み合わせに対して構成されているすべてのソリューションとプロジェクトの設定が削除されます。

1. **[ビルド]** メニューの **[構成マネージャー]** をクリックします。

2. **[アクティブ ソリューション プラットフォーム]** ボックスで、 **\<Edit>** を選びます。 **[ソリューション プラットフォームの編集]** ダイアログ ボックスが表示されます。

3. 削除するプラットフォームをクリックし、 **[削除]** をクリックします。

## <a name="target-multiple-platforms-with-one-solution"></a>1 つのソリューションで複数のプラットフォームを対象にする

構成とプラットフォームの設定の組み合わせに基づいて設定を変更できるので、複数のプラットフォームを対象とするソリューションを設定することができます。

### <a name="to-target-multiple-platforms"></a>複数のプラットフォームを対象にするには

1. **[構成マネージャー]** を使って、少なくとも 2 つの対象プラットフォームをソリューションに追加します。

2. **[アクティブ ソリューション プラットフォーム]** ボックスの一覧から、対象にするプラットフォームを選びます。

3. ソリューションをビルドします。

### <a name="to-build-multiple-solution-configurations-at-once"></a>一度に複数のソリューション構成をビルドするには

1. **[構成マネージャー]** を使って、少なくとも 2 つの対象プラットフォームをソリューションに追加します。

2. 一度に複数のソリューション構成をビルドするには、 **[バッチ ビルド]** ウィンドウを使います。

   ソリューション レベルのプラットフォームをたとえば [!INCLUDE[vcprx64](../extensibility/internals/includes/vcprx64_md.md)] に設定し、そのソリューション内のプロジェクトでは同じプラットフォームを対象としない、といったことができます。 また、ソリューション内の複数のプロジェクトで、それぞれ異なるプラットフォームを対象とすることもできます。 いずれかの状況の場合は、混乱を避けるためにわかりやすい名前で新しい構成を作成することをお勧めします。

## <a name="see-also"></a>関連項目

- [方法: 構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)
- [ビルド構成について](../ide/understanding-build-configurations.md)
- [Visual Studio でのプロジェクトとソリューションのビルドおよびクリーン](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
