---
title: リモート ツールのダウンロードのブロックを解除する
description: Windows Server でリモート ツールをダウンロードすると IE の既定のセキュリティ設定に起因して時間がかかることがありますが、そのブロックを解除します。
ms.custom: SEO-VS-2020
ms.date: 07/19/2018
ms.topic: troubleshooting
helpviewer_keywords:
- remote debugging, unblock download
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ffefa70c59658382073a10db8ae1832b0d9b03c7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934560"
---
# <a name="how-to-unblock-the-download-of-the-remote-tools-on-windows-server"></a>方法: Windows Server でリモート ツールのダウンロードのブロックを解除する

Windows Server の Internet Explorer の既定のセキュリティ設定では、リモート ツールなどのコンポーネントのダウンロードに時間がかかることがあります。

* [セキュリティ強化の構成] が Internet Explorer で有効になっています。これにより、リソースが含まれるドメインが明示的に許可されている (つまり、信頼されている) 場合を除き、Web サイトを開いたり、Web リソースにアクセスしたりすることができません。 この設定は無効にすることができますが、セキュリティ上のリスクが生じるおそれがあるため、お勧めしません。

* また、Windows Server 2016 では、 **[インターネット オプション]**  >  **[セキュリティ]**  >  **[インターネット]**  >  **[レベルのカスタマイズ]**  >  **[ダウンロード]** の既定の設定により、ファイルのダウンロードが無効にされます。 リモート ツールを Windows Server に直接ダウンロードする場合は、ファイルのダウンロードを有効にする必要があります。

Windows Server でツールをダウンロードするには、次のいずれかの操作をお勧めします。

* Visual Studio を実行しているコンピューターなど、別のコンピューターでリモート ツールをダウンロードし、 *.exe* ファイルを Windows Server にコピーします。

* Visual Studio コンピューターで[ファイル共有から](../debugger/remote-debugging.md#fileshare_msvsmon)リモート デバッガーを実行します。

* リモート ツールを Windows Server に直接ダウンロードし、プロンプトに従って、信頼済みサイトを追加します。 多くの場合、最新の Web サイトには多数のサード パーティのリソースが含まれているため、たくさんのプロンプトが表示される可能性があります。 また、リダイレクトされたリンクがあれば、手動で追加する必要があります。 ダウンロードを開始する前に、信頼済みサイトの一部を追加することを選択できます。 **[インターネット オプション] > [セキュリティ] > [信頼済みサイト] > [サイト]** にアクセスして、次のサイトを追加します。

  * visualstudio.microsoft.com
  * download.visualstudio.microsoft.com
  * about:blank

  my.visualstudio.com 上のデバッガーのバージョンが古い場合は、次の他のサイトを追加して、ログインが成功することを確認します。

  * microsoft.com
  * go.microsoft.com
  * download.microsoft.com
  * my.visualstudio.com
  * login.microsoftonline.com
  * login.live.com
  * secure.aadcdn.microsoftonline-p.com
  * msft.sts.microsoft.com
  * auth.gfx.ms
  * app.vssps.visualstudio.com
  * vlscppe.microsoft.com
  * query.prod.cms.rt.microsoft.com

    リモート ツールのダウンロード中にこれらのドメインの追加を選択する場合は、プロンプトが表示されたら、 **[追加]** を選択します。

    ![ブロックされたコンテンツのダイアログ ボックス](../debugger/media/remotedbg-blocked-content.png)

    ソフトウェアをダウンロードすると、さまざまな Web サイトのスクリプトとリソースを読み込むためのアクセス許可を付与する要求がたくさん届きます。 my.visualstudio.com で、ドメインを追加して、ログインが成功することを確認することお勧めします。