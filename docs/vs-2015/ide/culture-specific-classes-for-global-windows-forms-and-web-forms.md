---
title: グローバルな Windows フォームおよび Web フォームにおけるカルチャ固有のクラス | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- globalization [Windows Forms], classes
- Web applications [.NET Framework], globalization
- culture, culture-specific classes
- numbers, international
- localization [Windows Forms], classes
- globalization [Visual Studio], culture-specific classes
- Windows Forms, localization
- international applications [Visual Studio], data formats
- time [Visual Studio], international
- dates [Visual Studio], international
- culture
- international characters
- currency formats
- ASP.NET, globalization
- classes [Visual Studio], culture-specific
- localization [Visual Studio], culture-specific classes
ms.assetid: 0d06a0a4-f887-4f7c-bde7-1d543c06f803
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6c2d048387e4e81763a63b5bf010c36c87beeacf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665908"
---
# <a name="culture-specific-classes-for-global-windows-forms-and-web-forms"></a>グローバルな Windows フォームおよび Web フォームにおけるカルチャ固有のクラス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

各カルチャには、日付、時間、数、通貨などの情報を表示するさまざまな規約があります。 <xref:System.Globalization> 名前空間には、<xref:System.Globalization.DateTimeFormatInfo>、**Calendar**、<xref:System.Globalization.NumberFormatInfo> など、カルチャ固有の値の表示方法を変更するために使用できるクラスが含まれています。

## <a name="using-the-culture-setting"></a>カルチャ設定の使用
 ただし、ほとんどの場合、アプリケーションまたは **[地域のオプション]** コントロール パネルのどちらかに保存されているカルチャ設定を使用して、規約を実行時に自動で判別しそれに応じて情報の形式を設定できます。 カルチャの設定方法の詳細については、「[方法 : Windows フォームのグローバリゼーション用のカルチャおよび UI カルチャを設定する](https://msdn.microsoft.com/694e049f-0b91-474a-9789-d35124f248f0)」または「[方法: ASP.NET Web ページのグローバリゼーション用のカルチャおよび UI カルチャを設定する](https://msdn.microsoft.com/library/76091f86-f967-4687-a40f-de87bd8cc9a0)を参照してください。 カルチャ設定に基づいて情報の形式を自動で設定するクラスは、カルチャ固有と呼ばれます。 カルチャ固有のメソッドには、<xref:System.IFormattable.ToString%2A?displayProperty=fullName>、<xref:System.Console.WriteLine%2A?displayProperty=fullName>、<xref:System.String.Format%2A?displayProperty=fullName> があります。 カルチャ固有の関数 (Visual Basic 言語) には、`MonthName` や `WeekDayName` などがあります。

 例として、次のコードに <xref:System.IFormattable.ToString%2A> メソッドを使用して、現在のカルチャで通貨の形式を設定する方法を示します。

```vb
' Put the Imports statements at the beginning of the code module
Imports System.Threading
Imports System.Globalization
' Display a number with the culture-specific currency formatting
Dim MyInt As Integer = 100
Console.WriteLine(MyInt.ToString("C", Thread.CurrentThread.CurrentCulture))

```

```csharp
// Put the using statements at the beginning of the code module
using System.Threading;
using System.Globalization;
// Display a number with the culture-specific currency formatting
int myInt = 100;
Console.WriteLine(myInt.ToString("C", Thread.CurrentThread.CurrentCulture));
```

 カルチャが "fr-FR" に設定されている場合は、出力ウィンドウの表示は次のようになります。

 `100,00`

 カルチャが "en-US" に設定されている場合は、出力ウィンドウの表示は次のようになります。

 `$100.00`

## <a name="see-also"></a>参照
 <xref:System.IFormattable.ToString%2A?displayProperty=fullName> <xref:System.Globalization.DateTimeFormatInfo>
 <xref:System.Globalization.NumberFormatInfo>
 <xref:System.Globalization.Calendar>
 <xref:System.Console.WriteLine%2A?displayProperty=fullName>
 <xref:System.String.Format%2A?displayProperty=fullName>
 [アプリケーションのグローバライズとローカライズ](../ide/globalizing-and-localizing-applications.md)
