---
title: リリース後のパッケージ ペイロードが変更されるタイミング
description: レイアウトの作成時に、リリースが既に出荷された後にパッケージ ペイロードが変更されたかどうかを判断する方法を説明します。
ms.date: 05/22/2019
ms.topic: how-to
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: e773ddf85df1d7f71b1ed929b8f942a5f3b36421
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "107295298"
---
# <a name="package-payload-changes"></a>パッケージ ペイロードの変更

リリースが既に出荷された後に、一部のパッケージ ペイロードの変更が許可されます。 自分または誰かがレイアウトを作成するときに、レイアウトが作成されたタイミングに応じて、この動作によって、レイアウト コンテンツが異なる可能性があります。

## <a name="verify-that-a-layout-includes-package-payload-changes"></a>レイアウトにパッケージ ペイロードの変更が含まれていることを確認する

以前に作成されたレイアウトで、リリースが出荷された後に変更されたパッケージ ペイロードを取得しているかどうかを判断する方法を次に示します。

1. セットアップ ログを開きます。 ログは通常 `%TEMP%\dd_setup_[date].log` にあります。ここで `[date]` は、`yyyyMMddHHmmss` 形式でのレイアウト操作が開始されたときです。

2. 次のテキストのように構築されているログ内の行を探します。

    `Falling back to signature and signer check because hash verification returned HashMismatch for path: [path]`

3. 次に、[パス] に対してダウンロードが成功したことを示すログ内の後半の行を探します。 それらは次のテキストのように見える可能性があります。

    `Download of [url] succeeded using engine 'WebClient'`

    `END: Downloading [url] to [path]`

## <a name="see-also"></a>関連項目

* [Visual Studio のネットワーク インストールを作成する](create-a-network-installation-of-visual-studio.md)
* [Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)
