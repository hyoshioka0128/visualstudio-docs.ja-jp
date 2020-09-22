---
title: 'チュートリアル: ClickOnce アプリケーションのカスタムインストーラーの作成 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, custom installer
- installer [ClickOnce], custom
- deploying applications [ClickOnce], custom installer
- InPlaceHostingManager [ClickOnce], custom installer
- custom installer [ClickOnce]
ms.assetid: fb222cc5-8aeb-4b94-8c49-b93e342f5f69
caps.latest.revision: 36
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9ebde75fdf36c84f40ae660a24d469c36e72ceaf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842049"
---
# <a name="walkthrough-creating-a-custom-installer-for-a-clickonce-application"></a>チュートリアル: ClickOnce アプリケーションのカスタム インストーラーの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

.Exe ファイルに基づく ClickOnce アプリケーションは、カスタムインストーラーによってサイレントインストールおよび更新できます。 カスタムインストーラーは、インストール時にカスタムのユーザーエクスペリエンスを実装できます。たとえば、セキュリティおよびメンテナンス操作のためのカスタムダイアログボックスがあります。 インストール操作を実行するために、カスタムインストーラーはクラスを使用し <xref:System.Deployment.Application.InPlaceHostingManager> ます。 このチュートリアルでは、ClickOnce アプリケーションをサイレントインストールするカスタムインストーラーを作成する方法について説明します。  
  
## <a name="prerequisites"></a>前提条件  
  
### <a name="to-create-a-custom-clickonce-application-installer"></a>カスタム ClickOnce アプリケーションインストーラーを作成するには  
  
1. ClickOnce アプリケーションで、system.servicemodel および system.string への参照を追加します。  
  
2. アプリケーションに新しいクラスを追加し、任意の名前を指定します。 このチュートリアルでは、名前 `MyInstaller` を使用します。  
  
3. 次の `Imports` または `using` ステートメントを新しいクラスの先頭に追加します。  
  
    ```vb  
    Imports System.Deployment.Application  
    Imports System.Windows.Forms  
    ```  
  
    ```csharp  
    using System.Deployment.Application;  
    using System.Windows.Forms;  
    ```  
  
4. 次のメソッドをクラスに追加します。  
  
     これらのメソッドは、メソッドを呼び出して <xref:System.Deployment.Application.InPlaceHostingManager> 配置マニフェストをダウンロードし、適切なアクセス許可をアサートして、インストールのアクセス許可をユーザーに要求してから、アプリケーションを ClickOnce キャッシュにダウンロードしてインストールします。 カスタムインストーラーでは、ClickOnce アプリケーションが事前に信頼されていることを指定できます。また、メソッド呼び出しに対して信頼の決定を延期することもでき <xref:System.Deployment.Application.InPlaceHostingManager.AssertApplicationRequirements%2A> ます。 このコードは、アプリケーションを事前に信頼します。  
  
    > [!NOTE]
    > 事前信頼によって割り当てられたアクセス許可は、カスタムインストーラーコードのアクセス許可を超えることはできません。  
  
     [!code-csharp[System.Deployment.Application.InPlaceHostingManager#1](../snippets/csharp/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/CS/Form1.cs#1)]
     [!code-vb[System.Deployment.Application.InPlaceHostingManager#1](../snippets/visualbasic/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/VB/Form1.vb#1)]  
  
5. コードからインストールを試みるには、メソッドを呼び出し `InstallApplication` ます。 たとえば、クラスにという名前を付けた場合は、 `MyInstaller` 次のようにを呼び出すことができ `InstallApplication` ます。  
  
    ```vb  
    Dim installer As New MyInstaller()  
    installer.InstallApplication("\\myServer\myShare\myApp.application")  
    MessageBox.Show("Installer object created.")  
    ```  
  
    ```csharp  
    MyInstaller installer = new MyInstaller();  
    installer.InstallApplication(@"\\myServer\myShare\myApp.application");  
    MessageBox.Show("Installer object created.");  
    ```  
  
## <a name="next-steps"></a>次の手順  
 ClickOnce アプリケーションでは、更新プロセス中に表示するカスタムユーザーインターフェイスを含む、カスタムの更新ロジックを追加することもできます。 詳細については、 <xref:System.Deployment.Application.UpdateCheckInfo> を参照してください。 ClickOnce アプリケーションでは、要素を使用して、[スタート] メニューの標準エントリ、ショートカット、および [プログラムの追加と削除] エントリを抑制することもでき `<customUX>` ます。 詳細については、「 [ \<entryPoint> 要素](../deployment/entrypoint-element-clickonce-application.md)」と「」を参照してください <xref:System.Deployment.Application.DownloadApplicationCompletedEventArgs.ShortcutAppId%2A> 。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)   
 [\<entryPoint> 要素](../deployment/entrypoint-element-clickonce-application.md)
