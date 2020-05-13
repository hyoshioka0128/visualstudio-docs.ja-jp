---
title: '方法: 複数の構成を同時にビルドする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: ba830937-3317-4674-8cc2-c0cd565603c5
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 719b31e834b5410dd137a0c5b69cc07ae01651e3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645473"
---
# <a name="how-to-build-multiple-configurations-simultaneously"></a>方法: 複数の構成を同時にビルドする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[バッチ ビルド]** ダイアログ ボックスを使用すると、複数、またはすべてのプロジェクト ビルド構成で、ほとんどの種類のプロジェクトを同時にビルドできます。 ただし、次の種類のプロジェクトは、複数のビルド構成で同時にビルドすることはできません。

1. JavaScript を使用して Windows 用にビルドされた [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリ。

2. すべての Visual Basic プロジェクト。

   ビルド構成の詳細については、「[ビルド構成について](../ide/understanding-build-configurations.md)」を参照してください。

### <a name="to-build-a-project-in-multiple-build-configurations"></a>複数のビルド構成でプロジェクトをビルドするには

1. メニュー バーで、 **[ビルド]** 、 **[バッチ ビルド]** の順に選択します。

2. **[ビルド]** 列で、プロジェクトをビルドする構成のチェック ボックスをオンにします。

    > [!TIP]
    > ソリューションのビルド構成を編集または作成するには、メニュー バーで **[ビルド]** 、 **[構成マネージャー]** の順に選択し、 **[構成マネージャー]** ダイアログ ボックスを開きます。 ソリューションのビルド構成の編集後に、ソリューションのプロジェクトのすべてのビルド構成を更新するには、 **[バッチ ビルド]** ダイアログ ボックスで **[リビルド]** ボタンを選択します。

3. 指定した構成でプロジェクトをビルドするには、 **[ビルド]** または **[リビルド]** ボタンを選択します。

## <a name="see-also"></a>参照
 [方法: 構成を作成および編集](../ide/how-to-create-and-edit-configurations.md)する[ビルド構成につい](../ide/understanding-build-configurations.md)て[複数のプロジェクトを並行](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)してビルドする
