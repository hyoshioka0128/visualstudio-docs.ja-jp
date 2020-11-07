---
title: カスタムログファイルの場所の設定 (ClickOnce 配置エラー)
description: Clickonce がすべての配置のために保持するアクティベーションログファイルについて説明します。 clickonce 配置をインストールおよび初期化するためのエラーを文書化します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- ClickOnce deployment, error logging
ms.assetid: 77424414-7f0e-4b99-94bb-ea130de92d09
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3d9c8ce481ab9ca99b7d456f53418641654369ad
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94351038"
---
# <a name="how-to-set-a-custom-log-file-location-for-clickonce-deployment-errors"></a>方法: ClickOnce 配置エラー用にカスタム ログ ファイルの場所を設定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] すべての配置のアクティブ化ログファイルを保持します。 これらのログには、展開のインストールと初期化に関連するエラーが記録さ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] れます。 既定では、は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] デプロイのアクティブ化ごとに1つのログファイルを作成します。 これらのログファイルは、Temporary Internet Files フォルダーに格納されます。 アクティブ化エラーが発生すると、展開のログファイルがユーザーに表示され、ユーザーは結果のエラーダイアログボックスで [ **詳細** ] をクリックします。

 レジストリエディター ( **regedit.exe** ) を使用してカスタムログファイルのパスを設定することにより、特定のクライアントのこの動作を変更できます。 この場合、は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 1 つのファイル内のすべての配置について、アクティブ化の成功と失敗をログに記録します。

> [!CAUTION]
> レジストリ エディタの使用を誤ると、オペレーティング システムの再インストールが必要になるような深刻な問題を引き起こす可能性があります。 問題が発生する可能性のあることを十分に認識したうえで利用してください。

> [!NOTE]
> ログファイルが大きくなりすぎないようにするには、ログファイルをときどき切り捨てるか削除する必要があります。

 次の手順では、1つのクライアントに対してカスタムログファイルの場所を設定する方法について説明します。

### <a name="to-set-a-custom-log-file-location"></a>カスタムログファイルの場所を設定するには

1. **Regedit.exe** を開きます。

2. ノードに移動 `HKCU\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment` します。

3. 文字列値を、 `LogFilePath` 任意のカスタムログの場所の完全なパスとファイル名に設定します。

     この場所は、ユーザーが書き込みアクセス権を持っているディレクトリに存在する必要があります。 たとえば、Windows Vista では、次のフォルダー構造を作成し、 `LogFilePath` を *C:\Users \\ \<username> \Documents\Logs\ClickOnce\installation.log* に設定します。

## <a name="see-also"></a>関連項目
- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)