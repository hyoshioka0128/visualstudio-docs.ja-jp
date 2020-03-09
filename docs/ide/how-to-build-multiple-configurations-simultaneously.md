---
title: '方法: 複数の構成を同時にビルドする'
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
ms.assetid: ba830937-3317-4674-8cc2-c0cd565603c5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 33cd217a08f62b4919af6d72017176c110cf5e5a
ms.sourcegitcommit: b016ea260856264eee730ee8cbcab198314a7ece
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "77904088"
---
# <a name="how-to-build-multiple-configurations-simultaneously"></a>方法: 複数の構成を同時にビルドする

**[バッチ ビルド]** ダイアログ ボックスを使用すると、複数、またはすべてのプロジェクト ビルド構成で、ほとんどの種類のプロジェクトを同時にビルドできます。 ただし、次の種類のプロジェクトは、複数のビルド構成で同時にビルドすることはできません。

1. JavaScript を使用して Windows 用にビルドされた [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] アプリ。

2. すべての Visual Basic プロジェクト。

この 2 つのプロジェクト タイプに該当するプロジェクトがソリューションに含まれている場合、そのソリューションでは **[バッチ ビルド]** を利用できません。 この場合、そのコマンドは **[ビルド]** メニューに表示されません。

   ビルド構成の詳細については、「[ビルド構成について](../ide/understanding-build-configurations.md)」を参照してください。

## <a name="to-build-a-project-in-multiple-build-configurations"></a>複数のビルド構成でプロジェクトをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[バッチ ビルド]** の順に選択します。 または、**Ctrl** + **Q** キーを押して検索ボックスを開き、「`Batch Build`」を検索します。

2. **[ビルド]** 列で、プロジェクトをビルドする構成のチェック ボックスをオンにします。

    > [!TIP]
    > ソリューションのビルド構成を編集または作成するには、メニュー バーで **[ビルド]**  >  **[構成マネージャー]** の順に選択し、 **[構成マネージャー]** ダイアログ ボックスを開きます。 ソリューションのビルド構成の編集後に、ソリューションのプロジェクトのすべてのビルド構成を更新するには、 **[バッチ ビルド]** ダイアログ ボックスで **[リビルド]** ボタンを選択します。

3. 指定した構成でプロジェクトをビルドするには、 **[ビルド]** または **[リビルド]** ボタンを選択します。

## <a name="see-also"></a>関連項目

- [方法: 構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)
- [ビルド構成について](../ide/understanding-build-configurations.md)
- [複数プロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)