---
title: Emulator Express を使用したローカル コンピューターでの Azure クラウド サービスの実行とデバッグ | Microsoft Docs
description: Emulator Express を使用したローカル コンピューターでのクラウド サービス実行とデバッグ
author: mikejo5000
manager: jillfra
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 03/06/2017
ms.author: mikejo
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.openlocfilehash: 89d6662a1da987f927951937d04426b5e0b8cfa9
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846576"
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Emulator Express を使用したローカル コンピューターでの Azure クラウド サービスの実行とデバッグ
Emulator Express を使用することにより、管理者として Visual Studio を実行せずに、クラウド サービスをテストおよびデバッグできます。 クラウド サービスの要件に応じて、Emulator Express または完全なエミュレーターのどちらを使用するかをプロジェクト設定で指定できます。 完全なエミュレーターの詳細については、「[コンピューティング エミュレーターでの Azure アプリケーションの実行](/azure/storage/common/storage-use-emulator)」を参照してください。

## <a name="using-emulator-express-in-visual-studio"></a>Visual Studio での Emulator Express の使用
Azure SDK 2.3 以降で Azure プロジェクトを作成すると、Emulator Express が自動的に使用されます。 以前のバージョンの Azure SDK で作成された既存のプロジェクトは、次の手順に従って Emulator Express を選択します。

1. Visual Studio で Azure クラウド サービス プロジェクトを開くか新たに作成します。

1. **ソリューション エクスプローラー**でそのプロジェクトを右クリックし、コンテキスト メニューから **[プロパティ]** を選択します。

1. プロジェクト プロパティのページで、 **[Web]** タブを選択します。

    ![Azure クラウド サービス プロジェクトのプロパティ](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. **[ローカル開発サーバー]** で、 **[IIS Express を使用する]** オプションを選択します。

1. **[エミュレーター]** で、 **[Emulator Express を使用する]** を選択します。
   
1. Emulator Express を起動するには、コマンド プロンプトで次のコマンドを実行します。 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Emulator Express の制限事項
Emulator Express には、次のような制限事項があることがわかっています。 

- Emulator Express は IIS Web サーバーと互換性がありません。
- クラウド サービスには複数のロールを含めることができますが、各ロールのインスタンスは 1 つに制限されます。
- 1,000 未満のポート番号にはアクセスできません。 通常 1,000 未満のポートが使用される認証プロバイダーを使用する場合は、この値を 1,000 を超えるポート番号に変更する必要がある場合があります。
- Azure コンピューティング エミュレーターに適用されるすべての制限は、Emulator Express にも適用されます。 たとえば、デプロイあたり 50 を超えるロール インスタンスを保持できません。 Azure コンピューティング エミュレーターの詳細については、「[クラウド サービスのパフォーマンスのテスト](https://docs.microsoft.com/visualstudio/azure/vs-azure-tools-performance-profiling-cloud-services?view=vs-2019)」をご覧ください。

## <a name="next-steps"></a>次のステップ:
[Azure Cloud Services のデバッグ](vs-azure-tools-debugging-cloud-services-overview.md)
