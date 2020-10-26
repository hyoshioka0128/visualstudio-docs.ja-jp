---
title: エラー :IIS 管理サービスが応答しないため、セキュリティ チェックに失敗しました | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.iis_not_responding
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: 6060e94e-71dc-49f2-bb59-2584216eadbf
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 65eb724d14123292a0694623bf46859f8a3966f9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197088"
---
# <a name="error-a-security-check-failed-because-the-iis-admin-service-did-not-respond"></a>エラー :IIS 管理サービスが応答しないため、セキュリティ チェックに失敗しました
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このエラーは、IIS Admin サービスが応答しないときに発生します。 これは通常、IIS のインストールに問題があることを意味します。 まず、 **[管理ツール]** の **[サービス]** ツールを使用して、サービスが実行中であることを確認します。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- コントロール パネルの **[プログラムの追加と削除]** を使って、IIS を再インストールします。  
  
- \- または -  
  
- コントロール パネルの [アプリケーションの追加と削除] を使って、コンピューターから IIS を削除します。 IIS を削除しても問題が解決しない場合は、レジストリをチェックして、次のキーが存在しないことを確認します。  
  
    ```  
    HKEY_CLASSES_ROOT\CLSID\{A9E69610-B80D-11D0-B9B9-00A0C922E750}  
    ```  
  
     \- または -  
  
- コントロール パネルの [管理ツール] を使って、IIS Admin サービスを無効にします。 これによって、コンピューター上の IIS は無効になります。  
  
     この 3 つの手順のいずれかを実行した後は、コンピューターを再起動します。  
  
     詳細については、IIS のドキュメントを参照してください。  
  
## <a name="see-also"></a>参照  
 [Web アプリケーションのデバッグ: エラーとトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
