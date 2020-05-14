---
title: VS Shell 配置
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3ca497244a806324d9d2315fa1b1b89404838ff3
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81445000"
---
# <a name="vs-shell-deployment"></a>VS Shell 配置

分離シェルを使用すると、ドメイン固有言語と対話する必要がある Visual Studio の機能と、そのソリューションの表示方法を決定できます。 Visual Studio の分離シェルの詳細については、「[分離シェルのカスタマイズ](https://docs.microsoft.com/visualstudio/extensibility/customizing-the-isolated-shell)」を参照してください。

Visual Studio シェルを配置ターゲットとして設定するには、次の手順を実行します。

1. **DslPackage**プロジェクトで、 **source.extension.tt**を開きます。

2. 挿入`<SupportedProducts>`時:

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   *MyIsolatedShell*を分離シェル パッケージの名前に置き換えます。
