---
title: VS シェルのデプロイ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: be8f2ffe-a322-4ac0-9c9e-873bd28e5d5e
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a42ec6a762655589bfd589ae9dc0354e3a7d1cb5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659304"
---
# <a name="vs-shell-deployment"></a>VS Shell 配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

分離シェルを使用すると、ドメイン固有言語と対話するために必要な Visual Studio の機能と、そのソリューションをどのように表示するかを決定できます。 Visual Studio の分離シェルの詳細については、「 [分離シェルのカスタマイズ](../extensibility/customizing-the-isolated-shell.md)」を参照してください。 分離シェルをカスタマイズする方法の詳細については、「 [分離シェルのカスタマイズ](https://msdn.microsoft.com/d75463cd-1155-42e4-8b7a-046ed6becbbf)」を参照してください。

### <a name="to-set-a-visual-studio-shell-as-the-deployment-target"></a>Visual Studio シェルを配置ターゲットとして設定するには

1. **Dslpackage**プロジェクトで、 **source.extension.tt**を開きます。

2. [挿入] の下 `<SupportedProducts>` :

    ```
    <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
    ```

     *MyIsolatedShell*を分離シェルパッケージの名前に置き換えます。
