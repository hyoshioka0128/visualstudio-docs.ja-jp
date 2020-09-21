---
title: VS Shell 配置
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f3729c09198b331728e2cc67299ffc3ad6c3d26
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90809649"
---
# <a name="vs-shell-deployment"></a>VS Shell 配置

分離シェルを使用すると、ドメイン固有言語と対話するために必要な Visual Studio の機能と、そのソリューションをどのように表示するかを決定できます。 Visual Studio の分離シェルの詳細については、「 [分離シェルのカスタマイズ](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)」を参照してください。

Visual Studio シェルを配置ターゲットとして設定するには、次のようにします。

1. **Dslpackage**プロジェクトで、 **source.extension.tt**を開きます。

2. [挿入] の下 `<SupportedProducts>` :

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   *MyIsolatedShell*を分離シェルパッケージの名前に置き換えます。