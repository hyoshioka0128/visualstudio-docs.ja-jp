---
title: '方法: アクセス許可を設定する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling, setting permissions
- security [Visual Studio ALM], setting permissions
- permissions [Visual Studio ALM], profiling
- profiling tools, setting profiling permissions
- performance tools, setting profiling permissions
ms.assetid: 69f27896-8f46-4ef3-bfb7-726d95304f3a
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 03991f3d5900377ceca5464bf41cfb90fcae650e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842316"
---
# <a name="how-to-set-permissions"></a>方法: アクセス許可を設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、コンピューターの管理者が、プロファイリングに必要なセキュリティ アクセス許可を、そのコンピューター上で管理者アクセス許可を持たないユーザーまたはグループに付与する方法について説明します。  
  
 基本的なセキュリティ原則として、必要以上のアクセス許可でアプリケーションを実行しないことが規定されています。 この原則は、ユーザーにも適用されます。 ユーザーが Administrators グループではなく Users グループのメンバーとしてログオンしても必要な操作をすべて行うことができるのであれば、ユーザーに管理者アクセス許可を与えないでください。 最初の手順「ユーザー アクセス許可を持つユーザー アカウントを作成するには」では、Users グループのメンバーのユーザー アカウントを作成する方法を説明します。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  Users グループのメンバーの場合は、チームの他のメンバーとの間で共有されるディスク上のフォルダーおよびファイルにアクセスする必要があります。 2 番目の手順「共有プロジェクト ファイルへのアクセスを許可するには」では、そのアクセスを許可する方法を説明します。  
  
  管理者が Users グループのメンバーにプロファイリング ツールのソフトウェア ドライバーへのアクセスを許可すると、メンバーはプロファイリング ツールを実行できます。 最後の手順「プロファイリング ドライバーへのアクセスを許可するには」では、ドライバーへのアクセスを許可する方法について説明します。  
  
> [!NOTE]
> これらの手順を実行するには、管理者アクセス許可が必要です。  
  
### <a name="to-create-a-user-account-that-has-user-permissions"></a>ユーザー アクセス許可を持つユーザー アカウントを作成するには  
  
1. **[マイ コンピューター]** を右クリックし、次いで **[管理]** をクリックします。  
  
     **[コンピューターの管理]** ウィンドウが開きます。  
  
2. **[ローカル ユーザーとグループ]** を展開します。  
  
3. **[ユーザー]** フォルダーを右クリックし、 **[新しいユーザー]** をクリックします。  
  
     **[新しいユーザー]** ダイアログ ボックスが表示されます。  
  
4. 作成するユーザー アカウントの情報をこのダイアログ ボックスのフィールドに入力します。 パスワードを指定します。 必要に応じて、ユーザーが次のログオン時にパスワードを変更することを求めるチェック ボックスを選択します。  
  
5. **[作成]** をクリックし、 **[閉じる]** をクリックします。  
  
     Users グループに新しいユーザーが作成されます。このグループのユーザーには、管理者アクセス許可が与えられていません。  
  
### <a name="to-grant-access-to-shared-project-files"></a>共有プロジェクト ファイルへのアクセスを許可するには  
  
1. エクスプローラーで、このユーザーによって使用され、プロジェクト チームで共有されるプロジェクト ファイルのフォルダー ツリーのルートを見つけます。  
  
     このフォルダーのパスの一例を次に示します。  
  
    ```  
    D:\ourProject  
    ```  
  
2. フォルダーを右クリックし、 **[プロパティ]** をクリックします。  
  
     **[\<folder name> プロパティ]** ダイアログ ボックスが表示されます。  
  
3. **[セキュリティ]** タブをクリックします。  
  
4. **[グループ名またはユーザー名]** ボックスにあるユーザーのアカウント名をクリックします。  
  
5. **[\<user name> のアクセス許可]** ボックスで、 **[フル コントロール]** のチェック ボックスを選択します。  
  
6. **[OK]** をクリックします。  
  
     これにより、手順 5 で選択されたフォルダーで始まる共有フォルダー ツリーに対するアクセス許可がユーザーに付与されます。  
  
### <a name="to-grant-access-to-the-profiling-driver"></a>プロファイリング ドライバーへのアクセスを許可するには  
  
1. 管理者としてコマンド プロンプトを開きます。  
  
2. 次のディレクトリに移動します。  
  
   ```  
   <drive>:\Program Files\Microsoft Visual Studio 10\Team Tools\Performance Tools  
   ```  
  
3. 次のコマンドを実行します。  
  
   ```  
   vsperfcmd /admin:driver,start /admin:service,start  
   ```  
  
    このコマンドによって、プロファイリング ツールのドライバーがインストールされ、開始します。  
  
    このコマンドによってプロファイリング ドライバーとサービスが開始され、管理者以外のユーザーがユーザーのプロセス空間で使用可能なプロファイリング機能を使用できるようになります。 このコマンドは管理者だけが実行でき、管理者以外のユーザーの場合は失敗します。  
  
    この一連の手順の最後の手順も実行しない限り、この手順の効果はコンピューターの再起動時に無効になります。  
  
4. コンピューターへの管理者アクセス許可を持たないユーザーまたはグループがプロファイリング ドライバー機能にアクセスできるようにするために、次のコマンドを実行します。  
  
   ```  
   vsperfcmd /admin:security,allow,<right[,right],<user name|group name>  
   ```  
  
    このコマンドにより、\<user name> または \<group name> アカウントにプロファイリング ツールへのアクセス許可が付与されます。 \<right> オプションは、ユーザーがアクセスできるプロファイリング機能を決定します。 \<right> オプションには次の値の 1 つ以上を指定できます。  
  
   - FullAccess - サービスからのパフォーマンス データの収集、サンプリング、セッション間のプロファイリングを含むすべてのプロファイリング メソッドへのアクセスを許可します。  
  
   - SampleProfiling - サンプル プロファイリング メソッドへのアクセスを許可します。  
  
   - CrossSession - プロファイリング サービスに必要なセッション間のプロファイリングへのアクセスを許可します。  
  
5. (省略可能) コンピューターの再起動後に前の手順の結果を維持する場合は、次のコマンドを実行します。  
  
   ```  
   vsperfcmd /admin:driver,autostart,on  
   ```  
  
   指定されたユーザーは、ログオン後に、管理者アクセス許可なしにプロファイリング ツールを使用できるようになります。  
  
## <a name="see-also"></a>参照  
 [パフォーマンスセッションの構成](../profiling/configuring-performance-sessions.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [プロファイルと Windows Vista のセキュリティ](../profiling/profiling-and-windows-vista-security.md)
