---
title: '方法: コード分析のチェックインポリシーを使用して保守が容易なコードを適用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis, check-in policies
ms.assetid: d1b3b04f-4dd9-40e6-b2d4-b414d33fb647
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0d54ca9a31e8a1bbd2496bf8689a119e53580c79
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72660217"
---
# <a name="how-to-enforce-maintainable-code-with-a-code-analysis-check-in-policy"></a>方法: コード分析のチェックイン ポリシーを使用して保守が容易なコードを適用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

開発者は、コードメトリックスツールを使用して、コードの複雑さと保守性を測定できますが、チェックインポリシーの一部としてコードメトリックスを呼び出すことはできません。 ただし、コードメトリックス標準でコードの準拠を確認し、チェックインポリシーを使用してルールを適用するコード分析ルールをチームで有効にすることができます。 コードメトリックスの詳細については、「 [コードメトリックスの値](../code-quality/code-metrics-values.md)」を参照してください。

 開発者は、コード分析チェックインポリシーを使用して保守性のあるコードを適用するために、継承の深さ、クラスの結合、保守容易性のインデックス、および複雑さの規則を有効にすることができます。 これらの4つのルールはすべて、コード分析ポリシーエディターの [保守容易性ルール] カテゴリにあります。

 のバージョン管理の管理者 [!INCLUDE[esprfound](../includes/esprfound-md.md)] は、コード分析の保守容易性の規則をチェックインポリシーの要件に追加できます。 これらのチェックインポリシーでは、開発者は、チェックインを開始する前に、これらの規則の変更に基づいてコード分析を実行する必要があります。

### <a name="to-open-the-code-analysis-policy-editor"></a>コード分析ポリシーエディターを開くには

1. **チームエクスプローラー**で、チームプロジェクトを右クリックし、[**チームプロジェクトの設定**] をクリックして、[**ソース管理**] をクリックします。

     [ **ソース管理** ] ダイアログボックスが表示されます。

2. [ **チェックインポリシー** ] タブで、[ **追加**] をクリックします。

     [ **チェックインポリシーの追加** ] ダイアログボックスが表示されます。

3. [ **チェックインポリシー** ] の一覧で [ **コード分析** ] チェックボックスをオンにし、[ **OK]** をクリックします。

     [ **コード分析ポリシーエディター** ] ダイアログボックスが表示されます。

### <a name="to-enable-code-analysis-maintainability-rules"></a>コード分析の保守容易性の規則を有効にするには

1. [ **コード分析ポリシーエディター** ] ダイアログボックスの [ **ルールの設定**] で、[ **メンテナンスルール** ] ノードを展開します。

2. 次の規則のチェックボックスをオンにします。

    - 継承の深さ: **CA1501 AvoidExcessiveInheritance** -Threshold: Warning が5レベルを超える場合

    - 複雑さ: **CA1502 AvoidExcessiveComplexity** -しきい値:25 を超える警告

    - 保守容易性のインデックス: **CA1505 AvoidUnmaintainableCode** -Threshold: Warning が20未満

    - クラスの結合: **CA1506 AvoidExcessiveClassCoupling** -Threshold: クラスの場合は80以上、メソッドの場合は30を超える警告

    - また、規則違反でビルドを防止するには、規則の説明の横にある [ **警告をエラーとして扱う** ] チェックボックスをオンにします。

3. **[OK]** をクリックします。 新しいチェックインポリシーは、今後のチェックインに適用されるようになりました。

## <a name="see-also"></a>参照
 コード[メトリックスの値](../code-quality/code-metrics-values.md)コード[分析のチェックインポリシーの作成と使用](../code-quality/creating-and-using-code-analysis-check-in-policies.md)
