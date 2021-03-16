---
description: スクリプトは、現在のページのホスト以外のソースから、データにアクセスしようとしました。
title: アクセスが拒否されました |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 8a512060-d744-47af-a83e-4ba42ea2c5b2
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 6be3bce0643a5892973235871191766cac140962
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571936"
---
# <a name="access-is-denied"></a>アクセスが拒否されました
スクリプトは、現在のページのホスト以外のソースから、データにアクセスしようとしました。 Internet Explorer や他のブラウザーが従う同一生成元ポリシーは、現在のページの URL と同じスキーム、ホスト、およびポートのソースからのみ、スクリプトがデータにアクセスすることを許可しています。  
  
 たとえば、現在のページがの場合、 `https://employees.mycompany.com` 次の url からデータにアクセスすることはできません。  
  
- `http://data.contoso.com`HTTPS ではなく HTTP が使用されているためです。  
  
- `https://somedatasource.com`。これは別のドメインであるためです。  
  
- `https://employees.mycompany.com:8888`。別のポートを使用しているためです。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 呼び出そうとしている API が、クロス オリジンのスクリプトを安全に許可する 2 つの手段である、JSONP または CORS をサポートしているかどうかを調査します。  
  
- REST API を呼び出そうとしている場合は、サーバー側コードにこの呼び出しをリファクタリングして、クライアント側スクリプトの新しい REST エンドポイントを公開します。  
  
     詳しくは、同一生成元ポリシー、JSONP、および CORS に関連したオンライン ドキュメントを参照してください。
