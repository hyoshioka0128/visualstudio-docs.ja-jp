---
title: ClickOnce 配置 API を使用したアプリの自動更新
description: ApplicationDeployment クラスを使用して、ユーザー要求などのイベントに基づいて更新プログラムを確認するコードを ClickOnce で記述する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- application updates
ms.assetid: 1a886310-67c8-44e5-a382-c2f0454f887d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f00bd8aaa5db8ab72e6b6286763fd89fc900599f
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94351259"
---
# <a name="how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api"></a>方法: ClickOnce 配置 API を使用してアプリケーションの更新プログラムをプログラムで確認する
ClickOnce には、アプリケーションを配置した後に更新する2つの方法が用意されています。 最初の方法では、特定の間隔で更新プログラムが自動的にチェックされるように ClickOnce 配置を構成できます。 2番目のメソッドでは、クラスを使用して、 <xref:System.Deployment.Application.ApplicationDeployment> ユーザー要求などのイベントに基づいて更新プログラムをチェックするコードを記述できます。

 次の手順は、プログラムによる更新を実行するためのコードを示しています。また、ClickOnce 配置を構成してプログラムによる更新チェックを有効にする方法についても説明しています。

 ClickOnce アプリケーションをプログラムで更新するには、更新プログラムの場所を指定する必要があります。 これは、配置プロバイダーと呼ばれることもあります。 このプロパティの設定の詳細については、「 [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。

> [!NOTE]
> 次に示す手法を使用して、アプリケーションを1つの場所からデプロイし、別の場所からアプリケーションを更新することもできます。 詳細については、「 [方法: 配置の更新用に別の場所を指定する](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)」を参照してください。

### <a name="to-check-for-updates-programmatically"></a>プログラムによって更新プログラムをチェックするには

1. 任意のコマンドラインまたはビジュアルツールを使用して、新しい Windows フォームアプリケーションを作成します。

2. ユーザーが更新プログラムをチェックするために選択する任意のボタン、メニュー項目、またはその他のユーザーインターフェイス項目を作成します。 その項目のイベントハンドラーから、次のメソッドを呼び出して、更新プログラムの確認とインストールを行います。

     [!code-csharp[ClickOnceAPI#6](../deployment/codesnippet/CSharp/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api_1.cs)]
     [!code-cpp[ClickOnceAPI#6](../deployment/codesnippet/CPP/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api_1.cpp)]
     [!code-vb[ClickOnceAPI#6](../deployment/codesnippet/VisualBasic/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api_1.vb)]

3. アプリケーションをコンパイルします。

### <a name="use-mageexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>Mage.exe を使用して、プログラムで更新プログラムをチェックするアプリケーションを展開する

- 「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」で説明されているように Mage.exe を使用してアプリケーションを配置する手順に従います。 配置マニフェストを生成するために Mage.exe を呼び出すときは、コマンドラインスイッチを使用し、 `providerUrl` ClickOnce が更新プログラムをチェックする URL を指定するようにしてください。 アプリケーションから更新する場合`http://www.adatum.com/MyApp`、たとえば、配置マニフェストを生成する呼び出しが、これのようになります。

    ```cmd
    mage -New Deployment -ToFile WindowsFormsApp1.application -Name "My App 1.0" -Version 1.0.0.0 -AppManifest 1.0.0.0\MyApp.manifest -providerUrl http://www.adatum.com/MyApp/MyApp.application
    ```

### <a name="using-mageuiexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>MageUI.exe を使用してプログラムによって更新プログラムをチェックするアプリケーションを展開する

- 「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」で説明されているように Mage.exe を使用してアプリケーションを配置する手順に従います。 [ **配置オプション** ] タブで、[ **開始場所** ] フィールドをアプリケーションマニフェスト ClickOnce が更新プログラムをチェックするように設定します。 [ **更新オプション** ] タブで、[ **このアプリケーションは更新プログラムを確認する** ] チェックボックスをオフにします。

## <a name="net-framework-security"></a>.NET Framework セキュリティ
 プログラムによる更新を使用するには、アプリケーションに完全信頼のアクセス許可が必要です。

## <a name="see-also"></a>関連項目
- [方法: 配置の更新用に別の場所を指定する](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)