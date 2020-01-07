---
title: 生成されたコードのコード分析違反を抑制する
ms.date: 05/13/2019
ms.topic: conceptual
ms.assetid: 3a96434e-d419-43a7-81ba-95cccac835b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9ab2ffce28103059414cef8f1b556152485a12ff
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587434"
---
# <a name="how-to-suppress-code-analysis-warnings-for-generated-code"></a>方法: 生成されたコードのコード分析の警告を非表示にする

生成されたコードには、マネージコードコンパイラまたはサードパーティ製のツールによってプロジェクトに追加されたコードが含まれます。 生成されたコードでコード分析によって検出された規則違反を確認することができます。 ただし、違反が含まれているコードを表示および管理することはできないため、表示されない場合があります。

プロジェクトの [コード分析] プロパティページの [**生成されたコードの結果を**表示しない] チェックボックスを使用すると、サードパーティのツールで生成されたコードからコード分析の警告を表示するかどうかを選択できます。

> [!NOTE]
> コード分析のエラーおよび警告がフォームやテンプレートで表示される場合、このオプションを使用しても、生成されたコードからこのエラーおよび警告の出力は抑制されません。 フォームまたはテンプレートのソース コードは表示することも保持することもできます。

### <a name="to-suppress-warnings-for-generated-code-in-a-project"></a>プロジェクトで生成されたコードの警告を抑制するには

1. **ソリューションエクスプローラー**でプロジェクトを右クリックし、 **[プロパティ]** をクリックします。

2. **[コード分析]** タブをクリックします。

3. [**生成されたコードから結果**を表示しない] チェックボックスをオンにします。

> [!IMPORTANT]
> レガシ分析からの警告のみを非表示にすることができます。 この設定のプロパティページは非推奨とされており、今後の製品リリースでは削除される予定です。 現時点では、[アナライザー](roslyn-analyzers-overview.md)からのコード分析の警告を抑制することはできません。
