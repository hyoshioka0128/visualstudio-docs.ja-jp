---
title: リリース後のパッケージ ペイロードが変更されるタイミング
description: レイアウトの作成時に、リリースが既に出荷された後にパッケージ ペイロードが変更されたかどうかを判断する方法を説明します。
ms.date: 05/22/2019
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: dec1478314e752ddace8fae822747e7c8e328b70
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76114581"
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
