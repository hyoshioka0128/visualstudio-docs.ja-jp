---
title: VS Shell 配置
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d8793312e0ed022fc7210508efdf20a81b293f0f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85535851"
---
# <a name="vs-shell-deployment"></a>VS Shell 配置

分離シェルを使用すると、ドメイン固有言語と対話するために必要な Visual Studio の機能と、そのソリューションをどのように表示するかを決定できます。 Visual Studio の分離シェルの詳細については、「 [分離シェルのカスタマイズ](https://docs.microsoft.com/visualstudio/extensibility/customizing-the-isolated-shell)」を参照してください。

Visual Studio シェルを配置ターゲットとして設定するには、次のようにします。

1. **Dslpackage**プロジェクトで、 **source.extension.tt**を開きます。

2. [挿入] の下 `<SupportedProducts>` :

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   *MyIsolatedShell*を分離シェルパッケージの名前に置き換えます。
