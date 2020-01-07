---
title: LINQ to XML による WPF のデータ バインディングの概要 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 3bf80845-891b-41de-a71b-4080b5bd3ea6
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 751840960288f46c0a1ca09ebe80a2b8e7603359
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299530"
---
# <a name="wpf-data-binding-with-linq-to-xml-overview"></a>LINQ to XML による WPF のデータ バインディングの概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、<xref:System.Xml.Linq> 名前空間の動的データ バインド機能について説明します。 これらの機能は、Windows Presentation Foundation (WPF) のユーザー インターフェイス (UI) 要素のデータ ソースとして使用できます。

## <a name="xaml-and-linq-to-xml"></a>XAML と LINQ to XML
 Extensible Application Markup Language (XAML) は、.NET Framework 3.0 のテクノロジをサポートするために Microsoft によって作成された XML 言語です。 XAML は、WPF ではユーザー インターフェイス要素やその関連機能 (イベントやデータ バインドなど) を表すために使用され、 Windows Workflow Foundation ではプログラム制御 (*ワークフロー*) などのプログラム構造を表すために使用されます。 XAML を使用すると、テクノロジの宣言型の側面を、プログラムのより個別的な動作を定義する、関連する手続き型のコードから分離することができます。

 XAML と LINQ to XML の相互作用には、大きく分けて次の 2 つの方法があります。

- XAML ファイルは整形式の XML であるため、LINQ to XML などの XML テクノロジによるクエリや操作が可能です。

- LINQ to XML のクエリはデータのソースを表すため、WPF UI 要素のデータ バインドのデータ ソースとして使用できます。

  このドキュメントでは、2 番目のシナリオについて説明します。

## <a name="data-binding-in-the-windows-presentation-foundation"></a>Windows Presentation Foundation のデータ バインド
 WPF のデータ バインディングでは、UI 要素のプロパティをデータ ソースに関連付けることができます。 たとえば、ユーザー定義オブジェクトのパブリック プロパティの値をテキストとして表示する <xref:System.Windows.Controls.Label> はその簡単な例です。 WPF のデータ バインディングは次のコンポーネントに依存しています。

