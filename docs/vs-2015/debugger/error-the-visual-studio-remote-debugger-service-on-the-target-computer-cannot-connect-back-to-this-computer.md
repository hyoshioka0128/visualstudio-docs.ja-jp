---
title: 'エラー: 対象のコンピューターの Visual Studio リモートデバッガーサービスは、このコンピューターに接続できません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.service_access_denied_oncallback
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 89ecf99d-66bf-4da0-a840-aa95b0be1702
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 80a7de83f118b38d9a3c71f1c7e7febf48e0f5bc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520511"
---
# <a name="error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer"></a>エラー :ターゲット コンピューター上の Visual Studio リモート デバッガーが、このコンピューターに接続できません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このエラーは、Visual Studio リモート デバッガー サービスがデバッグを開始したコンピューターに接続するときに、このサービスを実行しているユーザー アカウントを認証できないことを示します。  
  
 コンピューターにアクセスできるアカウントは、次の表のとおりです。  
  
|シナリオ|LocalSystem アカウント|ドメイン アカウント|両方のコンピューターに同じユーザー名とパスワードを持つローカル アカウント|  
|-|-|-|-|-|  
|両方のコンピューターが同じドメインにある場合|はい|はい|はい|  
|両方のコンピューターが双方向の信頼関係を持つドメインにある場合|いいえ|いいえ|はい|  
|一方または両方のコンピューターがワークグループにある場合|いいえ|いいえ|はい|  
|コンピューターが異なるドメインにある場合|いいえ|いいえ|はい|  
  
 さらに:  
  
- Visual Studio リモート デバッガー サービスを実行するアカウントは、すべてのプロセスをデバッグできるように、リモート コンピューターの管理者アカウントであることが必要です。  
  
- このアカウントには、**ローカル セキュリティ ポリシー**管理ツールを使用して、リモート コンピューターに対する `Log on as a service` 特権が与えられている必要もあります。  
  
- ローカル アカウントを使用してコンピューターにアクセスしている場合は、ローカル アカウントで Visual Studio リモート デバッガー サービスを実行する必要があります。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. リモート コンピューターに Visual Studio リモート デバッガー サービスが正しく設定されていることを確認します。 詳細については、「[デバイスにリモートツールを設定する](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)」を参照してください。  
  
2. 上の表に示した、デバッガー ホスト コンピューターにアクセスできる適切なアカウントを使用して、リモート デバッガー サービスを実行します。  
  
### <a name="to-add-log-on-as-a-service-privilege"></a>"サービスとしてログオンする" 特権を追加するには  
  
1. **[スタート]** メニューの **[コントロール パネル]** を選択します。  
  
2. 必要に応じて、[コントロール パネル] で **[クラシック表示]** を選択します。  
  
3. **[管理ツール]** をダブルクリックします。  
  
4. [管理ツール] ウィンドウで、 **[ローカル セキュリティ ポリシー]** をダブルクリックします。  
  
5. **[ローカル セキュリティ設定]** ウィンドウで、 **[ローカル ポリシー]** フォルダーを展開します。  
  
6. **[ユーザー権利の割り当て]** をクリックします。  
  
7. **[ポリシー]** 列の **[サービスとしてログオン]** をダブルクリックすると、現在のローカル グループ ポリシーの割り当てが **[サービスとしてログオン]** ダイアログ ボックスに表示されます。  
  
8. 新しいユーザーを追加するには、 **[ユーザーまたはグループの追加]** をクリックします。  
  
9. ユーザーの追加作業が終了したら、 **[OK]** をクリックします。  
  
### <a name="to-work-around-this-error"></a>このエラーを回避するには  
  
- リモート デバッグ モニターをサービスとして実行する代わりに、アプリケーションとして実行します。  
  
## <a name="see-also"></a>関連項目  
 [リモートデバッグエラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Remote Debugging](../debugger/remote-debugging.md)
