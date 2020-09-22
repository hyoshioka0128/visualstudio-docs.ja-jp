---
title: Office ソリューションの省略可能なパラメーター
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], optional parameters
- Visual C# [Office development in Visual Studio], optional parameters
- Visual Basic [Office development in Visual Studio], optional parameters
- application development [Office development in Visual Studio], optional parameters
- missing field [Office development in Visual Studio]
- optional parameters [Office development in Visual Studio]
- parameters [Office development in Visual Studio], optional
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e8684ad4b9429a5499660ef4ad6fdd8133dccaa5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841997"
---
# <a name="optional-parameters-in-office-solutions"></a>Office ソリューションの省略可能なパラメーター
  Microsoft Office アプリケーションのオブジェクト モデルに含まれるメソッドの多くは、省略可能なパラメーターを受け取ります。 Visual Studio で Visual Basic を使用して Office ソリューションを開発する場合は、省略可能なパラメーターに値を渡す必要はありません。省略したパラメーターに対しては自動的に既定値が使用されます。 ほとんどの場合は、Visual C# プロジェクトでも省略可能なパラメーターを省略できます。 ただし、ドキュメントレベルの Word プロジェクトでは、クラスの省略可能な **ref** パラメーターを省略することはできません `ThisDocument` 。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Visual C# と Visual Basic のプロジェクトで省略可能なパラメーターを使用する方法の詳細については、「 [名前付き引数と省略可能な引数」 &#40;C&#35; プログラミングガイド&#41;](/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments) および [省略可能なパラメーター ](/dotnet/visual-basic/programming-guide/language-features/procedures/optional-parameters)&#40;Visual Basic&#41;」を参照してください。

> [!NOTE]
> 旧バージョンの Visual Studio では、Visual C# プロジェクトのすべての省略可能なパラメーターに値を渡す必要があります。 便宜上、これらのプロジェクトには `missing` というグローバル変数が含まれています。パラメーターの既定値を使用する場合に、このグローバル変数を省略可能なパラメーターに渡すことができます。 Visual Studio の Office 用 visual C# プロジェクトにも変数が含まれてい `missing` ますが、通常、で office ソリューションを開発するときは、この変数を使用する必要はありません [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 。ただし、 **ref** `ThisDocument` Word のドキュメントレベルのプロジェクトのクラスでオプションの ref パラメーターを指定してメソッドを呼び出す場合を除きます。

## <a name="example-in-excel"></a>Excel の例
 <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> メソッドには、多くの省略可能なパラメーターがあります。 次のコード例に示すように、一部のパラメーターの値を指定し、他のパラメーターには既定値を使用することができます。 この例では、`Sheet1` というワークシート クラスを持つドキュメント レベルのプロジェクトが必要です。

 [!code-csharp[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/CSharp/excelworkbook1/Sheet1.cs#1)]
 [!code-vb[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/VisualBasic/excelworkbook1/Sheet1.vb#1)]

## <a name="example-in-word"></a>Word の例
 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> メソッドには、多くの省略可能なパラメーターがあります。 次のコード例に示すように、一部のパラメーターの値を指定し、他のパラメーターには既定値を使用することができます。

 [!code-vb[Trin_VstrefGeneralWord#1](../vsto/codesnippet/VisualBasic/worddocument1/ThisDocument.vb#1)]
 [!code-csharp[Trin_VstrefGeneralWord#1](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#1)]

## <a name="use-optional-parameters-of-methods-in-the-thisdocument-class-in-visual-c-document-level-projects-for-word"></a>Word の Visual C# ドキュメントレベルのプロジェクトで、ThisDocument クラスのメソッドの省略可能なパラメーターを使用する
 Word オブジェクトモデルには、値を受け入れるオプションの **ref** パラメーターを持つ多くのメソッドが含まれてい <xref:System.Object> ます。 ただし、 **ref** `ThisDocument` Word の Visual C# ドキュメントレベルのプロジェクトでは、生成されたクラスのメソッドの ref パラメーター (省略可能) を省略することはできません。 Visual C# では、クラスではなく、インターフェイスのメソッドに対してのみ省略可能な **ref** パラメーターを省略できます。 たとえば、次のコード例はコンパイルされません。これは、クラスのメソッドの省略可能な **ref** パラメーターを省略できないため <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> `ThisDocument` です。

 [!code-csharp[Trin_VstrefGeneralWord#3](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#3)]

 `ThisDocument` クラスのメソッドを呼び出す場合は、次のガイドラインに従います。

- 省略可能な **ref** パラメーターの既定値をそのまま使用するには、 `missing` パラメーターに変数を渡します。 `missing` 変数は Visual C# Office プロジェクトで自動的に定義され、生成されたプロジェクト コード内で <xref:System.Type.Missing> 値に割り当てられます。

- 省略可能な **ref** パラメーターに独自の値を指定するには、指定する値に割り当てられたオブジェクトを宣言し、そのオブジェクトをパラメーターに渡します。

  次のコード例では、 <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> *ignoreuppercase* パラメーターの値を指定し、他のパラメーターの既定値をそのまま使用して、メソッドを呼び出す方法を示します。

  [!code-csharp[Trin_VstrefGeneralWord#4](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#4)]

  クラスのメソッドの省略可能な **ref** パラメーターを省略するコードを記述する場合は、 `ThisDocument` <xref:Microsoft.Office.Interop.Word.Document> プロパティによって返されるオブジェクトで同じメソッドを呼び出し、 <xref:Microsoft.Office.Tools.Word.Document.InnerObject%2A> そのメソッドからパラメーターを省略することもできます。 これは、<xref:Microsoft.Office.Interop.Word.Document> がクラスではなくインターフェイスであるためです。

  [!code-csharp[Trin_VstrefGeneralWord#5](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#5)]

  値と参照型のパラメーターの詳細については、「 [引数を値で渡す」と「参照渡し &#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference) (Visual Basic の場合)」と「 [&#40;パラメーターを渡す ](/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [Office ソリューションの開発](../vsto/developing-office-solutions.md)
- [Office ソリューションでコードを記述する](../vsto/writing-code-in-office-solutions.md)
