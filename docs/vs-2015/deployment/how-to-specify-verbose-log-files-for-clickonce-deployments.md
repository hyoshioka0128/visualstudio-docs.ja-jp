---
title: '方法: ClickOnce 配置の詳細ログファイルを指定するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- logs, ClickOnce deployment
- ClickOnce deployment, logging
ms.assetid: 0807a28d-2e40-4a51-ab10-308d808ded6b
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 78fa278952004348e035a675a1e159b2164285b1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842239"
---
# <a name="how-to-specify-verbose-log-files-for-clickonce-deployments"></a>方法: ClickOnce 配置用の詳細ログ ファイルを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] すべての展開のアクティビティログファイルを保持します。 これらのログには、展開のインストール、初期化、更新、およびアンインストールに関する詳細が記録さ [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] れます。 これらのログファイルへの書き込みの詳細を増やすには [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 、レジストリエディター (**regedit.exe**) を使用して詳細レベルを指定します。  
  
> [!CAUTION]
> レジストリエディターを誤って使用すると、重大な問題が発生し、オペレーティングシステムの再インストールが必要になることがあります。 問題が発生する可能性のあることを十分に認識したうえで利用してください。  
  
 次の手順では、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 現在のユーザーのログファイルの詳細レベルを指定する方法について説明します。 詳細レベルを下げるには、このレジストリ値を削除します。  
  
### <a name="to-specify-verbose-log-files"></a>詳細ログファイルを指定するには  
  
1. **Regedit.exe**を開きます。  
  
2. ノードに移動 `HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment` します。  
  
3. 必要に応じて、という名前の新しい文字列値を作成 `LogVerbosityLevel` します。  
  
4. `LogVerbosityLevel`値をに設定 `1` します。  
  
## <a name="see-also"></a>参照  
 [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)
