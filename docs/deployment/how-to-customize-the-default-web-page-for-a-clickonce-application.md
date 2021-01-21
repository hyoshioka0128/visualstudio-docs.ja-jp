---
title: ClickOnce アプリケーションの既定の web ページをカスタマイズする
description: ClickOnce アプリケーションを Web に発行するときに生成される Web ページについて説明します。これには、アプリケーションの名前とその他の情報が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish.htm Web page
- ClickOnce deployment default Web page
- deploying applications [ClickOnce], publishing
- publishing, ClickOnce
ms.assetid: 418de18c-bee9-4f24-9cd9-0252d175070d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fbda4558622c2e244071a218d3d5e42196460113
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94351207"
---
# <a name="how-to-customize-the-default-web-page-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションの既定の Web ページをカスタマイズする
ClickOnce アプリケーションを Web に発行すると、Web ページが自動的に生成され、アプリケーションと共に発行されます。 既定のページには、アプリケーションの名前、アプリケーションをインストールするためのリンク、必須コンポーネントのインストール、または MSDN のヘルプへのアクセスを行うためのリンクが表示されます。

> [!NOTE]
> ページに表示される実際のリンクは、ページが表示されているコンピューターと、含める必要のある前提条件によって異なります。

 Web ページの既定の名前は *Publish.htm* ; **プロジェクトデザイナー** で名前を変更できます。 詳細については、「 [方法: ClickOnce アプリケーションの発行ページを指定](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)する」を参照してください。

 *Publish.htm* Web ページは、新しいバージョンが検出された場合にのみ公開されます。

> [!NOTE]
> **発行** 設定に加えた変更は、 *Publish.htm* ページには影響しません。ただし、最初の発行後に前提条件を追加または削除した場合、前提条件の一覧は正確ではなくなります。 変更内容を反映するには、前提条件リンクのテキストを編集する必要があります。

### <a name="to-customize-the-publish-web-page"></a>[Web の発行] ページをカスタマイズするには

1. ClickOnce アプリケーションを Web サイトに発行します。 詳細については、「 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する」を参照してください。

2. Web サーバーで、Visual Web デザイナーまたは他の HTML エディターで *Publish.htm* ファイルを開きます。

3. 必要に応じてページをカスタマイズして保存します。

4. 任意。 Visual Studio によってカスタマイズされた発行 Web ページが上書きされないようにするには、[ **発行オプション** ] ダイアログボックスで [ **発行のたびに配置 Web ページを自動的に生成** する] をオフにします。

## <a name="see-also"></a>関連項目
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールする](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションの発行ページを指定する](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)