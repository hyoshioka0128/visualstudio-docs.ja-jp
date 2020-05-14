---
title: '方法 : ClickOnce 配置 API を使用してプログラムでアプリケーションの更新を確認する |マイクロソフトドキュメント'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- application updates
ms.assetid: 1a886310-67c8-44e5-a382-c2f0454f887d
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5250e719cce945bdcce90a9d49d2ed8c27555612
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444980"
---
# <a name="how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api"></a>方法 : ClickOnce 配置 API を使用してアプリケーションの更新プログラムをプログラムで確認する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ClickOnce には、配置後にアプリケーションを更新する方法が 2 つあります。 最初のメソッドでは、ClickOnce 配置を構成して、特定の間隔で更新プログラムを自動的にチェックするように設定できます。 2 番目のメソッドでは、クラスを<xref:System.Deployment.Application.ApplicationDeployment>使用して、ユーザー要求などのイベントに基づいて更新をチェックするコードを記述できます。  
  
 次の手順では、プログラムによる更新を実行するためのコードと、プログラムによる更新チェックを有効にするように ClickOnce 配置を構成する方法について説明します。  
  
 ClickOnce アプリケーションをプログラムで更新するには、更新の場所を指定する必要があります。 これは、デプロイメント プロバイダーと呼ばれることもあります。 このプロパティの設定の詳細については、「 [ClickOnce 更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。  
  
> [!NOTE]
> また、次に説明する手法を使用して、アプリケーションをある場所からデプロイし、別の場所からアプリケーションを更新することもできます。 詳細については、「[方法 : 展開の更新の代替場所を指定する](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)」を参照してください。  
  
### <a name="to-check-for-updates-programmatically"></a>プログラムによって更新プログラムをチェックするには  
  
1. 任意のコマンド ライン ツールまたはビジュアル ツールを使用して、新しい Windows フォーム アプリケーションを作成します。  
  
2. ユーザーが更新をチェックするために選択するボタン、メニュー項目、またはその他のユーザー インターフェイス項目を作成します。 その項目のイベント ハンドラーから、更新プログラムを確認およびインストールする次のメソッドを呼び出します。  
  
     [!code-cpp[ClickOnceAPI#6](../snippets/cpp/VS_Snippets_Winforms/ClickOnceAPI/cpp/form1.cpp#6)]
     [!code-csharp[ClickOnceAPI#6](../snippets/csharp/VS_Snippets_Winforms/ClickOnceAPI/CS/Form1.cs#6)]
     [!code-vb[ClickOnceAPI#6](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceAPI/VB/Form1.vb#6)]  
  
3. アプリケーションをコンパイルします。  
  
### <a name="using-mageexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>Mage.exe を使用して、プログラムで更新プログラムをチェックするアプリケーションを展開する  
  
- Mage.exe を使用してアプリケーションを配置する手順に従ってください[。](../deployment/walkthrough-manually-deploying-a-clickonce-application.md) Mage.exe を呼び出して配置マニフェストを生成する場合は、必ずコマンド`providerUrl`ライン スイッチ を使用し、ClickOnce が更新を確認する URL を指定してください。 アプリケーションから更新する場合`http://www.adatum.com/MyApp`、たとえば、配置マニフェストを生成する呼び出しが、これのようになります。  
  
    ```  
    mage -New Deployment -ToFile WindowsFormsApp1.application -Name "My App 1.0" -Version 1.0.0.0 -AppManifest 1.0.0.0\MyApp.manifest -providerUrl http://www.adatum.com/MyApp/MyApp.application  
    ```  
  
### <a name="using-mageuiexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>プログラムで更新をチェックするアプリケーションを MageUI.exe を使用して展開する  
  
- Mage.exe を使用してアプリケーションを配置する手順に従ってください[。](../deployment/walkthrough-manually-deploying-a-clickonce-application.md) [**配置オプション]** タブで、[**開始場所**] フィールドをアプリケーション マニフェストに設定します。 [**更新オプション]** タブで、[**このアプリケーションは更新を確認する]** チェック ボックスをオフにします。  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
 アプリケーションは、プログラムによる更新を使用するために完全に信頼できるアクセス許可を持っている必要があります。  
  
## <a name="see-also"></a>参照  
 [方法: 展開の更新の代替場所を指定する](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)   
 [クリックワンス更新戦略の選択](../deployment/choosing-a-clickonce-update-strategy.md)   
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
