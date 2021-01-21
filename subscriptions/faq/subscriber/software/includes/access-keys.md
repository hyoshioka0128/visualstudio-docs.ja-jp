---
title: サブスクリプションの有効期限が切れたときにプロダクト キーにアクセスするには、どうすればよいですか?
description: サブスクリプションの有効期限が切れた後にプロダクト キーにアクセスできるようにするには、サブスクリプションの有効期限が切れる前に、要求...
ms.topic: include
ms.assetid: 73342d98-bedb-4c3b-8961-5ee2210b7029
author: CaityBuschlen
ms.author: cabuschl
ms.date: 4/3/2020
ms.faqid: q2_3
ms.openlocfilehash: 32c295a236b3221636b241c1fa806bbdd93d3c15
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "81385911"
---
## <a name="how-do-i-access-my-product-keys-when-my-subscription-expires"></a>サブスクリプションの有効期限が切れたときにプロダクト キーにアクセスするには、どうすればよいですか?

サブスクリプションの有効期限が切れた後にプロダクト キーにアクセスできるようにするには、サブスクリプションの有効期限が切れる前に、要求されたキーをエクスポートする必要があります。 有効期限が切れると、キーを取得できなくなります。

キーをエクスポートするには、[プロダクト キー] ページの右端にある [[すべてのキーをエクスポート]](https://my.visualstudio.com/ProductKeys) リンクをクリックします。 KeysExport.xml という名前の .xml ファイルが作成され、ファイルを開くか保存するオプションが表示されます。 .Xml ファイルを処理できるアプリケーションでファイルを開く必要があります。 たとえば、Excel で読み取り専用のブックとしてファイルを開くことができます。 このファイルには、要求したすべてのキーに加えて、自動的に要求されたすべての\'静的\'キーが含まれています。
