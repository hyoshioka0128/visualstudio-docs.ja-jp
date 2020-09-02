---
title: ソース内の抑制の概要 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
ms.assetid: f1a2dc6a-a9eb-408c-9078-2571e57d207d
caps.latest.revision: 42
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 63d405b0e62735c0c1e3d7bb716ea2db29bc19fe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651575"
---
# <a name="in-source-suppression-overview"></a>ソース内抑制の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ソース内抑制とは、違反の原因となったコードセグメントに **SuppressMessage** 属性を追加することによって、マネージコードのコード分析違反を抑制または無視する機能です。 **SuppressMessage**属性は、コンパイル時に CODE_ANALYSIS コンパイルシンボルが定義されている場合にのみ、マネージコードアセンブリの IL メタデータに含まれる条件付き属性です。

 C++/CLI では、ヘッダーファイルのマクロ CA_SUPPRESS_MESSAGE または CA_GLOBAL_SUPPRESS_MESSAGE を使用して、属性を追加します。

 ソース内の抑制メタデータが誤って配布されるのを防ぐために、リリースビルドでは、ソース内の抑制を使用しないでください。 ソース内抑制の処理コストが原因で、ソース内の抑制メタデータを含めることで、アプリケーションのパフォーマンスを低下させることもできます。

> [!NOTE]
> これらの属性を自分でコードに渡す必要はありません。 詳細については、「 [方法: メニュー項目を使用](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md)して警告を非表示にする」を参照してください。 メニュー項目は、C++ コードでは使用できません。

## <a name="suppressmessage-attribute"></a>SuppressMessage 属性
 **エラー一覧**でコード分析の警告を右クリックし、[**メッセージの非**表示] をクリックすると、コード内またはプロジェクトのグローバル抑制ファイルに**SuppressMessage**属性が追加されます。

 **SuppressMessage**属性の形式は次のとおりです。

```vb
<Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]

```

 [C++]

```
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")

```

 この場合、

- [**ルールカテゴリ]** -ルールが定義されているカテゴリ。 コード分析規則のカテゴリの詳細については、「 [マネージコードの警告のコード分析](../code-quality/code-analysis-for-managed-code-warnings.md)」を参照してください。

- **ルール Id** -ルールの識別子。 サポートには、規則識別子の短い名前と長い名前の両方が含まれます。 短い名前は CAXXXX です。長い名前は CAXXXX: FriendlyTypeName です。

- **理由** -メッセージを抑制する理由を文書化するために使用されるテキストです。

- **メッセージ Id** -各メッセージの問題の一意の識別子。

- **スコープ** -警告が抑制されている対象。 ターゲットが指定されていない場合は、属性のターゲットに設定されます。 サポートされるスコープは次のとおりです。

  - モジュール

  - 名前空間

  - リソース

  - 種類

  - メンバー

- **Target** -警告が抑制されるターゲットを指定するために使用される識別子。 これには、完全修飾された項目名が含まれている必要があります。

## <a name="suppressmessage-usage"></a>SuppressMessage の使用法
 コード分析の警告は、 **SuppressMessage** 属性のインスタンスが適用されるレベルでは抑制されます。 この目的は、違反が発生したコードに対して抑制情報を密に結合することです。

 一般的な形式の抑制には、規則のカテゴリと規則の識別子が含まれます。これには、ユーザーが判読できる規則名の表現が含まれています。 たとえば、次のように入力します。

 `[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

 ソース内の抑制メタデータを最小限に抑えるためにパフォーマンス上の厳密な理由がある場合、規則名自体は除外できます。ルールカテゴリとそのルール ID が一緒に、十分に一意なルール識別子が構成されます。 たとえば、次のように入力します。

 `[SuppressMessage("Microsoft.Design", "CA1039")]`

 この形式は、保守容易性の問題のため、推奨されません。

## <a name="suppressing-multiple-violations-within-a-method-body"></a>メソッド本体内での複数の違反の抑制
 属性はメソッドにのみ適用でき、メソッド本体内に埋め込むことはできません。 ただし、この識別子をメッセージ ID として指定すると、メソッド内での違反の複数の出現を区別できます。

 [!code-cpp[InSourceSuppression#1](../snippets/cpp/VS_Snippets_CodeAnalysis/InSourceSuppression/cpp/insourcesuppression.cpp#1)]
 [!code-csharp[InSourceSuppression#1](../snippets/csharp/VS_Snippets_CodeAnalysis/InSourceSuppression/cs/InSourceSuppression.cs#1)]
 [!code-vb[InSourceSuppression#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/InSourceSuppression/vb/InSourceSuppression.vb#1)]

## <a name="generated-code"></a>生成されたコード
 マネージコードコンパイラと一部のサードパーティツールでは、コードの迅速な開発を容易にするコードが生成されます。 ソースファイルに表示されるコンパイラで生成されたコードは、通常、生成される **Codeattribute** 属性でマークされます。

 生成されたコードのコード分析の警告とエラーを非表示にするかどうかを選択できます。 このような警告やエラーを抑制する方法の詳細については、「 [方法: 生成されたコードの警告を非](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md)表示にする」を参照してください。

 アセンブリ全体または単一のパラメーターに適用されている場合、コード分析では、発生した **Codeattribute** が無視されることに注意してください。 このような状況はめったに発生しません。

## <a name="global-level-suppressions"></a>グローバルレベルの抑制
 マネージコード分析ツールは、アセンブリ、モジュール、型、メンバー、またはパラメーターレベルで適用された **SuppressMessage** 属性を調べます。 また、リソースと名前空間に対する違反も発生します。 これらの違反はグローバルレベルで適用される必要があり、スコープが設定され、対象となります。 たとえば、次のメッセージでは、名前空間違反が抑制されます。

 `[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> 名前空間スコープの警告を非表示にすると、名前空間自体に対して警告が抑制されます。 名前空間内の型に対して警告が抑制されることはありません。

 明示的なスコープを指定することで、任意の抑制を表現できます。 これらの抑制はグローバルレベルで有効である必要があります。 型を修飾することによって、メンバーレベルの抑制を指定することはできません。

 明示的に指定されたユーザーソースにマップされないコンパイラで生成されたコードを参照するメッセージを抑制する唯一の方法は、グローバルレベルの抑制です。 たとえば、次のコードは、コンパイラによって生成されたコンストラクターに対する違反を抑制します。

 `[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> ターゲットには、常に完全修飾された項目名が含まれます。

## <a name="global-suppression-file"></a>グローバル抑制ファイル
 グローバル抑制ファイルは、グローバルレベルの抑制またはターゲットを指定しない抑制のいずれかである抑制を保持します。 たとえば、アセンブリレベルの違反の抑制は、このファイルに格納されます。 また、一部の ASP.NET 抑制は、このファイルに格納されています。これは、フォームのコードでプロジェクトレベルの設定を使用できないためです。 グローバル抑制が作成され、プロジェクトに追加されます。その際、[エラー一覧] ウィンドウの [**メッセージ**を表示しない] コマンドの [**プロジェクト抑制ファイル内**] オプションを初めて選択します。 詳細については、「 [方法: メニュー項目を使用](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md)して警告を非表示にする」を参照してください。

## <a name="see-also"></a>参照
 <xref:System.Diagnostics.CodeAnalysis>
