---
title: '方法: マネージ コードに対してレガシ コード分析を手動で実行する'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code analysis, running
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 9d2693bcff8e83839b4171bae60b138c967f10e5
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/17/2020
ms.locfileid: "79432085"
---
# <a name="how-to-run-legacy-code-analysis-manually-for-managed-code"></a>方法: マネージ コードに対してレガシ コード分析を手動で実行する
コード分析ツールは、ソース コードの可能性のある障害に関する情報を提供します。 コード分析は、コード プロジェクトのビルドごとに自動的に実行でき、コード分析を手動で実行することもできます。 コード分析の実行時にチェックされる規則は、プロジェクトのプロパティ ページの [コード分析] ページで指定します。 詳細については、「[方法 : マネージ コード プロジェクトのコード分析を構成する](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)」を参照してください。

## <a name="to-run-code-analysis-manually"></a>コード分析を手動で実行するには

1. Visual Studio 2019 バージョン 16.5 以降の場合は、Visual Studio を起動する前に、コマンド プロンプトで次のコマンドを実行します。

```
set EnableLegacyCodeAnalysis = true
```

2. **ソリューション エクスプローラー**で、プロジェクトをクリックします。

3. [**分析**] メニューの [*プロジェクト名***でコード分析を実行**] をクリックします。

