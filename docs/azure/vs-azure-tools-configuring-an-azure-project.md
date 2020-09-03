---
title: Azure クラウド サービス プロジェクトを構成する
description: Visual Studio で、そのプロジェクトの要件に応じて、Azure クラウド サービス プロジェクトを構成する方法について説明します。
author: ghogen
manager: jillfra
assetId: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 03/06/2017
ms.author: ghogen
ms.openlocfilehash: 7f207afc600402924969e4d2eee6df229c3d6f09
ms.sourcegitcommit: a3edc753c951f317b67ce294cd2fc74f0c45390c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "89426721"
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Visual Studio で Azure クラウド サービス プロジェクトを構成する
Azure クラウド サービス プロジェクトは、そのプロジェクトの要件に応じて構成できます。 次のカテゴリに関して、プロジェクトのプロパティを設定できます。

- **クラウド サービスを Azure に発行する** - Azure にデプロイされた既存のクラウド サービスが誤って削除されないようにするためのプロパティを設定できます。
- **ローカルコンピューターでクラウドサービスを実行またはデバッグ** する-使用するサービス構成を選択し、Azure Storage エミュレーターを起動するかどうかを指定できます。
- **クラウド サービス パッケージを作成時に検証する** - クラウド サービス パッケージを問題のない状態で確実にデプロイできるように、すべての警告をエラーとして処理できます。

## <a name="steps-to-configure-an-azure-cloud-service-project"></a>Azure クラウド サービス プロジェクトを構成する手順
1. Visual Studio でクラウド サービス プロジェクトを開くか作成します。

1. **ソリューション エクスプローラー**でそのプロジェクトを右クリックし、コンテキスト メニューから **[プロパティ]** を選択します。

1. プロジェクトのプロパティ ページで **[開発]** タブを選択します。

    ![プロジェクトのプロパティ メニュー](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. **[既存の配置を削除する前にプロンプトで確認します]** を **[True]** に設定します。 この設定により、Azure で既存のデプロイが誤って削除されないようにすることができます。

1. クラウド サービスをローカルで実行またはデバッグするときに使用する**サービス構成**を選択します。 ロールのサービス構成を変更する方法の詳細については、[Visual Studio で Azure クラウド サービスのロールを構成する方法](./vs-azure-tools-configure-roles-for-cloud-service.md)に関する記事をご覧ください。

1. クラウドサービスをローカルで実行またはデバッグするときに Azure Storage エミュレーターを起動するには、[ **開始 Azure Storage エミュレーター** を **True** に設定します。

1. パッケージの検証エラーがある場合には発行できないようにするには、**[警告をエラーとして扱う]** を **[True]** に設定します。

1. IIS Express で Web ロールがローカルで開始されるときに毎回同じポートが使用されるようにするには、**[Web プロジェクト ポートの使用]** を **[True]** に設定します。

1. Visual Studio ツール バーの **[保存]** を選択します。

## <a name="next-steps"></a>次のステップ
- [複数のサービス構成を使用した Azure プロジェクトの構成](vs-azure-tools-multiple-services-project-configurations.md)
