---
title: '方法: C/C + + プロジェクトのコード分析プロパティを設定するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.native
- VC.Project.VCCLCompilerTool.EnablePrefast
- VC.Project.VCFxCopTool.EnablePREfast
- VC.Project.VCFxCopTool.IgnoreGeneratedCode
helpviewer_keywords:
- properties, C/C++ Code Analysis
- properties, Code Analysis
- code analysis properties
- C/C++ code analysis properties
ms.assetid: 7af52097-6d44-4785-9b9f-43b7a7d447d7
caps.latest.revision: 19
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: b2fb3cb81b49fd4b8cc83e0548110d2025c7488d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77277985"
---
# <a name="how-to-set-code-analysis-properties-for-cc-projects"></a>方法: C/C++ プロジェクトのコード分析プロパティを設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード分析ツールがプロジェクトの各構成でコードを分析するために使用する規則を構成できます。 さらに、サードパーティのツールによって生成され、プロジェクトに追加されたコードからの警告を表示しないようにコード分析を指示することもできます。  
  
## <a name="code-analysis-property-page"></a>[コード分析] プロパティページ  
 [ **コード分析** ] プロパティページには、プロジェクトのすべてのコード分析の構成設定が含まれています。 **ソリューションエクスプローラー**のプロジェクトの [コード分析] プロパティページを開くには、プロジェクトを右クリックし、[**プロパティ**] をクリックします。 次に、[ **構成プロパティ** ] を展開し、[ **コード分析** ] タブを選択します。  
  
## <a name="project-configuration-and-platform"></a>プロジェクト構成とプラットフォーム  
 [ **構成** リスト] と [ **プラットフォーム** ] ボックスの一覧では、さまざまなコード分析設定をプロジェクトの構成とプラットフォームの組み合わせごとに適用できます。 たとえば、デバッグビルドのプロジェクトに1つのルールセットを適用し、リリースビルド用に別のセットを適用するようにコード分析を指示することができます。  
  
## <a name="enabling-code-analysis"></a>コード分析の有効化  
 **[ビルド時に C/c + + のコード分析を有効**にする] を選択すると、プロジェクトのコード分析を有効にするかどうかを決定できます。 たとえば、 **構成** リストと組み合わせて、デバッグビルドのコード分析を無効にし、リリースビルドに対して有効にすることができます。  
  
 プロジェクトにマネージコードが含まれている場合は、[ **ビルドでコード分析を有効**にする] を選択して、コード分析を有効または無効にするかどうかを決定できます。  
  
 コード分析は、コードの品質を向上させ、一般的な落とし穴を回避できるように設計されています。 そのため、コード分析を無効にするかどうかを慎重に検討してください。 通常は、プロジェクトに適用しないルールセットまたは個々のルールを無効にすることをお勧めします。  
  
## <a name="generated-code"></a>生成されたコード  
 開発者は、アプリケーションの迅速な開発に役立つツールを頻繁に使用します。 これらのツールは、プロジェクトに追加されたコードを生成できます。 生成されたコードでコード分析によって検出された規則違反を確認することができます。 ただし、コードを管理したくない場合は、表示したくない場合があります。  
  
 **[全般**プロパティ] ページの [**生成されたコードの結果を**表示しない] チェックボックスをオンにすると、サードパーティツールによって生成されたマネージコードからコード分析の警告を表示するかどうかを選択できます。  
  
## <a name="rule-sets"></a>規則セット  
 プロジェクトにマネージコードが含まれている場合は、[ **この規則セットを実行** する] の一覧から規則セットを選択して、コード分析で適用する規則を選択できます。  
  
## <a name="see-also"></a>参照  
 [マネージコードの品質の分析](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)   
 [C/c + + のコード分析の警告](../code-quality/code-analysis-for-c-cpp-warnings.md)
