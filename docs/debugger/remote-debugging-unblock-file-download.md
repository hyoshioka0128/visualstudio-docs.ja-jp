---
title: リモート ツールのダウンロードのブロックを解除する
ms.date: 07/19/2018
ms.topic: troubleshooting
helpviewer_keywords:
- remote debugging, unblock download
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8a243033bf5831952d83fdf688302651e02b76b7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62903026"
---
# <a name="how-to-unblock-the-download-of-the-remote-tools-on-windows-server"></a>方法: Windows Server でリモート ツールのダウンロードのブロックを解除する

Windows Server の Internet Explorer の既定のセキュリティ設定では、リモート ツールなどのコンポーネントのダウンロードに時間がかかることがあります。

* [セキュリティ強化の構成] が Internet Explorer で有効になっています。これにより、リソースが含まれるドメインが明示的に許可されている (つまり、信頼されている) 場合を除き、Web サイトを開いたり、Web リソースにアクセスしたりすることができません。 この設定は無効にすることができますが、セキュリティ上のリスクが生じる可能性があるため、お勧めしません。

* また、Windows Server 2016 では、 **[インターネット オプション]**  >  **[セキュリティ]**  >  **[インターネット]**  >  **[レベルのカスタマイズ]**  >  **[ダウンロード]** の既定の設定により、ファイルのダウンロードが無効にされます。 リモート ツールを Windows Server に直接ダウンロードする場合は、ファイルのダウンロードを有効にする必要があります。

Windows Server でツールをダウンロードするには、次のいずれかをお勧めします。

* Visual Studio を実行しているコンピューターなど、別のコンピューターでリモート ツールをダウンロードし、 *.exe* ファイルを Windows Server にコピーします。

* Visual Studio コンピューターで[ファイル共有から](../debugger/remote-debugging.md#fileshare_msvsmon)リモート デバッガーを実行します。

* リモート ツールを Windows Server に直接ダウンロードし、プロンプトに従って、信頼済みサイトを追加します。 多くの場合、最新の Web サイトには多数のサード パーティのリソースが含まれているため、数多くのプロンプトが表示される可能性があります。 さらに、リダイレクトされたリンクがあれば、手動で追加する必要があります。 ダウンロードを開始する前に、信頼済みサイトの一部を追加することを選択できます。 **[インターネット オプション] > [セキュリティ] > [信頼済みサイト] > [サイト]** にアクセスして、次のサイトを追加します。

  * visualstudio.microsoft.com
  * download.visualstudio.microsoft.com
  * about:blank

  my.visualstudio.com 上のデバッガーのバージョンが古い場合は、次のサイトを追加して、ログインが成功することを確認します。

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

    ソフトウェアをダウンロードすると、さまざまな Web サイトのスクリプトとリソースを読み込むためのアクセス許可を付与するための追加の要求を受け取ります。 my.visualstudio.com で、ドメインを追加して、ログインが成功することを確認することお勧めします。