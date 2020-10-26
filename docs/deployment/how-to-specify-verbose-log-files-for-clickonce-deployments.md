---
title: '方法: ClickOnce 配置の詳細ログファイルを指定するMicrosoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- logs, ClickOnce deployment
- ClickOnce deployment, logging
ms.assetid: 0807a28d-2e40-4a51-ab10-308d808ded6b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1e1d2ca7c58d7da85ad67e56eae7713e517a1d2c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85381770"
---
# <a name="how-to-specify-verbose-log-files-for-clickonce-deployments"></a>方法: ClickOnce 配置用の詳細ログ ファイルを指定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] すべての展開のアクティビティログファイルを保持します。 これらのログには、展開のインストール、初期化、更新、およびアンインストールに関する詳細が記録さ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] れます。 これらのログファイルへの書き込みの詳細を増やすには [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、レジストリエディター (*regedit.exe*) を使用して詳細レベルを指定します。

> [!CAUTION]
> レジストリエディターを誤って使用すると、重大な問題が発生し、オペレーティングシステムの再インストールが必要になることがあります。 問題が発生する可能性のあることを十分に認識したうえで利用してください。

 次の手順では、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 現在のユーザーのログファイルの詳細レベルを指定する方法について説明します。 詳細レベルを下げるには、このレジストリ値を削除します。

### <a name="to-specify-verbose-log-files"></a>詳細ログファイルを指定するには

1. *Regedit.exe*を開きます。

2. ノード **HKEY_CURRENT_USER \software\classes\software\microsoft\windows\currentversion\deployment**に移動します。

3. 必要に応じて、という名前の新しい文字列値を作成 `LogVerbosityLevel` します。

4. `LogVerbosityLevel`値をに設定 `1` します。

## <a name="see-also"></a>関連項目
- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)