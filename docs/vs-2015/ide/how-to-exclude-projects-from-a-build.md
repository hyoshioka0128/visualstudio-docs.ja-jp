---
title: '方法: ビルドからプロジェクトを除外する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 17a837ca-5db9-46cd-b5a7-b14ad1d2c47d
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ffa2b0fd8cab35fc73031d3ead8a5803558c2c07
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667944"
---
# <a name="how-to-exclude-projects-from-a-build"></a>方法: ビルドからプロジェクトを除外する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ソリューションをビルドするために、含まれるすべてのプロジェクトをビルドする必要はありません。 たとえば、ビルドを中断するプロジェクトを除外できます。 その後、問題の調査と対処を行ってからプロジェクトをビルドすることができます。

 次の方法を実行することでプロジェクトを除外できます。

- アクティブなソリューション構成からプロジェクトを一時的に削除する。

- 対象プロジェクトを含まないソリューション構成を作成する。

  詳しくは、「[ビルド構成について](../ide/understanding-build-configurations.md)」をご覧ください。

### <a name="to-temporarily-remove-a-project-from-the-active-solution-configuration"></a>アクティブなソリューション構成からプロジェクトを一時的に削除するには

1. メニュー バーで **[ビルド]** 、 **[構成マネージャー]** の順に選択します。

2. **[プロジェクトのコンテキスト]** テーブルで、ビルドから除外するプロジェクトを見つけます。

3. プロジェクトの **[ビルド]** 列で、チェック ボックスをオフにします。

4. **[閉じる]** を選択し、ソリューションをリビルドします。

### <a name="to-create-a-solution-configuration-that-excludes-a-project"></a>プロジェクトを除外するソリューション構成を作成するには

1. メニュー バーで **[ビルド]** 、 **[構成マネージャー]** の順に選択します。

2. **[アクティブ ソリューション構成]** 一覧の **[\<新規作成>]** を選択します。

3. **[名前]** ボックスに、ソリューション構成の名前を入力します。

4. **[設定のコピー元]** ボックスの一覧で、新しい構成のベースにするソリューション構成 ( **[デバッグ]** など) を選択し、 **[OK]** を選択します。

5. **[構成マネージャー]** ダイアログ ボックスで、除外するプロジェクトの **[ビルド]** 列のチェック ボックスをオフにし、 **[閉じる]** を選択します。

6. **[標準]** ツール バーで、 **[ソリューション構成]** ボックスのアクティブな構成が、新しいソリューション構成であることを確認します。

7. メニュー バーから、 **[ビルド]** 、 **[ソリューションのリビルド]** の順に選びます。

## <a name="see-also"></a>参照
 [ビルド構成につい](../ide/understanding-build-configurations.md)[て方法: 構成を作成および編集](../ide/how-to-create-and-edit-configurations.md)する[方法: 複数の構成を同時にビルド](../ide/how-to-build-multiple-configurations-simultaneously.md)する
