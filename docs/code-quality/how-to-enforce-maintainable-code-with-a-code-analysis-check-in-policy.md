---
title: コード分析のチェックインポリシーを使用する
ms.date: 11/04/2016
description: コード分析のチェックインポリシーを使用して、コードが継承、クラス結合、保守容易性、および複雑さの標準に準拠していることを確認する方法について説明します。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code analysis, check-in policies
ms.assetid: d1b3b04f-4dd9-40e6-b2d4-b414d33fb647
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6fa97f52f67e08b2ccf0843e5b5400680ed1c020
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94434819"
---
# <a name="how-to-enforce-maintainable-code-with-a-code-analysis-check-in-policy"></a>方法: コード分析チェックインポリシーを使用して保守が容易なコードを適用する

開発者はコードメトリックスツールを使用して、コードの複雑さと保守性を測定できますが、コードメトリックスをチェックインポリシーの一部として呼び出すことはできません。 ただし、コードメトリックス標準でコードの準拠を確認し、チェックインポリシーを使用して規則を適用するコード分析規則を有効にすることができます。 コードメトリックスの詳細については、「 [コードメトリックスの値](../code-quality/code-metrics-values.md)」を参照してください。

継承の深さ、クラスの結合、保守容易性のインデックス、および複雑さの規則を有効にすることで、コード分析のチェックインポリシーを使用して保守性のあるコードを適用できます。 これらの4つのルールはすべて、コード分析ポリシーエディターの [保守容易性ルール] カテゴリにあります。

Team Foundation のバージョン管理の管理者は、コード分析の保守容易性の規則をチェックインポリシーの要件に追加できます。 これらのチェックインポリシーでは、開発者は、チェックインを開始する前に、これらの規則の変更に基づいてコード分析を実行する必要があります。

## <a name="to-open-the-code-analysis-policy-editor"></a>コード分析ポリシーエディターを開くには

1. **チームエクスプローラー** で、プロジェクトを右クリックし、[ **プロジェクトの設定** ] をクリックして、[ **ソース管理** ] をクリックします。

     [ **ソース管理** ] ダイアログボックスが表示されます。

2. [ **チェックインポリシー** ] タブで、[ **追加** ] をクリックします。

     [ **チェックインポリシーの追加** ] ダイアログボックスが表示されます。

3. [ **チェックインポリシー** ] の一覧で [ **コード分析** ] チェックボックスをオンにし、[ **OK]** をクリックします。

     [ **コード分析ポリシーエディター** ] ダイアログボックスが表示されます。

## <a name="to-enable-code-analysis-maintainability-rules"></a>コード分析の保守容易性の規則を有効にするには

1. [ **コード分析ポリシーエディター** ] ダイアログボックスの [ **ルールの設定** ] で、[ **メンテナンスルール** ] ノードを展開します。

2. 次の規則のチェックボックスをオンにします。

   - 継承の深さ: **CA1501 AvoidExcessiveInheritance** -Threshold: Warning が5レベルを超える場合

   - 複雑さ: **CA1502 AvoidExcessiveComplexity** -しきい値:25 を超える警告

   - 保守容易性のインデックス: **CA1505 AvoidUnmaintainableCode** -Threshold: Warning が20未満

   - クラスの結合: **CA1506 AvoidExcessiveClassCoupling** -Threshold: クラスの場合は80以上、メソッドの場合は30を超える警告

     また、成功したビルドを防ぐために規則違反が必要な場合は、規則の説明の横にある [ **警告をエラーとして扱う** ] チェックボックスをオンにします。

3. **[OK]** をクリックします。 新しいチェックインポリシーは、今後のチェックインに適用されるようになりました。

## <a name="see-also"></a>関連項目

- [コードメトリックスの値](../code-quality/code-metrics-values.md)
- [コード分析チェックインポリシーの作成と使用](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)
