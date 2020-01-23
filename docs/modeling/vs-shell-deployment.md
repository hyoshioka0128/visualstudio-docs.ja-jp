---
title: VS Shell 配置
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99ef0124c06cd6f1a4d24e29b2c02cd0b50a37b0
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76115271"
---
# <a name="vs-shell-deployment"></a>VS Shell 配置

分離シェルを使用すると、ドメイン固有言語と対話するために必要な Visual Studio の機能と、そのソリューションをどのように表示するかを決定できます。 Visual Studio の分離シェルの詳細については、「[分離シェルのカスタマイズ](https://vspartner.com/pages/vsshells)」を参照してください。

Visual Studio シェルを配置ターゲットとして設定するには、次のようにします。

1. **Dslpackage**プロジェクトで、 **source.extension.tt**を開きます。

2. `<SupportedProducts>` 挿入:

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   *MyIsolatedShell*を分離シェルパッケージの名前に置き換えます。
