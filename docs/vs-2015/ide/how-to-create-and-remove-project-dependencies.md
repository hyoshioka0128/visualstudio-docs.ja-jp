---
title: '方法 : プロジェクトの依存関係を作成および削除する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
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
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a1403beccdb6bf9b938787f62cb3da2e5bb5c259
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668133"
---
# <a name="how-to-create-and-remove-project-dependencies"></a>方法 : プロジェクトの依存関係を作成および削除する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

複数のプロジェクトを含むソリューションをビルドするとき、最初に特定のプロジェクトをビルドし、他のプロジェクトで使われるコードを生成することが必要な場合があります。 別のプロジェクトによって生成された実行可能コードをプロジェクトで使用するとき、コードを生成するプロジェクトは、そのコードを使うプロジェクトのプロジェクトの依存関係と呼ばれます。 このような依存関係は、 **[プロジェクトの依存関係]** ダイアログ ボックスで定義できます。

### <a name="to-assign-dependencies-to-projects"></a>プロジェクトに依存関係を割り当てるには

1. ソリューション エクスプローラーでプロジェクトを選択します。

2. **[プロジェクト]** メニューの **[プロジェクトの依存関係]** を選びます。

    **[プロジェクトの依存関係]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > **[プロジェクトの依存関係]** オプションは、複数のプロジェクトを含むソリューションでのみ使うことができます。

3. **[依存関係]** タブで、 **[プロジェクト]** ドロップダウン メニューからプロジェクトを選びます。

4. **[依存先]** フィールドで、このプロジェクトより先にビルドする必要のある他のプロジェクトのチェック ボックスをオンにします。

   プロジェクトの依存関係を作成するには、先に複数のプロジェクトでソリューションを構成しておく必要があります。

### <a name="to-remove-dependencies-from-projects"></a>プロジェクトから依存関係を削除するには

1. ソリューション エクスプローラーでプロジェクトを選択します。

2. **[プロジェクト]** メニューの **[プロジェクトの依存関係]** を選びます。

     **[プロジェクトの依存関係]** ダイアログ ボックスが表示されます。

    > [!NOTE]
    > **[プロジェクトの依存関係]** オプションは、複数のプロジェクトを含むソリューションでのみ使うことができます。

3. **[依存関係]** タブで、 **[プロジェクト]** ドロップダウン メニューからプロジェクトを選びます。

4. **[依存先]** フィールドで、このプロジェクトの依存関係ではなくなった他のプロジェクトの横にあるチェック ボックスをオフにします。

## <a name="see-also"></a>関連項目
 [Visual Studio でのプロジェクトとソリューションのビルドとクリーン](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)[ビルド構成](../ide/understanding-build-configurations.md)の[コンパイルと](../ide/compiling-and-building-in-visual-studio.md)ビルド[NIB 方法: プロジェクトプロパティと構成設定を変更する](https://msdn.microsoft.com/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
