---
title: System.object を使用する ClickOnce アプリケーションのデバッグ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, debugging
- debugging, ClickOnce applications
- debugging, System.Deployment
- deploying applications [ClickOnce], debugging
ms.assetid: 86f31948-2ca8-47c0-8e8b-c2b817bbf79f
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c0b12faf451d3ed9bb70e2bb1ec6c8503cfb86d5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187792"
---
# <a name="debugging-clickonce-applications-that-use-systemdeploymentapplication"></a>System.Deployment.Application を使用する ClickOnce アプリケーションのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

で [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] は、展開を使用して、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションの更新方法を構成できます。 ただし、高度な配置機能を使用してカスタマイズする必要がある場合 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] は、によって提供される配置オブジェクトモデルにアクセスする必要があり <xref:System.Deployment.Application> ます。 Api は、 <xref:System.Deployment.Application> 次のような高度なタスクに使用できます。  
  
- アプリケーションで [今すぐ更新] オプションを作成する  
  
- さまざまなアプリケーションコンポーネントの条件付きオンデマンドダウンロード  
  
- アプリケーションに直接統合された更新プログラム  
  
- クライアントアプリケーションが常に最新であることを保証する  
  
  Api は、 <xref:System.Deployment.Application> アプリケーションがテクノロジと共に配置されている場合にのみ機能するため、を [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 使用してアプリケーションを配置し、アタッチしてからデバッグするだけです [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 。 デバッガーをアタッチする前にアプリケーションを起動して実行すると、多くの場合、デバッガーをアタッチすることが困難になる可能性があります。 解決策として、更新チェックコードまたはオンデマンドコードの前に、中断 (または Visual Basic プロジェクトの場合は停止) を行うことができます。  
  
  推奨されるデバッグ手法は次のとおりです。  
  
1. 開始する前に、シンボル (.pdb) ファイルとソースファイルがアーカイブされていることを確認します。  
  
2. バージョン1のアプリケーションを展開します。  
  
3. 新しい空のソリューションを作成します。 **[ファイル]** メニューから **[新規作成]**、**[プロジェクト]** の順にクリックします。 [ **新しいプロジェクト** ] ダイアログボックスで、[ **その他のプロジェクトの種類** ] ノードを開き、[ **Visual Studio Solutions** ] フォルダーを選択します。 [ **テンプレート** ] ペインで、[ **空のソリューション**] を選択します。  
  
4. アーカイブされたソースの場所を、この新しいソリューションのプロパティに追加します。 **ソリューションエクスプローラー**で、ソリューションノードを右クリックし、[**プロパティ**] をクリックします。 [ **プロパティページ** ] ダイアログボックスで、[ **デバッグソースファイル**] を選択し、アーカイブされたソースコードのディレクトリを追加します。 それ以外の場合、ソースファイルのパスは .pdb ファイルに記録されるため、古いソースファイルがデバッガーによって検出されます。 デバッガーで古いソースファイルが使用されている場合は、ソースが一致しないことを示すメッセージが表示されます。  
  
5. デバッガーが .pdb ファイルを見つけられることを確認します。 アプリケーションを使用して配置した場合は、デバッガーによって自動的に検出されます。 常に、問題のアセンブリの横に表示されます。 それ以外の場合は、 **シンボルファイル (.pdb) の場所** にアーカイブパスを追加する必要があります (このオプションにアクセスするには、[ **ツール** ] メニューの [ **オプション**] をクリックし、[ **デバッグ** ] ノードを開き、[ **シンボル**] をクリックします)。  
  
6. メソッドとメソッドの呼び出しの間の動作 `CheckForUpdate` をデバッグ `Download` / `Update` します。  
  
    たとえば、更新コードは次のようになります。  
  
   ```  
       Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
           If My.Application.Deployment.IsNetworkDeployed Then  
  
               If (My.Application.Deployment.CheckForUpdate()) Then  
  
                   My.Application.Deployment.Update()  
                   Application.Restart()  
  
               End If  
  
           End If  
       End Sub  
   ```  
  
7. バージョン2を展開します。  
  
8. バージョン2の更新プログラムをダウンロードするときに、バージョン1のアプリケーションにデバッガーをアタッチしようとしました。 また `System.Diagnostics.Debugger.Break` は、メソッドまたは単に Visual Basic を使用することもでき `Stop` ます。 もちろん、これらのメソッド呼び出しを実稼働コードに残してはいけません。  
  
    たとえば、Windows フォームアプリケーションを開発していて、更新ロジックがこのメソッドのイベントハンドラーに含まれているとします。 これをデバッグするには、ボタンが押される前にをアタッチし、ブレークポイントを設定します (適切なアーカイブファイルを開いて、そこにブレークポイントを設定してください)。  
  
   プロパティは、 <xref:System.Deployment.Application.ApplicationDeployment.IsNetworkDeployed%2A> <xref:System.Deployment.Application> アプリケーションが配置されている場合にのみ api を呼び出すために使用します。でデバッグ中に api を呼び出すことはできません [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
## <a name="see-also"></a>参照  
 <xref:System.Deployment.Application>
