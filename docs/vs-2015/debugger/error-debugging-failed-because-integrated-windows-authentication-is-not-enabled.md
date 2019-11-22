---
title: 'Error: Debugging Failed Because Integrated Windows Authentication Is Not Enabled | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.webdbg_ntlm_authn_not_enabled
dev_langs:
- FSharp
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: 6027cd94-74cf-470f-b7ce-6f6b68bc56ba
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4c8c83676c8f01891aed97e931581c65b799e61e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299791"
---
# <a name="error-debugging-failed-because-integrated-windows-authentication-is-not-enabled"></a>エラー ： Windows 統合認証が無効になっているため、デバッグに失敗しました。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デバッグを要求したユーザーの認証が認証エラーで失敗しました。 このエラーは、Web アプリケーションまたは XML Web サービスにステップ インしようとするときに発生することがあります。 このエラーの原因の 1 つとして、統合 Windows 認証が有効ではないことが挙げられます。 その機能を有効にする場合は、「統合 Windows 認証を有効にするには」の手順を実行します。  
  
 統合 Windows 認証を有効にしていてもこのエラーが表示される場合は、 **[Windows ドメイン サーバーでダイジェスト認証を使用する]** が有効なためにエラーが発生した可能性があります。 この場合は、ネットワーク管理者に問い合わせてください。  
  
### <a name="to-enable-integrated-windows-authentication"></a>統合 Windows 認証を有効にするには  
  
1. 管理者アカウントを使って Web サーバーにログオンします。  
  
2. **[スタート]** ボタンをクリックし、**コントロール パネル** をクリックします。  
  
3. **[コントロール パネル]** で、 **[管理ツール]** をダブルクリックします。  
  
4. **[インターネット インフォメーション サービス]** をダブルクリックします。  
  
5. Web サーバー ノードをクリックします。  
  
     サーバー名の下に **[Web サイト]** フォルダーが表示されます。  
  
6. 認証の設定は、すべての Web サイトまたは個々の Web サイトについて行うことができます。 すべての Web サイトについて認証を設定するには、 **[Web サイト]** フォルダーを右クリックしてから、 **[プロパティ]** をクリックします。 個々の Web サイトについて認証を設定するには、 **[Web サイト]** フォルダーを開き、個々の Web サイトを右クリックして、 **[プロパティ]** をクリックします。  
  
     **[プロパティ]** ダイアログ ボックスが表示されます。  
  
7. **[ディレクトリ セキュリティ]** タブをクリックします。  
  
8. **[匿名アクセスおよび認証コントロール]** セクションの **[編集]** をクリックします。  
  
     **[認証方法]** ダイアログ ボックスが表示されます。  
  
9. **[認証済みアクセス]** の **[統合 Windows 認証]** を選択します。  
  
10. **[OK]** をクリックして **[認証方法]** ダイアログ ボックスを閉じます。  
  
11. **[OK]** をクリックして、 **[プロパティ]** ダイアログ ボックスを閉じます。  
  
12. **[インターネット インフォメーション サービス]** ウィンドウを閉じます。  
  
### <a name="to-enable-integrated-windows-authentication-in-windows-vistaiis-7"></a>Windows Vista/IIS 7 で統合 Windows 認証を有効にするには  
  
1. 管理者アカウントを使って Web サーバーにログオンします。  
  
2. Windows 認証と II6 管理互換の機能を有効にするために、以下の手順をまだ実行していなければ、この手順を実行します。  
  
    1. クリックして**開始**、をクリックして **コントロール パネルの** 順にクリックします**プログラム**します。  
  
    2. **[プログラムと機能]** で **[Windows の機能を有効化または無効化]** をクリックします。  
  
         続行するかどうかの確認を求める [ユーザー アカウント制御] ダイアログ ボックスが表示されます。  
  
    3. **[続行]** をクリックします。  
  
         [Windows の機能] ダイアログ ボックスが表示されます。  
  
    4. 機能の一覧で **[インターネット インフォメーション サービス]** ノードを展開します。  
  
    5. **[インターネット インフォメーション サービス]** の **[World Wide Web サービス]** ノードを展開します。  
  
    6. **[World Wide Web サービス]** の **[セキュリティ]** をクリックします。  
  
    7. **[Windows 認証]** をクリックします。  
  
    8. **[インターネット インフォメーション サービス]** の **[Web 管理ツール]** ノードを展開します。  
  
    9. **[Web 管理ツール]** の **[IIS 6 と互換性のある管理]** ノードを展開します。次に、 **[IIS 6 メタベースおよび IIS 6 構成との互換性]** チェック ボックスをオンにします。  
  
    10. **[Web 管理ツール]** の **[IIS 管理コンソール]** を選択し、 **[OK]** をクリックします。  
  
    11. コンピューターを再起動して、これらの変更を反映します。  
  
3. **[スタート]** ボタン、 **[コントロール パネル]** の順にクリックします。  
  
4. **[クラシック表示]** をクリックし、 **[管理ツール]** をダブルクリックしします。  
  
5. **[名前]** 列で **[インターネット インフォメーション サービス (IIS) マネージャー]** をダブルクリックします。  
  
6. **[接続]** 列で、ご使用のサーバーに対応するノードを展開します。  
  
     サーバー名の下に **[Web サイト]** フォルダーが表示されます。  
  
7. **[Web サイト]** ノードを展開し、統合 Windows 認証を有効にする Web サイトをクリックします。  
  
8. 中央のペインのタイトルが、選択した Web サイトの名前に変わります。 このペインで、 **[IIS]** という見出しの下の **[認証]** をダブルクリックします。  
  
     このペインのタイトルが **[認証]** に変わります。  
  
9. **[認証]** ペインの **[名前]** 列で [**Windows 認証]** を右クリックし、 **[有効化]** をクリックします。  
  
10. **[インターネット インフォメーション サービス (IIS) マネージャー]** ウィンドウを閉じます。  
  
## <a name="see-also"></a>参照  
 [Debugging Web Applications: Errors and Troubleshooting](../debugger/debugging-web-applications-errors-and-troubleshooting.md)   
 [Microsoft ダイジェスト認証](https://go.microsoft.com/fwlink/?LinkId=77938)   
 [Running Web Applications on Windows Vista with IIS 7.0 and Visual Studio](https://msdn.microsoft.com/library/262a82ac-dd0e-4096-86c6-fb463e88be66)
