---
title: エラー :プロセスの ID を検査する権限がありません | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 6233d060-85b8-42be-ae5f-bde7e1d0f241
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d66eacb1b7f5205ea430d7154f67d05bdd047a74
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157517"
---
# <a name="error-you-do-not-have-permission-to-inspect-the-process39s-identity"></a>エラー :プロセスの ID を検査する権限がありません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロセスの ID を検査する権限がありません。 これは、システムの混が原因である可鉢があります。  
  
 デバッグに必要なプロセス ID をデバッガーが検査できませんでした。 最も可能性の高い原因として、ターミナル サービスが無効になっていることが挙げられます。 既定では、ターミナル サービスが有効に設定されています。 再度有効にするには、次の手順に従います。  
  
### <a name="to-enable-terminal-services"></a>ターミナル サービスを有効にするには  
  
1. **[スタート]** ボタンをクリックして、 **[コントロール パネル]** をクリックします。  
  
2. コントロール パネルで必要に応じて **[クラシック表示に切り替える]** を選択し、 **[管理ツール]** をダブルクリックします。  
  
3. **[管理ツール]** ウィンドウで、 **[コンピューターの管理]** をダブルクリックします。  
  
4. [コンピューターの管理] ウィンドウで、 **[サービスとアプリケーション]** ノードを展開します。  
  
5. **[サービスとアプリケーション]** の **[サービス]** をクリックします。  
  
     右側のパネルにサービスの一覧が表示されます。  
  
6. **[サービス]** 一覧の **[Terminal Services]** を右クリックして、 **[プロパティ]** をクリックします。  
  
7. **[ターミナル サービスのプロパティ]** ウィンドウの **[全般]** タブで、 **[スタートアップの種類]** を **[手動]** に設定します。  
  
8. **[OK]** をクリックします。  
  
9. コンピューターを再起動します。  
  
     この手順では、リモート デスクトップを自動的に有効にすることはできません。 コンピューターのリモート デスクトップを有効にするには、別途、次の手順を実行する必要があります。  
  
### <a name="to-enable-remote-desktop"></a>リモート デスクトップを有効にするには  
  
1. **[スタート]** ボタンをクリックして、 **[マイ コンピューター]** を右クリックします。  
  
2. **[プロパティ]** を選択します。  
  
     **[システムのプロパティ]** ウィンドウが表示されます。  
  
3. **[リモート]** をクリックします。  
  
4. **[リモート デスクトップ]** の **[このコンピューターにユーザーがリモートで接続することを許可する]** をオンにします。  
  
5. **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)
