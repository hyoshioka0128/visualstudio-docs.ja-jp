---
title: '方法: ClickOnce 配置エラー用にカスタムログファイルの場所を設定するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- ClickOnce deployment, error logging
ms.assetid: 77424414-7f0e-4b99-94bb-ea130de92d09
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7a1b7c93e4b30bbfd373a5fad9d7001452d4f587
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841597"
---
# <a name="how-to-set-a-custom-log-file-location-for-clickonce-deployment-errors"></a>方法 : ClickOnce 配置エラー用にカスタム ログ ファイルの場所を設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] すべての配置のアクティブ化ログファイルを保持します。 これらのログには、展開のインストールと初期化に関連するエラーが記録さ [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] れます。 既定では、は、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] デプロイのアクティブ化ごとに1つのログファイルを作成します。 これらのログファイルは、Temporary Internet Files フォルダーに格納されます。 アクティブ化エラーが発生すると、展開のログファイルがユーザーに表示され、ユーザーは結果のエラーダイアログボックスで [ **詳細** ] をクリックします。  
  
 レジストリエディター (**regedit.exe**) を使用してカスタムログファイルのパスを設定することにより、特定のクライアントのこの動作を変更できます。 この場合、は、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 1 つのファイル内のすべての配置について、アクティブ化の成功と失敗をログに記録します。  
  
> [!CAUTION]
> レジストリ エディタの使用を誤ると、オペレーティング システムの再インストールが必要になるような深刻な問題を引き起こす可能性があります。 問題が発生する可能性のあることを十分に認識したうえで利用してください。  
  
> [!NOTE]
> ログファイルが大きくなりすぎないようにするには、ログファイルをときどき切り捨てるか削除する必要があります。  
  
 次の手順では、1つのクライアントに対してカスタムログファイルの場所を設定する方法について説明します。  
  
### <a name="to-set-a-custom-log-file-location"></a>カスタムログファイルの場所を設定するには  
  
1. **Regedit.exe**を開きます。  
  
2. ノードに移動 `HKCU\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment` します。  
  
3. 文字列値を、 `LogFilePath` 任意のカスタムログの場所の完全なパスとファイル名に設定します。  
  
     この場所は、ユーザーが書き込みアクセス権を持っているディレクトリに存在する必要があります。 たとえば、Windows Vista では、次のフォルダー構造を作成し、 `LogFilePath` C:\Users \\<username \Documents\Logs\ClickOnce\installation.log. に設定します。 \>  
  
## <a name="see-also"></a>参照  
 [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)
