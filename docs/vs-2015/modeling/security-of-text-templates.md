---
title: テキストテンプレートのセキュリティ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, security
ms.assetid: 567a2383-7d43-4acc-af4a-cd70b7a0151e
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e24a90d4e7af351fc4ba5807d2af7830edede9cb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671215"
---
# <a name="security-of-text-templates"></a>テキスト テンプレートのセキュリティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストテンプレートには、次のようなセキュリティの問題があります。

- テキストテンプレートは、任意のコードの挿入に対して脆弱です。

- ディレクティブプロセッサを検索するためにホストが使用するメカニズムがセキュリティで保護されていない場合は、悪意のあるディレクティブプロセッサを実行できます。

## <a name="arbitrary-code"></a>任意のコード
 テンプレートを記述するときに、タグ内に任意のコードを配置でき \<# #> ます。 これにより、テキストテンプレート内から任意のコードを実行できます。

 信頼されたソースからテンプレートを取得していることを確認してください。 信頼できるソースからのものではないテンプレートを実行しないように、アプリケーションのエンドユーザーに警告してください。

## <a name="malicious-directive-processor"></a>悪意のあるディレクティブプロセッサ
 テキストテンプレートエンジンは、変換ホストと1つ以上のディレクティブプロセッサと対話し、テンプレートテキストを出力ファイルに変換します。 詳細については、「 [テキストテンプレート変換プロセス](../modeling/the-text-template-transformation-process.md)」を参照してください。

 ディレクティブプロセッサを見つけるためにホストが使用するメカニズムが安全でない場合は、悪意のあるディレクティブプロセッサを実行するリスクがあります。 悪意のあるディレクティブプロセッサは、テンプレートの実行時にモードで実行されるコードを提供でき `FullTrust` ます。 カスタムテキストテンプレート変換ホストを作成する場合は、エンジンがディレクティブプロセッサを見つけるために、レジストリなどの安全な機構を使用する必要があります。
