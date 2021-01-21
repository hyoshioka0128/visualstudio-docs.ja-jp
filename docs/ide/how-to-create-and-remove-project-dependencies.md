---
title: '方法 : プロジェクトの依存関係を作成および削除する'
description: Visual Studio を使用すれば、他のプロジェクトに対する自分のプロジェクトの依存関係をコード上で作成したり、削除したりできます。そのしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 06/21/2017
ms.topic: how-to
f1_keywords:
- VS.ProjectDependenciesDlg
helpviewer_keywords:
- vs.build.projectdependencies
- project dependencies
- builds [Visual Studio], setting up
- project build configurations, dependencies
- dependencies, project
- projects [Visual Studio], dependencies
ms.assetid: e2a0a8ff-dae7-40a8-b774-b88aa5235183
ms.technology: vs-ide-compile
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8b2a99e297b4ce7291c0dd94947155794cf8c3d4
ms.sourcegitcommit: c9a84e6c01e12ccda9ec7072dd524830007e02a3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92137026"
---
# <a name="how-to-create-and-remove-project-dependencies"></a>方法 : プロジェクトの依存関係を作成および削除する

複数のプロジェクトを含むソリューションをビルドするとき、最初に特定のプロジェクトをビルドし、他のプロジェクトで使われるコードを生成することが必要な場合があります。 別のプロジェクトによって生成された実行可能コードをプロジェクトで使用するとき、コードを生成するプロジェクトは、そのコードを使うプロジェクトのプロジェクトの依存関係と呼ばれます。 このような依存関係は、 **[プロジェクトの依存関係]** ダイアログ ボックスで定義できます。

## <a name="to-assign-dependencies-to-projects"></a>プロジェクトに依存関係を割り当てるには

1. **ソリューション エクスプローラー** でプロジェクトを選択します。

2. **[プロジェクト]** メニューの **[プロジェクトの依存関係]** を選びます。

    **[プロジェクトの依存関係]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > **[プロジェクトの依存関係]** オプションは、複数のプロジェクトを含むソリューションでのみ使うことができます。

3. **[依存関係]** タブで、 **[プロジェクト]** ドロップダウン メニューからプロジェクトを選びます。

4. **[依存先]** フィールドで、このプロジェクトより先にビルドする必要のある他のプロジェクトのチェック ボックスをオンにします。

   プロジェクトの依存関係を作成するには、先に複数のプロジェクトでソリューションを構成しておく必要があります。

## <a name="to-remove-dependencies-from-projects"></a>プロジェクトから依存関係を削除するには

1. **ソリューション エクスプローラー** でプロジェクトを選択します。

2. **[プロジェクト]** メニューの **[プロジェクトの依存関係]** を選びます。

     **[プロジェクトの依存関係]** ダイアログ ボックスが表示されます。

    > [!NOTE]
    > **[プロジェクトの依存関係]** オプションは、複数のプロジェクトを含むソリューションでのみ使うことができます。

3. **[依存関係]** タブで、 **[プロジェクト]** ドロップダウン メニューからプロジェクトを選びます。

4. **[依存先]** フィールドで、このプロジェクトの依存関係ではなくなった他のプロジェクトの横にあるチェック ボックスをオフにします。

## <a name="see-also"></a>関連項目

- [Visual Studio でのプロジェクトとソリューションのビルドおよびクリーン](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
- [ビルド構成について](../ide/understanding-build-configurations.md)
- [プロジェクトおよびソリューションのプロパティの管理](managing-project-and-solution-properties.md)
