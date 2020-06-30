---
title: 'CA1500: 変数名はフィールド名 | と同じにすることはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
helpviewer_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
ms.assetid: fa0e5029-79e9-4a33-8576-787ac3c26c39
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9565bc1ae3166c0475e8af7f0fde381497309b01
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547915"
---
# <a name="ca1500-variable-names-should-not-match-field-names"></a>CA1500:変数名はフィールド名と同一にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [CA1500: 変数名はフィールド名と一致しない](/visualstudio/code-quality/ca1500-variable-names-should-not-match-field-names)」を参照してください。

|Item|値|
|-|-|
|TypeName|VariableNamesShouldNotMatchFieldNames|
|CheckId|CA1500|
|カテゴリ|Microsoft の保守容易性|
|互換性に影響する変更点|フィールドと同じ名前を持つパラメーターで発生した場合は、次のようになります。<br /><br /> -非互換性-加えられた変更に関係なく、パラメーターを宣言するフィールドとメソッドの両方がアセンブリの外部に表示されない場合。<br />-中断-フィールドの名前を変更すると、アセンブリの外部に表示される場合があります。<br />-中断-パラメーターの名前を変更すると、そのパラメーターを宣言するメソッドがアセンブリの外部に表示される可能性があります。<br /><br /> フィールドと同じ名前を持つローカル変数でが発生した場合は、次のようになります。<br /><br /> -中断されていない-行った変更に関係なく、アセンブリの外部にフィールドを表示できない場合。<br />-非互換性-ローカル変数の名前を変更し、フィールドの名前を変更しない場合。<br />-中断-フィールドの名前を変更すると、アセンブリの外部に表示される場合があります。|

## <a name="cause"></a>原因
 インスタンスメソッドは、宣言する型のインスタンスフィールドと名前が一致するパラメーターまたはローカル変数を宣言します。 規則に違反するローカル変数をキャッチするには、デバッグ情報を使用してテストされたアセンブリをビルドし、関連付けられているプログラムデータベース (.pdb) ファイルを使用できるようにする必要があります。

## <a name="rule-description"></a>ルールの説明
 インスタンスフィールドの名前がパラメーターまたはローカル変数名と一致する場合、インスタンスフィールドは、 `this` `Me` メソッド本体の内部で (in) キーワードを使用してアクセスされ [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ます。 コードを維持する場合は、この違いを忘れがちであり、パラメーター/ローカル変数がインスタンスフィールドを参照していることを前提として、エラーが発生します。 これは特に長いメソッド本体の場合に当てはまります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、パラメーター/変数またはフィールドのいずれかの名前を変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則の2つの違反を示しています。

 [!code-csharp[FxCop.Maintainability.VarMatchesField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/cs/FxCop.Maintainability.VarMatchesField.cs#1)]
 [!code-vb[FxCop.Maintainability.VarMatchesField#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/vb/FxCop.Maintainability.VarMatchesField.vb#1)]
