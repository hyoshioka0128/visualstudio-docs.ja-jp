---
title: '方法: ユーザーアカウントでワーカープロセスを実行する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- user accounts, aspnet_wp.exe
- ASP.NET, debugging Web applications
- tools, aspnet_wp.exe
- ASP.NET, tools
- aspnet_wp.exe
ms.assetid: b58e97b1-e62a-4318-aea4-52276ea20735
caps.latest.revision: 35
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ebb8ec1fe10f6fbc5c367cb0ed127e048351b0e4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157871"
---
# <a name="how-to-run-the-worker-process-under-a-user-account"></a>方法: ユーザー アカウントでワーカー プロセスを実行する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユーザー アカウントを使用して [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセス (aspnet_wp.exe または w3wp.exe) を実行できるようにコンピューターを設定するには、次の手順を実行します。  
  
## <a name="procedure"></a>プロシージャ  
  
#### <a name="to-run-aspnet_wpexe-under-a-user-account"></a>ユーザー アカウントで aspnet_wp.exe を実行するには  
  
1. コンピューターでランタイムをインストールしたパスの CONFIG フォルダーにある machine.config ファイルを開きます。  
  
2. &lt;processModel&gt; セクションを見つけ、user 属性と password 属性を、aspnet_wp.exe を実行するユーザー アカウントの名前とパスワードに変更します。  
  
3. machine.config ファイルを保存します。  
  
4. [!INCLUDE[winxpsvr](../includes/winxpsvr-md.md)] では、既定で、IIS 6.0 がインストールされます。 対応するワーカー プロセスは w3wp.exe です。aspnet_wp.exe をワーカー プロセスとして IIS 6.0 モードで実行するには、次の手順を実行します。  
  
    1. **[スタート]** ボタンをクリックし、 **[管理ツール]** をポイントして、 **[インターネット インフォメーション サービス (IIS) マネージャー]** をクリックします。  
  
    2. **[インターネット インフォメーション サービス]** ダイアログ ボックスの **[Web サイト]** フォルダーを右クリックし、 **[プロパティ]** を選択します。  
  
    3. **[Web サイトのプロパティ]** ダイアログ ボックスの **[サービス]** を選択します。  
  
    4. **[IIS 6.0 プロセス分離モードで WWW サービスを実行する]** をオンにします。  
  
    5. **[プロパティ]** ダイアログ ボックスを閉じ、 **[インターネット サービス マネージャー]** を閉じます。  
  
5. Windows のコマンド プロンプトを開き、次を実行してサーバーをリセットします。  
  
    ```  
    iisreset  
    ```  

    または  
  
    ```  
    net stop iisadmin /y  
    net start w3svc  
    ```  
  
6. [Temporary [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Files] フォルダーを探します。このフォルダーは、[CONFIG] フォルダーと同じパスにあります。 [Temporary [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Files] フォルダーを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。  
  
7. **[Temporary ASP.NET Files のプロパティ]** ダイアログ ボックスで、 **[セキュリティ]** タブをクリックします。  
  
8. **[詳細設定]** をクリックします。  
  
9. **[Temporary ASP.Net Files のセキュリティの詳細設定]** ダイアログ ボックスで、 **[追加]** をクリックします。  
  
    **[ユーザー、コンピューターまたはグループの選択]** ダイアログ ボックスが表示されます。  
  
10. **[選択するオブジェクト名を入力してください]** ボックスに、ユーザー名を入力して、 **[OK]** をクリックします。 ユーザー名は、次の形式で入力する必要があります: ドメイン名\ユーザー名。  
  
11. **[Temporary ASP.NET Files のアクセス許可のエントリ]** ダイアログ ボックスで、ユーザーに**フル コントロール**を付与し、 **[OK]** をクリックして **[Temporary ASP.NET Files のアクセス許可のエントリ]** ダイアログ ボックスを閉じます。  
  
12. **[セキュリティ]** ダイアログ ボックスが表示され、システム フォルダーのアクセス許可を本当に変更するかどうかの確認が求められます。 **[はい]** をクリックします。  
  
13. **[OK]** をクリックして、 **[Temporary ASP.NET Files のプロパティ]** ダイアログ ボックスを閉じます。  
  
## <a name="see-also"></a>参照  
[ASP.NET のデバッグ: システム要件](../debugger/aspnet-debugging-system-requirements.md)  
