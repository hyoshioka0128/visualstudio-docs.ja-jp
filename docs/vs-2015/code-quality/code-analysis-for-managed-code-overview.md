---
title: マネージド コードに対するコード分析の概要 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: overview
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
ms.assetid: 12ec0dab-46a4-43d8-984a-440730ef37a9
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 33ab4a000fac75c51c32e8a6d37de62e006160b3
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "72610070"
---
# <a name="code-analysis-for-managed-code-overview"></a>マネージド コードに対するコード分析の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

マネージド コードのコード分析を使用すると、マネージド アセンブリを分析し、Microsoft .NET Framework デザイン ガイドラインに規定されたプログラミングやデザインに関する規則違反など、アセンブリに関する情報をレポートとして得ることができます。

 分析ツールは、分析中に実行するチェック項目を警告メッセージとして表示します。 警告メッセージは、プログラミングやデザイン上の問題を識別し、可能であれば問題の解決方法を提供します。

## <a name="ide-integrated-development-environment-integration"></a>IDE (統合開発環境) の統合
 開発者は、プロジェクトに対してコード分析を自動的に実行できるだけでなく、手動で実行することもできます。

 プロジェクトをビルドするたびにコード分析を実行するには、プロジェクトのプロパティ ページで **[ビルドに対するコード分析の有効化 (定数 CODE_ANALYSIS を定義)]** をオンにします。 詳細については、[自動コード分析を有効/無効にする](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)」を参照してください。

 プロジェクトに対してコード分析を手動で実行するには、 **[分析]** メニューの **[_ProjectName_ でコード分析を実行]** をクリックします。 詳細については、[自動コード分析を有効/無効にする](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)」を参照してください。

## <a name="rule-sets"></a>規則セット
 マネージド コード用のコード分析規則は、*規則セット*にグループ化されています。 Microsoft の標準の規則セットのいずれかを使用するか、特定のニーズを満たす独自の規則セットを作成することができます。 詳細については、「[規則セットを使用したコード分析規則のグループ化](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)」を参照してください。

## <a name="in-source-suppression"></a>ソース内抑制
 警告が適用されないことを示すと役に立つことがよくあります。 これによって、開発者や、そのコードを後でレビューする担当者は、その警告が既に調査済みであり、抑制されるのかまたは無視されるのかがわかります。

 警告のソース内抑制は、カスタム属性を使用して実装します。 警告を抑制するには、次の例のように、属性 `SuppressMessage` をソース コードに追加します。

 ```csharp
 [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]
 Public class MyClass
 {
     // code
 }
 ```

 詳細については、「[SuppressMessage 属性を使用した警告の抑制](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md)」を参照してください。

## <a name="run-code-analysis-as-part-of-check-in-policy"></a>チェックイン ポリシーの一部としてのコード分析の実行
 組織的な取り決めとして、チェックインされるすべてのコードが、特定のポリシーを満たしていることが必要な場合があります。 たとえば、次のようなポリシーが考えられます。

- チェックイン対象のコードにビルド エラーが存在しないこと。

- 最近のビルドでコード分析が実行されていること。

  これは、チェックイン ポリシーを指定することにより実現できます。 詳細については、「[チーム プロジェクト チェックイン ポリシーによるコード品質の向上](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)」を参照してください。

## <a name="team-build-integration"></a>チーム ビルドの統合
 ビルド システムの統合機能を使用すると、分析ツールをビルド プロセスの一環として実行できます。 詳細については、「[アプリケーションのビルド](/azure/devops/pipelines/index)」をご覧ください。

## <a name="see-also"></a>関連項目
 [規則セットを使用したコード分析規則のグループ化](../code-quality/using-rule-sets-to-group-code-analysis-rules.md) [方法: 自動コード分析を有効/無効にする](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
