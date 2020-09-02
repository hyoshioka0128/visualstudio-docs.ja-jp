---
title: '方法: ClickOnce アプリケーションの更新プログラムを管理する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.Update
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, managing applications
- ClickOnce deployment, updates
- updating data, ClickOnce
- application updates
ms.assetid: a3f23f05-e7f1-4620-b23c-2d68f9643684
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0754d816104832f92a0be8d754046d1ee18e7a09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697647"
---
# <a name="how-to-manage-updates-for-a-clickonce-application"></a>方法 : ClickOnce アプリケーションの更新プログラムを管理する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションでは、更新プログラムを自動的にチェックするか、プログラムによって確認できます。 開発者は、更新プログラムのチェックを実行するタイミングと方法、更新プログラムが必須かどうか、アプリケーションが更新プログラムをチェックする場所などを柔軟に指定できます。  
  
 アプリケーションを開始する前に自動的に更新プログラムをチェックするようにアプリケーションを構成することも、アプリケーションの起動後に設定することもできます。 また、最低限必要なバージョンを指定することもできます。つまり、ユーザーのバージョンが必要なバージョンより古い場合は、更新プログラムがインストールされます。  
  
 ユーザー要求などのイベントに基づいて、プログラムで更新プログラムをチェックするようにアプリケーションを構成できます。 このトピックの「プログラムによって更新プログラムを確認するには」の手順では、クラスを使用して、 <xref:System.Deployment.Application.ApplicationDeployment> イベントに基づいて更新プログラムをチェックするコードを記述する方法を示します。  
  
 また、アプリケーションを1つの場所から配置し、別の場所から更新することもできます。 「別の更新の場所を指定するには」の手順を参照してください。  
  
 詳細については、「[ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。  
  
 更新動作は、プロジェクトデザイナーの [**発行**] ページから使用できる [**アプリケーションの更新プログラム**] ダイアログボックスで管理され**ます。**  
  
### <a name="to-check-for-updates-before-the-application-starts"></a>アプリケーションを起動する前に更新プログラムを確認するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **更新** ] ボタンをクリックして、[ **アプリケーションの更新** ] ダイアログボックスを開きます。  
  
4. [ **アプリケーションの更新プログラム** ] ダイアログボックスで、[ **アプリケーションの更新プログラムを確認する** ] チェックボックスがオンになっていることを確認します。  
  
5. [ **アプリケーションが更新プログラムを確認するタイミングを選択** してください] セクションで、[ **アプリケーションの開始前に**] を選択します。 これにより、ネットワークに接続されているユーザーは常に最新の更新プログラムを使用してアプリケーションを実行します。  
  
### <a name="to-check-for-updates-in-the-background-after-the-application-starts"></a>アプリケーションの起動後に、バック グラウンドで更新プログラムを確認するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **更新** ] ボタンをクリックして、[ **アプリケーションの更新** ] ダイアログボックスを開きます。  
  
4. [ **アプリケーションの更新プログラム** ] ダイアログボックスで、[ **アプリケーションの更新プログラムを確認する** ] チェックボックスがオンになっていることを確認します。  
  
5. [ **アプリケーションが更新プログラムを確認するタイミングを選択**してください] セクションで、[ **アプリケーションの開始後**] を選択します。 このようにすると、アプリケーションの起動が速くなり、バックグラウンドで更新プログラムがチェックされ、更新プログラムが利用可能になったときにのみユーザーに通知されます。 インストールが完了すると、アプリケーションが再起動されるまで更新は有効になりません。  
  
6. [ **アプリケーションが更新プログラムを確認する頻度を指定** してください] セクションで、[ **アプリケーションが実行される** たびにチェックする (既定)] または [すべてを **確認** ] を選択し、数値と時間間隔を入力します。  
  
### <a name="to-specify-a-minimum-required-version-for-the-application"></a>アプリケーションに最低限必要なバージョンを指定するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **更新** ] ボタンをクリックして、[ **アプリケーションの更新** ] ダイアログボックスを開きます。  
  
4. [ **アプリケーションの更新プログラム** ] ダイアログボックスで、[ **アプリケーションの更新プログラムを確認する** ] チェックボックスがオンになっていることを確認します。  
  
5. [ **このアプリケーションに最低限必要なバージョンを指定する** ] チェックボックスをオンにして、アプリケーションの **メジャー**番号、 **マイナー**番号、 **ビルド**番号、 **リビジョン** 番号を入力します。  
  
### <a name="to-specify-a-different-update-location"></a>別の更新プログラムの場所を指定するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **更新** ] ボタンをクリックして、[ **アプリケーションの更新** ] ダイアログボックスを開きます。  
  
4. [ **アプリケーションの更新プログラム** ] ダイアログボックスで、[ **アプリケーションの更新プログラムを確認する** ] チェックボックスがオンになっていることを確認します。  
  
5. [ **更新の場所** ] フィールドに、完全修飾 URL を使用して更新の場所を入力します。その際、形式を使用し http://Hostname/ApplicationName ます。または、\ \ (\) の形式で UNC パスを入力 \\ するか、[ **参照** ] ボタンをクリックして更新の場所を参照します。  
  
### <a name="to-check-for-updates-programmatically"></a>プログラムによって更新プログラムをチェックするには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[公開]** タブをクリックします。  
  
3. [ **更新** ] ボタンをクリックして、[ **アプリケーションの更新** ] ダイアログボックスを開きます。  
  
4. [ **アプリケーションの更新プログラム** ] ダイアログボックスで、[ **アプリケーションが更新プログラムを確認する必要が** ある] チェックボックスがオフになっていることを確認します。 (必要に応じて、このチェックボックスをオンにすると、プログラムによって更新プログラムがチェックされ、ClickOnce ランタイムが更新プログラムを自動的にチェックできるようになります)。  
  
5. [ **更新の場所** ] フィールドに、完全修飾 URL を使用して更新の場所を入力します。その際、形式を使用し http://Hostname/ApplicationName ます。または、\ \ (\) の形式で UNC パスを入力 \\ するか、[ **参照** ] ボタンをクリックして更新の場所を参照します。 更新プログラムの場所は、アプリケーションが更新されたバージョンを検索する場所です。  
  
6. ユーザーが更新プログラムをチェックするために選択する、Windows フォーム上のボタン、メニュー項目、またはその他のユーザーインターフェイス項目を作成します。 その項目のイベントハンドラーから、メソッドを呼び出して更新プログラムを確認し、インストールします。 Visual Basic と Visual C# のコード例については、 [「方法: ClickOnce 配置 API を使用してプログラムによってアプリケーションの更新プログラムを確認する](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)」を参照してください。  
  
7. アプリケーションをビルドします。  
  
## <a name="see-also"></a>参照  
 <xref:System.Deployment.Application.ApplicationDeployment>   
 [[アプリケーションの更新] ダイアログボックス](https://msdn.microsoft.com/8eca8743-8e68-4d04-bfd5-4dc0a9b2934f)   
 [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)   
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)   
 [方法: ClickOnce 配置 API を使用してプログラムによってアプリケーションの更新プログラムを確認する](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)
