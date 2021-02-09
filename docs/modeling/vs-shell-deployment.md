---
title: VS Shell 配置
description: 分離シェルを使用して、DSL と対話するために必要な Visual Studio の機能と、そのソリューションをどのように表示するかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1293593e71aa57d8e74b9035320b3da5108aba09
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924213"
---
# <a name="vs-shell-deployment"></a>VS Shell 配置

分離シェルを使用すると、ドメイン固有言語と対話するために必要な Visual Studio の機能と、そのソリューションをどのように表示するかを決定できます。 Visual Studio の分離シェルの詳細については、「 [分離シェルのカスタマイズ](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)」を参照してください。

Visual Studio シェルを配置ターゲットとして設定するには、次のようにします。

1. **Dslpackage** プロジェクトで、 **source.extension.tt** を開きます。

2. [挿入] の下 `<SupportedProducts>` :

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   *MyIsolatedShell* を分離シェルパッケージの名前に置き換えます。