---
title: グローバリゼーションの警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.globalizationrules
helpviewer_keywords:
- warnings, globalization
- globalization warnings
- globalization [Visual Studio], warnings
- managed code analysis warnings, globalization warnings
ms.assetid: a8d12d41-14bf-4b43-af24-168312d7c390
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fecc46ac6e1221cb547e98711d95b743010d4c6c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587577"
---
# <a name="globalization-warnings"></a>グローバリゼーションの警告
グローバリゼーションの警告は、国際対応のライブラリとアプリケーションをサポートします。

## <a name="in-this-section"></a>このセクションの内容

|規則|説明|
|----------|-----------------|
|[CA1300: MessageBoxOption を指定します](../code-quality/ca1300.md)|テキストを右から左へ読むカルチャでメッセージ ボックスを正しく表示するには、MessageBoxOptions 列挙体の RightAlign メンバーと RtlReading メンバーを、Show メソッドに渡す必要があります。|
|[CA1301: アクセラレータが重複しないようにします](../code-quality/ca1301.md)|Alt キーを使用するアクセス キー (アクセラレータとも呼ばれます) によって、キーボードからコントロールにアクセスできます。 複数のコントロールが重複するアクセスキーを持っている場合、アクセスキーの動作は適切に定義されていません。|
|[CA1302: ロケール特有の文字列をハードコードしません](../code-quality/ca1302.md)|System.Environment.SpecialFolder 列挙体には、特殊なシステム フォルダーを参照するメンバーが含まれます。 このフォルダーの位置は、オペレーティング システムによって異なる場合、ユーザーが位置を変更する場合、および位置がローカライズされる場合があります。 System.environment.specialfolder 列挙型に関連付けられている場所は、GetFolderPath メソッドによって返されます。これは、現在実行中のコンピューターに適しています。|
|[CA1303: ローカライズされたパラメーターとしてリテラルを渡さないでください](../code-quality/ca1303.md)|外部から参照できるメソッドは、.NET コンストラクターまたはメソッドにパラメーターとして文字列リテラルを渡し、その文字列はローカライズ可能である必要があります。|
|[CA1304: CultureInfo を指定します](../code-quality/ca1304.md)|System.Globalization.CultureInfo パラメーターを受け入れるオーバーロードを持つメンバーを呼び出しているメソッドまたはコンストラクターが、CultureInfo パラメーターを使用するオーバーロードを呼び出していません。 CultureInfo オブジェクトまたは System.IFormatProvider オブジェクトが指定されない場合、オーバーロードされたメンバーから提示された既定値は、すべてのロケールに効果が及ばない可能性があります。|
|[CA1305: IFormatProvider を指定します](../code-quality/ca1305.md)|System.IFormatProvider パラメーターを受け入れるオーバーロードを持つメンバーを 1 つ以上呼び出しているメソッドまたはコンストラクターが、IFormatProvider パラメーターを使用するオーバーロードを呼び出していません。 System.Globalization.CultureInfo オブジェクトまたは IFormatProvider オブジェクトが指定されない場合、オーバーロードされたメンバーから提示された既定値は、すべてのロケールに効果が及ばない可能性があります。|
|[CA1306: データ型のロケールを設定します](../code-quality/ca1306.md)|ロケールによって、データに関するカルチャ固有の表示要素が決まります。たとえば、数値、通貨記号、並べ替え順序に使用する形式などです。 DataTable または DataSet を作成するときは、ロケールを明示的に設定する必要があります。|
|[CA1307: StringComparison の指定](../code-quality/ca1307.md)|文字列比較演算で、StringComparison パラメーターを設定しないメソッド オーバーロードが使用されています。|
|[CA1308: 文字列を大文字に標準化します](../code-quality/ca1308.md)|文字列は大文字に正規化する必要があります。 小文字への変換時に 1 つの小さい文字グループをラウンド トリップさせることができません。|
|[CA1309: 順序を示す StringComparison を使用します](../code-quality/ca1309.md)|非言語的な文字列比較演算で、StringComparison パラメーターが Ordinal または OrdinalIgnoreCase に設定されていません。 パラメーターを StringComparison.Ordinal または StringComparison.OrdinalIgnoreCase に明示的に設定することによって、多くの場合、コードの速度、正確さ、および信頼性が向上します。|
|[CA2101: P/Invoke 文字列引数に対してマーシャリングを指定します](../code-quality/ca2101.md)|プラットフォーム呼び出しメンバーは、部分的に信頼された呼び出し元を許可し、文字列パラメーターを持ち、文字列を明示的にマーシャリングしません。 これはセキュリティ上の脆弱性となる可能性があります。|
