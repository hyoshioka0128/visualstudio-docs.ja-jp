---
description: 別のユーザー名を使用してリモート コンピューターに接続できるように Windows ファイル共有が構成されました。
title: Windows ファイル共有が構成されました... | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.remote_credentials_prohibited
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cc34e269d609837d9080cd1e84787fbabf45ce76
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146250"
---
# <a name="error-windows-file-sharing-has-been-configured"></a>エラー :Windows ファイル共有が構成されました...
別のユーザー名を使用してリモート コンピューターに接続できるように Windows ファイル共有が構成されました。 この設定はリモート デバッグと互換性がありません。

 現在のファイル共有の構成は、別のユーザー名を使用してリモート コンピューターに接続するようにセットアップされています。 このシナリオでは、リモート デバッグを実行できません。

 このエラーを解決するには、他のアカウント名を使用してコンピューターにログオンするか、デバッグを実行しているアカウント名を使用するようにファイル共有を変更します。

 このユーザー名を使用してリモート コンピューターに接続する場合は、まずリモート コンピューターから切断する必要があります。

### <a name="to-correct-this-error"></a>このエラーを解決するには

1. 他のアカウント名を使用してローカル コンピューター (デバッグを起動したコンピューター) にログオンします。

     または

     . リモート コンピューターから切断します。次に、自分のアカウント名を使用して他のコンピューターに接続するようにファイル共有を再構成します。

    1. **[スタート]** メニューの **[アクセサリ]** をポイントして、 **[コマンド プロンプト]** をクリックします。

    2. Windows のコマンド プロンプトで、次のように入力します。

         `net use /delete computer_name`

    3. Windows ヘルプに記載されているいずれかの方法を使用して、ファイル共有の設定を変更します。