|コンポーネント|説明|
|---------------|-----------------|
|バインド ターゲット|データ ソースに関連付ける UI 要素。 WPF のビジュアル要素は <xref:System.Windows.UIElement> クラスから派生します。|
|対象になるプロパティ|バインド ターゲットの*依存プロパティ*。データ バインディング ソースの値が反映されます。 依存プロパティは、<xref:System.Windows.DependencyObject> の派生元である <xref:System.Windows.UIElement> クラスによって直接サポートされます。|
|バインド ソース|表示のために UI 要素に渡される 1 つ以上の値のソース オブジェクト。 WPF で自動的にサポートされるバインド ソースは、CLR オブジェクト、ADO.NET データ オブジェクト、XML データ (XPath または LINQ to XML のクエリからの XML データ)、および他の <xref:System.Windows.DependencyObject> です。|
|ソース パス|バインドされる値または値のセットに解決されるバインド ソースのプロパティ。|

 依存プロパティは WPF 固有の概念であり、UI 要素の動的に計算されるプロパティを表します。 たとえば、依存プロパティの既定値は多くの場合、親要素によって提供されます。 これらの特殊なプロパティは、<xref:System.Windows.DependencyProperty> クラスのインスタンスに基づいています (標準のプロパティはフィールドに基づいています)。 依存関係プロパティの詳細については、「[依存関係プロパティの概要](https://msdn.microsoft.com/library/d119d00c-3afb-48d6-87a0-c4da4f83dee5)」を参照してください。

### <a name="dynamic-data-binding-in-wpf"></a>WPF の動的データ バインディング
 既定では、対象となる UI 要素が初期化されたときにだけデータ バインディングが行われます。 これを*ワンタイム* バインドと呼びます。 ほとんどの場合、このバインドは十分には役立ちません。一般に、データ バインディングのソリューションでは、次のいずれかの方法を使用して実行時に変更が動的に反映されるようにする必要があります。

- *一方向*のバインド。一方に対する変更が自動的に反映されます。 ソースに対する変更がターゲットに反映されるのが最も一般的ですが、その逆のパターンが役に立つ場合もあります。

- *双方向*のバインド。ソースに対する変更がターゲットに、ターゲットに対する変更がソースに、それぞれ自動的に反映されます。

  一方向または双方向のバインドが行われるようにするには、変更通知のメカニズムをソースに実装する必要があります。たとえば、<xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスを実装するか、サポートする各プロパティに対して *PropertyNameChanged* パターンを使用します。

  WPF のデータ バインディングの詳細については、「[データ バインディングの概要](https://msdn.microsoft.com/library/90f79b97-17e7-40d1-abf0-3ba600ad1d7e)」を参照してください。

## <a name="dynamic-properties-in-linq-to-xml-classes"></a>LINQ to XML クラスの動的プロパティ
 ほとんどの LINQ to XML クラスは、WPF の動的データ ソースとして適切ではありません。その理由は、最も有用な情報の一部はメソッドを経由した場合にのみ取得でき (プロパティでは取得できません)、LINQ to XML クラスのプロパティには変更通知も実装されていないためです。 LINQ to XML では、WPF のデータ バインディングをサポートするために一連の*動的プロパティ*が公開されます。

 これらの動的プロパティは、<xref:System.Xml.Linq.XAttribute> クラスと <xref:System.Xml.Linq.XElement> クラスの既存のメソッドやプロパティと同じ機能を持つ特殊な実行時プロパティであり、 これらのクラスを WPF の動的データ ソースとして使用することのみを目的として追加されています。 この目的を満たすため、これらすべての動的プロパティに変更通知が実装されています。 これらの動的プロパティの詳細については、次の「[LINQ to XML の動的プロパティ](../designers/linq-to-xml-dynamic-properties.md)」を参照してください。

> [!NOTE]
> <xref:System.Xml.Linq> 名前空間のさまざまなクラスに含まれている標準のパブリック プロパティの多くは、一方向のデータ バインドには使用できます。 ただし、既に説明したように、一方向のデータ バインドではソースもターゲットも動的に更新されません。

### <a name="accessing-dynamic-properties"></a>動的プロパティへのアクセス
 <xref:System.Xml.Linq.XAttribute> クラスと <xref:System.Xml.Linq.XElement> クラスの動的プロパティには、標準のプロパティのようにアクセスすることはできません。 たとえば、C# などの CLR 準拠の言語で次のような操作を行うことはできません。

- コンパイル時に直接アクセスする。 動的プロパティは、コンパイラや Visual Studio の IntelliSense からは見えません。

- .NET リフレクションを使用して実行時に検出またはアクセスする。 動的プロパティは実行時においても、CLR の基本的な意味でのプロパティではありません。

  C# で動的プロパティへアクセスするには、実行時に <xref:System.ComponentModel> 名前空間の機能を使用する必要があります。

  一方、XML ソースでは、次のような形式の単純な表記法を使用して動的プロパティにアクセスできます。

```
<object>.<dynamic-property>
```

 この 2 つのクラスの動的プロパティは、1 つの値またはインデクサーのいずれかに解決されます。1 つの値の場合は直接使用できますが、インデクサーの場合は、結果の値または値のコレクションを取得するにはインデックスを渡す必要があります。 インデクサーの場合の構文は次のようになります。

```
<object>.<dynamic-property>[<index-value>]
```

 詳細については、「[LINQ to XML の動的プロパティ](../designers/linq-to-xml-dynamic-properties.md)」を参照してください。

 WPF の動的バインドを実装するには、動的プロパティを <xref:System.Windows.Data> 名前空間 (特に <xref:System.Windows.Data.Binding> クラス) の機能と共に使用します。

## <a name="see-also"></a>関連項目
 [LINQ to XML を使用した wpf のデータバインディング](../designers/wpf-data-binding-with-linq-to-xml.md)[ワークフローマークアップを使用し](https://go.microsoft.com/fwlink/?LinkId=98685)た[wpf](https://msdn.microsoft.com/library/5d858575-a83b-42df-ad3f-047ed2d6e3c8) [データバインディング (wpf)](https://msdn.microsoft.com/library/90f79b97-17e7-40d1-abf0-3ba600ad1d7e)の[動的プロパティ XAML LINQ to XML](../designers/linq-to-xml-dynamic-properties.md)
