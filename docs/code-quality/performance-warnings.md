---
title: パフォーマンスに関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.performancerules
helpviewer_keywords:
- warnings, performance
- performance warnings
- performance, warnings
- managed code analysis warnings, performance warnings
ms.assetid: e014ac3a-02e6-46d9-942c-3491dd63782f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e578bedf3e6b784321ffb14628ebbe10bc45dc20
ms.sourcegitcommit: 93859158465eab3423a0c0435f06490f0a456a57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "82167347"
---
# <a name="performance-warnings"></a>パフォーマンスに関する警告
パフォーマンスの警告は、高パフォーマンスのライブラリとアプリケーションをサポートします。

## <a name="in-this-section"></a>このセクションの内容

| ルール | 説明 |
| - | - |
| [CA1800:不必要にキャストしません](../code-quality/ca1800.md) | 二重のキャストがあるとパフォーマンスが低下します。特に、小さな繰り返しステートメントでキャストが実行される場合はそうです。 |
| [CA1801:使用されていないパラメーターの確認](../code-quality/ca1801.md) | メソッドのシグネチャに、メソッドの本体で使用されていないパラメーターがあります。 |
| [CA1802:適切な場所にリテラルを使用します](../code-quality/ca1802.md) | フィールドは静的および読み取り専用 (で[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]は Shared および ReadOnly) として宣言され、コンパイル時に計算できるという値を使用して初期化されます。 コンパイル時には対象のフィールドに割り当てられた値が計算できるであるため、宣言を const (const in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) フィールドに変更して、実行時ではなくコンパイル時に値が計算されるようにします。 |
| [CA1804:使用されていないローカルを削除します](../code-quality/ca1804.md) | 使用されていないローカル変数や不要な引数があると、アセンブリのサイズが大きくなり、パフォーマンスが低下します。 |
| [CA1806:メソッドの結果を無視しない](../code-quality/ca1806.md) | 新しいオブジェクトが作成されましたが、使用されていないか、新しい文字列を作成して返すメソッドが呼び出され、新しい文字列が使用されていないか、またはコンポーネントオブジェクトモデル (COM) または P/Invoke メソッドが、使用されていない HRESULT またはエラーコードを返しています。 |
| [CA1809:ローカルを使用しすぎないでください](../code-quality/ca1809.md) | パフォーマンス最適化の一般的な方法として、メモリではなくプロセッサのレジスタに値を格納する方法があります。これは "値のレジスタ格納" と呼ばれます。  すべてのローカル変数をレジスタ格納できるようにするには、ローカル変数の数を 64 個に制限します。 |
| [CA1810:参照型の静的フィールドをインラインで初期化します](../code-quality/ca1810.md) | 型で明示的な静的コンストラクターを宣言すると、Just-In-Time (JIT) コンパイラが、静的コンストラクターが呼び出されたことを確認するために、型の静的メソッドと静的インスタンス コンストラクターに個別にチェックを追加します。 静的コンストラクターのチェックによってパフォーマンスが低下することがあります。 |
| [CA1811:呼び出されていないプライベート コードを使用しません](../code-quality/ca1811.md) | プライベートまたは内部 (アセンブリレベル) のメンバーは、アセンブリ内の呼び出し元を持っていません。また、共通言語ランタイムによって呼び出されず、デリゲートによって呼び出されません。 |
| [CA1812:インスタンス化されていない内部クラスを使用しません](../code-quality/ca1812.md) | アセンブリ レベルの型のインスタンスが、アセンブリ内のコードから作成されません。 |
| [CA1813:アンシールド属性を使用しません](../code-quality/ca1813.md) | .NET には、カスタム属性を取得するためのメソッドが用意されています。 既定では、これらのメソッドで属性の継承階層が検索されます。 属性をシールすると、継承階層の全体が検索されなくなるため、パフォーマンスが向上します。 |
| [CA1814:複数次元の配列ではなくジャグ配列を使用します](../code-quality/ca1814.md) | ジャグ配列とは、その要素も配列である配列です。 要素を構成する配列のサイズは異なる可能性があるため、一部のデータセットで無駄な領域が生じる可能性があります。 |
| [CA1815:equals および operator equals を値型でオーバーライドします](../code-quality/ca1815.md) | 値型の場合、Equals を継承した実装が Reflection ライブラリを使用して、すべてのフィールドの内容を比較します。 Reflection は計算コストが高いため、場合によってはすべてのフィールドで等値性を比較する必要はありません。 ユーザーがインスタンスの比較または並べ替えを行うことや、ハッシュ テーブル キーとしてインスタンスを使用することが予想される場合には、値型に Equals を実装する必要があります。 |
| [CA1816:GC.SuppressFinalize を正しく呼び出します](../code-quality/ca1816.md) | Dispose の実装であるメソッドは、GC を呼び出しません。Gc.suppressfinalize、または Dispose の実装ではないメソッドは GC を呼び出します。Gc.suppressfinalize、またはメソッドは GC を呼び出します。Gc.suppressfinalize は、この (では[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]Me) 以外のものを渡します。 |
| [CA1819:プロパティは、配列を返すことはできません](../code-quality/ca1819.md) | プロパティが読み取り専用の場合でも、プロパティによって返される配列は書き込み禁止になりません。 配列の改ざんを防ぐには、プロパティで配列のコピーを返す必要があります。 一般に、このようなプロパティを呼び出すときのパフォーマンス低下は理解されません。 |
| [CA1820:文字列の長さを使用して空の文字列をテストします](../code-quality/ca1820.md) | String.Length プロパティまたは String.IsNullOrEmpty メソッドを使用して文字列を比較する方法は、Equals を使用する場合よりもはるかに高速です。 |
| [CA1821:空のファイナライザーを削除します](../code-quality/ca1821.md) | オブジェクトの有効期間の追跡に関連するパフォーマンス オーバーヘッドが増大するため、ファイナライザーは可能な限り使用しないでください。 空のファイナライザーを使用すると、追加のオーバーヘッドが発生します。 |
| [CA1822:メンバーを static に設定します](../code-quality/ca1822.md) | インスタンス データにアクセスしない、またはインスタンス メソッドを呼び出さないメンバーは、静的 ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では共有) としてマークできます。 メソッドを静的としてマークすると、コンパイラはこれらのメンバーに対する非仮想呼び出しサイトを出力します。 パフォーマンス重視のコードでは、これにより大きくパフォーマンスを向上できます。 |
| [CA1823:使用されていないプライベート フィールドを使用しません](../code-quality/ca1823.md) | アセンブリ内でアクセスされていないと思われるプライベート フィールドが検出されました。 |
| [CA1824:アセンブリを NeutralResourcesLanguageAttribute に設定します](../code-quality/ca1824.md) | NeutralResourcesLanguage 属性は、ResourceManager に対し、アセンブリのニュートラル カルチャのリソースを表示するために使用した言語を通知します。 これにより、読み込んだ最初のリソースに対する検索のパフォーマンスが向上し、ワーキング セットを縮小できます。 |
| [CA1825:長さ 0 の配列割り当てを回避します](../code-quality/ca1825.md) | 長さ0の配列を初期化すると、不要なメモリ割り当てにつながります。 代わりに、を呼び出す<xref:System.Array.Empty%2A?displayProperty=nameWithType>ことによって、静的に割り当てられた空の配列インスタンスを使用します。 メモリ割り当ては、このメソッドのすべての呼び出しで共有されます。 |
| [CA1826: Linq の列挙可能なメソッドの代わりにプロパティを使用します](../code-quality/ca1826.md) | <xref:System.Linq.Enumerable>LINQ メソッドが、同等のより効率的なプロパティをサポートする型で使用されました。 |
| [CA1827: 使用可能な場合、Count/LongCount を使用しないでください](../code-quality/ca1827.md) | <xref:System.Linq.Enumerable.Count%2A>また<xref:System.Linq.Enumerable.LongCount%2A>はメソッドが使用<xref:System.Linq.Enumerable.Any%2A>されました。メソッドの方が効率的です。 |
| [CA1828: AnyAsync を使用できる場合は、CountAsync/LongCountAsync を使用しないでください。](../code-quality/ca1828.md) | <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.CountAsync%2A>また<xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.LongCountAsync%2A>はメソッドが使用<xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.AnyAsync%2A>されました。メソッドの方が効率的です。 |
| [CA1829: Count メソッドではなく、Length/Count プロパティを使用します](../code-quality/ca1829.md) | <xref:System.Linq.Enumerable.Count%2A>LINQ メソッドは、同等の、より効率的`Length`なまたは`Count`プロパティをサポートする型で使用されていました。 |
