---
title: '方法: 生成されたコードのコード分析の警告を非表示にする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 3a96434e-d419-43a7-81ba-95cccac835b8
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 52caadd7f4dd9349eccb80a366a1458212aba5ca
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72646272"
---
# <a name="how-to-suppress-code-analysis-warnings-for-generated-code"></a>方法: 生成されたコードに対するコード分析の警告を抑制する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

マネージコードコンパイラは、多くの場合、迅速なコード開発を容易にするためにプロジェクトに追加されたコードを生成します。 また、多くの場合、開発者はサードパーティ製のツールを使用して、アプリケーションの開発を迅速に支援します。 これらのツールでは、プロジェクトに追加されるコードも生成されます。

 生成されたコードでコード分析によって検出された規則違反を確認することができます。 ただし、違反が含まれているコードを表示および管理できない場合は、表示したくない場合があります。

 プロジェクトの [コード分析] プロパティページの [ **生成されたコードの結果を** 表示しない] チェックボックスを使用すると、サードパーティのツールで生成されたコードからコード分析の警告を表示するかどうかを選択できます。

> [!NOTE]
> このオプションでは、フォームおよびテンプレートにエラーと警告が表示された場合に、生成されたコードからのコード分析エラーおよび警告は抑制されません。 フォームまたはテンプレートのソース コードは表示することも保持することもできます。

### <a name="to-suppress-warnings-for-generated-code-in-a-project"></a>プロジェクトで生成されたコードの警告を抑制するには

1. ソリューションエクスプローラーでプロジェクトを右クリックし、[ **プロパティ**] をクリックします。

2. **[コード分析]** をクリックします。

3. [ **生成されたコードから結果** を表示しない] チェックボックスをオンにします。
