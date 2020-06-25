---
title: マネージコードに対してレガシコード分析を手動で実行する方法
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 38c3de83dc0df39314ad236f647c69bbe614b75d
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371821"
---
# <a name="how-to-run-legacy-code-analysis-manually-for-managed-code"></a>方法: マネージコードに対してレガシコード分析を手動で実行する
コード分析ツールは、ソースコードで発生する可能性のある欠陥に関する情報を提供します。 コードプロジェクトの各ビルドでコード分析を自動的に実行できます。また、コード分析を手動で実行することもできます。 コード分析の実行時にチェックされる規則は、プロジェクトのプロパティページの [コード分析] ページで指定します。 詳細については、「[方法: マネージコードプロジェクトのコード分析を構成する](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)」を参照してください。

## <a name="to-run-code-analysis-manually"></a>コード分析を手動で実行するには

1. Visual Studio 2019 バージョン16.5 以降を使用している場合は、Visual Studio を起動する前に、コマンドプロンプトで次のコマンドを実行します。

```
set EnableLegacyCodeAnalysis = true
```

2. **ソリューションエクスプローラー**で、プロジェクトをクリックします。

3. [**分析**] メニューの [*プロジェクト名***に対してコード分析を実行**] をクリックします。

