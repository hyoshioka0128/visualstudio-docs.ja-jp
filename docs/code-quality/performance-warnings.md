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
ms.openlocfilehash: 13cb3e83b06b3533d1feb1e683fb246f238da732
ms.sourcegitcommit: 6a43ace7b84c401ebd03f65abc17ae1d2a21a130
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2020
ms.locfileid: "89471480"
---
# <a name="performance-warnings"></a>パフォーマンスに関する警告
パフォーマンスの警告は、高パフォーマンスのライブラリとアプリケーションをサポートします。

## <a name="in-this-section"></a>このセクションの内容

| ルール | 説明 |
| - | - |
| [CA1800:不必要にキャストしません](../code-quality/ca1800.md) | 二重のキャストがあるとパフォーマンスが低下します。特に、小さな繰り返しステートメントでキャストが実行される場合はそうです。 |
| [CA1801:使用されていないパラメーターの確認](../code-quality/ca1801.md) | メソッドのシグネチャに、メソッドの本体で使用されていないパラメーターがあります。 |
| [CA1802:適切な場所にリテラルを使用します](../code-quality/ca1802.md) | フィールドは静的および読み取り専用 (では Shared および ReadOnly) として宣言され [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 、コンパイル時に計算できるという値を使用して初期化されます。 コンパイル時には対象のフィールドに割り当てられた値が計算できるであるため、宣言を const (const in) フィールドに変更して、実行時で [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] はなくコンパイル時に値が計算されるようにします。 |
| [CA1804:使用されていないローカルを削除します](../code-quality/ca1804.md) | 使用されていないローカル変数や不要な引数があると、アセンブリのサイズが大きくなり、パフォーマンスが低下します。 |
| [CA1805:不必要に初期化しない](../code-quality/ca1805.md) | .NET ランタイムは、コンストラクターを実行する前に、参照型のすべてのフィールドを既定値に初期化します。 ほとんどの場合、フィールドを既定値に明示的に初期化することは冗長であり、メンテナンスコストがかかり、パフォーマンスが低下する可能性があります (アセンブリサイズの増加など)。 |
| [CA1806:メソッドの結果を無視しない](../code-quality/ca1806.md) | 新しいオブジェクトが作成されましたが、使用されていないか、新しい文字列を作成して返すメソッドが呼び出され、新しい文字列が使用されていないか、またはコンポーネントオブジェクトモデル (COM) または P/Invoke メソッドが、使用されていない HRESULT またはエラーコードを返しています。 |
| [CA1809:ローカルを使用しすぎないでください](../code-quality/ca1809.md) | パフォーマンス最適化の一般的な方法として、メモリではなくプロセッサのレジスタに値を格納する方法があります。これは "値のレジスタ格納" と呼ばれます。  すべてのローカル変数をレジスタ格納できるようにするには、ローカル変数の数を 64 個に制限します。 |
| [CA1810:参照型の静的フィールドをインラインで初期化します](../code-quality/ca1810.md) | 型で明示的な静的コンストラクターを宣言すると、Just-In-Time (JIT) コンパイラが、静的コンストラクターが呼び出されたことを確認するために、型の静的メソッドと静的インスタンス コンストラクターに個別にチェックを追加します。 静的コンストラクターのチェックによってパフォーマンスが低下することがあります。 |
| [CA1811:呼び出されていないプライベート コードを使用しません](../code-quality/ca1811.md) | プライベートまたは内部 (アセンブリレベル) のメンバーは、アセンブリ内の呼び出し元を持っていません。また、共通言語ランタイムによって呼び出されず、デリゲートによって呼び出されません。 |
| [CA1812:インスタンス化されていない内部クラスを使用しません](../code-quality/ca1812.md) | アセンブリ レベルの型のインスタンスが、アセンブリ内のコードから作成されません。 |
| [CA1813:アンシールド属性を使用しません](../code-quality/ca1813.md) | .NET には、カスタム属性を取得するためのメソッドが用意されています。 既定では、これらのメソッドで属性の継承階層が検索されます。 属性をシールすると、継承階層の全体が検索されなくなるため、パフォーマンスが向上します。 |
| [CA1814:複数次元の配列ではなくジャグ配列を使用します](../code-quality/ca1814.md) | ジャグ配列とは、その要素も配列である配列です。 要素を構成する配列のサイズは異なる可能性があるため、一部のデータセットで無駄な領域が生じる可能性があります。 |
| [CA1815:equals および operator equals を値型でオーバーライドします](../code-quality/ca1815.md) | 値型の場合、Equals を継承した実装が Reflection ライブラリを使用して、すべてのフィールドの内容を比較します。 Reflection は計算コストが高いため、場合によってはすべてのフィールドで等値性を比較する必要はありません。 ユーザーがインスタンスの比較または並べ替えを行うことや、ハッシュ テーブル キーとしてインスタンスを使用することが予想される場合には、値型に Equals を実装する必要があります。 |
| [CA1816:GC.SuppressFinalize を正しく呼び出します](../code-quality/ca1816.md) | Dispose の実装であるメソッドは、GC を呼び出しません。Gc.suppressfinalize、または Dispose の実装ではないメソッドは GC を呼び出します。Gc.suppressfinalize、またはメソッドは GC を呼び出します。Gc.suppressfinalize は、この (では Me) 以外のものを渡し [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ます。 |
| [CA1819:プロパティは、配列を返すことはできません](../code-quality/ca1819.md) | プロパティが読み取り専用の場合でも、プロパティによって返される配列は書き込み禁止になりません。 配列の改ざんを防ぐには、プロパティで配列のコピーを返す必要があります。 一般に、このようなプロパティを呼び出すときのパフォーマンス低下は理解されません。 |
| [CA1820:文字列の長さを使用して空の文字列をテストします](../code-quality/ca1820.md) | String.Length プロパティまたは String.IsNullOrEmpty メソッドを使用して文字列を比較する方法は、Equals を使用する場合よりもはるかに高速です。 |
| [CA1821:空のファイナライザーを削除します](../code-quality/ca1821.md) | オブジェクトの有効期間の追跡に関連するパフォーマンス オーバーヘッドが増大するため、ファイナライザーは可能な限り使用しないでください。 空のファイナライザーを使用すると、追加のオーバーヘッドが発生します。 |
| [CA1822:メンバーを static に設定します](../code-quality/ca1822.md) | インスタンス データにアクセスしない、またはインスタンス メソッドを呼び出さないメンバーは、静的 ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では共有) としてマークできます。 メソッドを静的としてマークすると、コンパイラはこれらのメンバーに対する非仮想呼び出しサイトを出力します。 パフォーマンス重視のコードでは、これにより大きくパフォーマンスを向上できます。 |
| [CA1823:使用されていないプライベート フィールドを使用しません](../code-quality/ca1823.md) | アセンブリ内でアクセスされていないと思われるプライベート フィールドが検出されました。 |
| [CA1824:アセンブリを NeutralResourcesLanguageAttribute に設定します](../code-quality/ca1824.md) | NeutralResourcesLanguage 属性は、アセンブリのニュートラルカルチャのリソースを表示するために使用された言語をリソースマネージャーに通知します。 これにより、読み込んだ最初のリソースに対する検索のパフォーマンスが向上し、ワーキング セットを縮小できます。 |
| [CA1825:長さ 0 の配列割り当てを回避します](../code-quality/ca1825.md) | 長さ0の配列を初期化すると、不要なメモリ割り当てにつながります。 代わりに、を呼び出すことによって、静的に割り当てられた空の配列インスタンスを使用し <xref:System.Array.Empty%2A?displayProperty=nameWithType> ます。 メモリ割り当ては、このメソッドのすべての呼び出しで共有されます。 |
| [CA1826:Linq の列挙可能なメソッドの代わりにプロパティを使用します](../code-quality/ca1826.md) | <xref:System.Linq.Enumerable> LINQ メソッドが、同等のより効率的なプロパティをサポートする型で使用されました。 |
| [CA1827:Any が使用できる場合は Count/LongCount を使用しません](../code-quality/ca1827.md) | <xref:System.Linq.Enumerable.Count%2A> または <xref:System.Linq.Enumerable.LongCount%2A> メソッドが使用されました <xref:System.Linq.Enumerable.Any%2A> 。メソッドの方が効率的です。 |
| [CA1828:AnyAsync が使用できる場合は CountAsync/LongCountAsync を使用しません](../code-quality/ca1828.md) | <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.CountAsync%2A> または <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.LongCountAsync%2A> メソッドが使用されました <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.AnyAsync%2A> 。メソッドの方が効率的です。 |
| [CA1829:Enumerable. Count メソッドではなく Length/Count プロパティを使用します](../code-quality/ca1829.md) | <xref:System.Linq.Enumerable.Count%2A> LINQ メソッドは、同等の、より効率的なまたはプロパティをサポートする型で使用されていま `Length` `Count` した。 |
| [CA1830:StringBuilder の厳密に型指定された Append および Insert メソッドのオーバーロードをお勧めします](../code-quality/ca1830.md) | <xref:System.Text.StringBuilder.Append%2A> と <xref:System.Text.StringBuilder.Insert%2A> は、system.string 以外の複数の型のオーバーロードを提供します。  可能であれば、ToString () と文字列ベースのオーバーロードを使用して、厳密に型指定されたオーバーロードを優先します。 |
| [CA1831: 該当する場合、文字列に範囲ベースのインデクサーの代わりに AsSpan を使用します](../code-quality/ca1831.md) | 文字列に対して range-インデクサーを使用し、その値を暗黙的に ReadOnlySpan char 型に割り当てると、 &lt; &gt; の代わりにメソッドが <xref:System.String.Substring%2A?#System_String_Substring_System_Int32_System_Int32_> 使用され、 <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> 文字列の要求された部分のコピーが生成されます。 |
| [CA1832: 配列の ReadOnlySpan または ReadOnlyMemory 部分を取得するために、範囲ベースのインデクサーの代わりに AsSpan または AsMemory を使用します](../code-quality/ca1832.md) | 配列に対して範囲インデクサーを使用し、その値を型または型に暗黙的に割り当てると、 <xref:System.ReadOnlySpan%601> <xref:System.ReadOnlyMemory%601> の代わりにメソッドが <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> 使用され <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> ます。これにより、配列の要求された部分のコピーが生成されます。 |
| [CA1833: 配列の Span または Memory 部分を取得するために、範囲ベースのインデクサーの代わりに AsSpan または AsMemory を使用します](../code-quality/ca1833.md) | 配列に対して範囲インデクサーを使用し、その値を型または型に暗黙的に割り当てると、 <xref:System.Span%601> <xref:System.Memory%601> の代わりにメソッドが <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> 使用され <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> ます。これにより、配列の要求された部分のコピーが生成されます。 |
| [CA1834: 1 つの文字列に対して StringBuilder (char) を使用します。](../code-quality/ca1834.md) | <xref:System.Text.StringBuilder> には `Append` 、引数としてを受け取るオーバーロードがあり `char` ます。 `char`パフォーマンスを向上させるために、オーバーロードの呼び出しを優先します。 |
| [CA1835: ' ReadAsync ' と ' WriteAsync ' に対して ' Memory' に基づくオーバーロードを優先します](../code-quality/ca1835.md) | ' Stream ' には、最初の引数として ' Memory byte ' を受け取る ' ReadAsync ' オーバーロード &lt; &gt; と、 &lt; &gt; 1 番目の引数として ' ReadOnlyMemory Byte ' を受け取る ' WriteAsync ' オーバーロードがあります。 より効率的なメモリベースのオーバーロードを呼び出すことをお勧めします。 |
| [CA1836: `IsEmpty` `Count` 使用可能な場合は優先します。](../code-quality/ca1836.md) | `IsEmpty` `Count` `Length` <xref:System.Linq.Enumerable.Count%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> <xref:System.Linq.Enumerable.LongCount%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> オブジェクトに項目が含まれているかどうかを判断するために、、、またはよりも効率的なプロパティを優先します。 |
| [CA1837: `Environment.ProcessId` の代わりにを使用します。 `Process.GetCurrentProcess().Id`](../code-quality/ca1837.md) | `Environment.ProcessId` はより単純で高速です `Process.GetCurrentProcess().Id` 。 |
| [CA1838: `StringBuilder` P/invoke のパラメーターを使用しない](../code-quality/ca1838.md) | のマーシャリングでは `StringBuilder` 、常にネイティブバッファーコピーが作成されるため、1つのマーシャリング操作に複数の割り当てが行われます。 |
