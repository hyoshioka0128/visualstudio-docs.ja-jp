---
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
ms.openlocfilehash: 874f7c0e5dcfaf4881c059a77f1c5e930d8c0578
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814838"
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
