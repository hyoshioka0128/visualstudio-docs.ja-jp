---
title: テキスト テンプレートのセキュリティ
description: 任意のコードや悪意のあるディレクティブプロセッサなどのトピックを含む、セキュリティとテキストテンプレートについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, security
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d54421ea4df9c54fd4ec8c1804a1a292061996ab
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97363797"
---
# <a name="security-of-text-templates"></a>テキスト テンプレートのセキュリティ
テキストテンプレートには、次のようなセキュリティの問題があります。

- テキストテンプレートは、任意のコードの挿入に対して脆弱です。

- ディレクティブプロセッサを検索するためにホストが使用するメカニズムがセキュリティで保護されていない場合は、悪意のあるディレクティブプロセッサを実行できます。

## <a name="arbitrary-code"></a>任意のコード
 テンプレートを記述するときに、タグ内に任意のコードを配置でき \<# #> ます。 これにより、テキストテンプレート内から任意のコードを実行できます。

 信頼されたソースからテンプレートを取得していることを確認してください。 信頼できるソースからのものではないテンプレートを実行しないように、アプリケーションのエンドユーザーに警告してください。

## <a name="malicious-directive-processor"></a>悪意のあるディレクティブプロセッサ
 テキストテンプレートエンジンは、変換ホストと1つ以上のディレクティブプロセッサと対話し、テンプレートテキストを出力ファイルに変換します。 詳細については、「 [テキストテンプレート変換プロセス](../modeling/the-text-template-transformation-process.md)」を参照してください。

 ディレクティブプロセッサを見つけるためにホストが使用するメカニズムが安全でない場合は、悪意のあるディレクティブプロセッサを実行するリスクがあります。 悪意のあるディレクティブプロセッサは、テンプレートの実行時にモードで実行されるコードを提供でき `FullTrust` ます。 カスタムテキストテンプレート変換ホストを作成する場合は、エンジンがディレクティブプロセッサを見つけるために、レジストリなどの安全な機構を使用する必要があります。
