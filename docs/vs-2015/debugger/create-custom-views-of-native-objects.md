---
title: ネイティブオブジェクトのカスタムビューを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- natvis
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 2d9a177a-e14b-404f-a6af-49498eff0bd7
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a510c522723cf991c7a3fff21542a069a3de000a
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299483"
---
# <a name="create-custom-views-of-native-objects"></a>ネイティブ オブジェクトのカスタム ビューを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の Natvis フレームワークでは、 **[ウォッチ]** 、 **[ローカル]** 、 **[データヒント]** のウィンドウのようなデバッガーの変数ウィンドウを Visual Studio でどのように表示するかをカスタマイズできます。  

 Natvis は、以前のバージョンの Visual Studio で使用されていた **autoexp.dat** ファイルよりも優先され、XML 構文の使用、より高度な診断、バージョン管理、複数ファイルのサポートが可能になります。  

> [!NOTE]
> Natvis フレームワークは次の場合には視覚化に使用されません。  
> 
> - [デバッガーのタイプ] を **[混合]** に設定して、C++  Windows のデスクトップ プロジェクトをデバッグしている。  
>   - マネージド互換モード ( **[ツール] / [オプション] / [デバッグ] / [一般] / [マネージド互換モードを使用する]** ) を使用して、Windows デスクトップ アプリケーションで混合モードのデバッグを行っている。  
>   - マネージ互換モード ( **[ツール] / [オプション] / [デバッグ] / [一般] / [Natvis 互換モードを使用する]** ) を使用して、Windows デスクトップ アプリケーションのデバッグを行っている。  

## <a name="BKMK_Why_create_visualizations_"></a> Natvis 視覚化を作成する理由  
 Natvis フレームワークを使用して型の視覚化ルールを作成すると、開発者がデバッグ中に型を確認しやすくなります。  

 たとえば、次の画像に示しているのは、カスタム視覚化が適用されずにデバッガーに表示された [Windows::UI::Xaml::Controls::TextBox](https://go.microsoft.com/fwlink/?LinkId=258422) 型の変数です。  

 ![TextBox の既定の視覚化](../debugger/media/dbg-natvis-textbox-default.png "DBG_NATVIS_TextBox_Default")  

 強調表示された行には `Text` クラスの `TextBox` プロパティが示されています。 クラスの階層構造が複雑なため、この値を見つけるのは困難です。さらに、デバッガーはオブジェクトによって使用されるカスタム文字列型を解釈する方法がわからないため、TextBox 内の文字列を表示できません。  

 同じ `TextBox` でも、カスタム視覚化ルールが適用されると、変数ウィンドウで非常に見やすくなります。 デバッガーはクラスの重要なメンバーも共に表示でき、カスタム文字列型の基になる文字列値も表示できます。  

 ![ビジュアライザーを使用したテキストボックスデータ](../debugger/media/dbg-natvis-textbox-visualizer.png "DBG_NATVIS_TextBox_Visualizer")  

## <a name="BKMK_Using_Natvis_files"></a> Natvis ファイルの使用  
 .natvis ファイルは .natvis という拡張子を持つ XML ファイルです。 スキーマは **%VSINSTALLDIR%\Xml\Schemas\natvis.xsd**で定義します。  

 .natvis ファイルの基本的な構造は 1 つ以上の `Type` 要素です。各 `Type` 要素は型の視覚化エントリを表し、型の完全修飾名が `Name` 属性で指定されます。  

```xml  

<?xml version="1.0" encoding="utf-8"?>  
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">  
  <Type Name="MyNamespace::CFoo">  
    .  
    .  
  </Type>  

  <Type Name="...">  
    .  
    .  
  </Type>  
</AutoVisualizer>  
```  

 Visual Studio には **%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers** フォルダーに .natvis ファイルがいくつか用意されています。 これらのファイルは、多くの一般的な型に関する視覚化ルールを格納しており、新しい型の視覚化を記述するときに例として使用できます。  

## <a name="adding-natvis-files-to-your-projects"></a><ph type="join"></ph>プロジェクトに .natvis ファイルを追加しています。  
 <ph type="join"></ph>.natvis ファイルはすべての C++ プロジェクトに追加できます。  

 オープン C++ プロジェクトを使用して新しい .natvis ファイルを追加するには、 **[ソリューション エクスプローラー]** でプロジェクト ノードを選んで、 **[追加] / [新しい項目] / [Visual C++] / [ユーティリティ] / [デバッガー視覚化ファイル (.natvis)]** をクリックします。 デバッガーは Natvis ファイルを C++ プロジェクトから自動的に読み込みます。 既定では、プロジェクトの Natvis ファイルは、プロジェクトによってビルドされた .pdb ファイルにも挿入されます。 つまり、このプロジェクトでビルドされたバイナリをデバッグする場合、たとえプロジェクトを開かなくても、デバッガーが Natvis ファイルを .pdb から読み込みます。 .natvis ファイルが .pdb に含まれないようにするには、 **[ソリューション エクスプローラー]** で .natvis ファイルを右クリックして、 **[構成プロパティ]** ウィンドウで **[ビルドから除外]** を **[はい]** に設定します。  

 Visual Studio を使用して Natvis ファイルを編集することをお勧めします。Visual Studio を使用すると、ファイルを保存時に、デバッグ中に行ったすべての変更が自動的に有効になります。 Intellisense から強化された編集エクスペリエンスを取得できます。  

 .pdb から読み込まれる Natvis ファイルは、pdb が参照するモジュールの型にのみ適用されます。 たとえば、Module1.pdb が `Test`という名前の型のエントリを定義する場合、このエントリは Module1.dll の **Test** クラスにのみ適用されます。 別のモジュールも **Test**という名前のクラスを定義する場合は、Module1.pdb の natvis エントリはこれに適用されません。  

## <a name="BKMK_natvis_location"></a> .natvis ファイルの配置  
 .natvis ファイルを、1 つの Visual Studio プロジェクトで作成する型にのみ適用する場合は、何も行う必要はありません。その .natvis は .pdb に含まれます。 <ph type="join"></ph>ただし、.natvis ファイルを複数のプロジェクトに適用したい場合は、natvis ファイルをユーザー ディレクトリまたはシステム ディレクトリに追加できます。  

 <ph type="join"></ph>.natvis ファイルを評価する順序は次のとおりです。  

1. デバッグ中の .pdb に埋め込まれた .natvis ファイル (読み込まれたプロジェクトに同じ名前のファイルが存在する場合を除く)  

2. 読み込まれた C++ プロジェクトまたはトップレベル ソリューション項目の一部である .natvis ファイル。 これには、クラス ライブラリなど、読み込まれたすべての C++ プロジェクトが含まれますが、他の言語のプロジェクトは含まれません (例: C# プロジェクトから .natvis ファイルを読み込むことはできません)。 実行可能プロジェクトでは、.pdb に既に存在しない .natvis ファイルをホストするにはソリューション項目を使用する必要があります。使用可能な C++ プロジェクトがないためです。  

3. ユーザー固有の natvis ディレクトリ ( **%USERPROFILE%\My Documents\Visual Studio 2015\Visualizers**)。  

4. システム全体の Natvis ディレクトリ ( **%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers**)。 <ph type="join"></ph>これは Visual Studio でインストールされる .natvis ファイルがコピーされる場所です。 管理者のアクセス許可がある場合には、このディレクトリに他のファイルも追加することができます。  

## <a name="modifying-natvis-files-while-debugging"></a><ph type="join"></ph>デバッグ中の .natvis ファイルの変更  
 <ph type="join"></ph>.natvis ファイルが含まれているプロジェクトのデバッグ中に、IDE で .natvis ファイルを変更することができます。 IDE で natvis ファイルを開き (デバッグ時に使用する Visual Studio の同じインスタンスを使用)、変更後、保存します。 ファイルを保存後すぐに、変更を反映するために **[ウォッチ]** と **[ローカル]** ウィンドウを更新する必要があります。 <ph type="join"></ph>IDE 以外で .natvis ファイルを変更する場合は、変更は自動的に有効になりません。 ウィンドウを更新するために、 **[ウォッチ]** ウィンドウで **.natvisreload** コマンドを評価できます。 これにより、デバッグ セッションを再起動しなくても変更を有効にできます。  

 デバッグしているソリューションに .natvis ファイルを追加したり、削除したりすることもできます。Visual Studio は、関連の視覚エフェクトを追加または削除します。  

 <ph type="join"></ph>.natvis ファイルが .pdb に埋め込まれている場合、デバッグ中に .natvis ファイルを変更することはできません。  

 .natvis ファイルを新しいバージョンにアップグレードする場合 (例: ファイルがソース管理にチェックインされていて、他の人がファイルに加えた最近の変更を取得する場合) には、 **.natvisreload** コマンドを使用します。 Visual Studio xml エディターを使用して、natvis ファイルを編集することをお勧めします。  

## <a name="BKMK_Expressions_and_formatting"></a> 式と書式  
 Natvis 視覚化では、C++ 式を使用して、表示するデータ項目を指定します。 「[コンテキスト演算子 (C++)](../debugger/context-operator-cpp.md)」で説明C++されているデバッガーの式の拡張と制限事項に加えて、次の相違点に注意する必要があります。  

- Natvis 式は、現在のスタック フレームではなく視覚化されるオブジェクトのコンテキストで評価されます。 たとえば、Natvis 式で `x` を使用している場合、これは視覚化されるオブジェクト内の `x` という名前のフィールドを参照します。現在実行中の関数内の `x` という名前のローカル変数を参照しません。 Natvis 式内のローカル変数にアクセスすることはできませんが、グローバル変数にはアクセスできます。  

- Natvis 式には関数の評価や副作用は許可されません。 つまり、関数呼び出しと代入演算子は無視されます。 [デバッガーの組み込み関数](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state) は、他の関数とは異なり副作用がないため、Natvis 式からは自由に呼び出すことができます。  

  変数ウィンドウに式を表示する方法を制御するには[、「」のC++ 「書式指定](../debugger/format-specifiers-in-cpp.md)子」の「[書式指定](../debugger/format-specifiers-in-cpp.md#BKMK_Visual_Studio_2012_format_specifiers)子」セクションで説明されている任意の書式指定子を使用できます。 Natvis によって内部的に仮想化エントリが使用されている場合 (ArrayItems の展開の `Size` 式など)、書式指定子は無視されることに注意してください。  

## <a name="natvis-views"></a>Natvis ビュー  
 Natvis ビューでは、さまざまな方法で任意の型を表示することができます。 たとえば、型の簡易ビューを提供する **simple** という名前のビューを定義できます。 たとえば、 `std::vector`の視覚化を次に示します。  

```xml  
<Type Name="std::vector&lt;*&gt;">  
    <DisplayString>{{ size={_Mylast - _Myfirst} }}</DisplayString>  
    <Expand>  
        <Item Name="[size]" ExcludeView="simple">_Mylast - _Myfirst</Item>  
        <Item Name="[capacity]" ExcludeView="simple">_Myend - _Myfirst</Item>  
        <ArrayItems>  
            <Size>_Mylast - _Myfirst</Size>  
            <ValuePointer>_Myfirst</ValuePointer>  
        </ArrayItems>  
    </Expand>  
</Type>  
```  

 `DisplayString` および `ArrayItems` の要素は、既定ビューと簡易ビューで使用されます。一方、 `[size]` および `[capacity]` の項目は簡易ビューから除外されます。 **,view** 書式指定子を使用して、別のビューを指定できます。 **[ウォッチ]** ウィンドウで、 **vec,view(simple)** として簡易ビューを指定します。  

 ![簡易ビューでのウォッチウィンドウ](../debugger/media/watch-simpleview.png "ウォッチ-SimpleView")  

## <a name="BKMK_Diagnosing_Natvis_errors"></a> Natvis エラーの診断  
 Natvis 診断を使用すると、構文のトラブルシューティングおよび解析エラーの検出が行えます。 デバッガーに視覚化エントリのエラーが発生すると、デバッガーはエラーを無視し、未加工の形式で型を表示するか、別の該当する視覚化を選択します。 特定の視覚化エントリが無視される理由を理解し、基になるエラーが何であるかを確認するために、 Natvis 診断の **[ツール] / [オプション] / [デバッグ] / [出力 ウィンドウ] / [Natvis 診断メッセージ (C++ のみ)]** オプションを有効にできます。 エラーは **[出力]** ウィンドウに表示されます。  

## <a name="BKMK_Syntax_reference"></a> Natvis 構文のリファレンス  

### <a name="BKMK_AutoVisualizer"></a> AutoVisualizer の要素  
 `AutoVisualizer`  要素は .natvis ファイルのルート ノードであり、名前空間 `xmlns:` 属性を含みます。  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">  
.  
.  
</AutoVisualizer>  
```  

### <a name="BKMK_Type"></a> 型の要素  
 基本的な型は、次のようになります。  

```xml  
<Type Name="[fully qualified type name]">  
  <DisplayString Condition="[Boolean expression]">[Display value]</DisplayString>  
  <Expand>  
    ...  
  </Expand>  
</Type>  

```  

 以下を指定します。  

1. この視覚化がどの型 ( `Type Name` 属性) に適用されるか。  

2. その型のオブジェクトの値がどのように表示されるか ( `DisplayString` 要素)。  

3. その型のメンバーが変数ウィンドウで展開されたときにどのように表示されるか ( `Expand` ノード)。  

   **テンプレート クラス** `Name` 要素の `Type` 属性には、アスタリスク ( `*` ) をワイルドカード文字として使用して、テンプレート クラス名を指定できます。  

```xml  
<Type Name="ATL::CAtlArray&lt;*&gt;">  
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>  
</Type>  

```  

 この例では、オブジェクトが `CAtlArray<int>` であっても `CAtlArray<float>`であっても、同じ視覚化が使用されます。 `CAtlArray<float>` に特定の視覚化エントリがある場合、そのエントリは汎用の視覚化エントリよりも優先されます。  

 マクロ $T1、$T2 などを使用することでテンプレート パラメーターを視覚化エントリで参照できることに注意してください。 これらのマクロの例を見つけるには、Visual Studio に付属の .natvis ファイルをご覧ください。  

#### <a name="BKMK_Visualizer_type_matching"></a> ビジュアライザーと型の対応付け  
 視覚化エントリの検証が失敗した場合は、次に使用可能な視覚化が使用されます。  

#### <a name="inheritable-attribute"></a>継承可能な属性  
 オプションの `Inheritable` 属性では、視覚エフェクトを基本型のみに適用するか、それとも基本型とすべての派生型に適用するかを指定することができます。 次の場合は、視覚エフェクトは `BaseClass` 型にのみ適用されます。  

```xml  
<Type Name="Namespace::BaseClass" Inheritable="true">  
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>  
</Type>  
```  

 `Inheritable` の既定値は `true` です。  

#### <a name="priority-attribute"></a>Priority 属性  
 `Priority` 属性には、定義が解析に失敗した場合、代替の定義が使用される順序を指定します。 `Priority` の有効な値は、 `Low`、 `MediumLow`、`Medium`、 `MediumHigh`、および `High`、であり、既定値は `Medium`です。  

 <ph type="join"></ph>Priority 属性は、同じ .natvis ファイル内での優先度を区別するためにのみ使用してください。異なるファイル間では使用してはいけません。  

 次の例では、まず 2015 STL と一致するエントリを解析します。この解析が失敗した場合、STL の 2013年バージョン用の別のエントリを使用します。  

```xml  
<!-- VC 2013 -->  
<Type Name="std::reference_wrapper&lt;*&gt;" Priority="MediumLow">  
     <DisplayString>{_Callee}</DisplayString>  
    <Expand>  
        <ExpandedItem>_Callee</ExpandedItem>  
    </Expand>  
</Type>  

<!-- VC 2015 -->  
<Type Name="std::reference_wrapper&lt;*&gt;">  
    <DisplayString>{*_Ptr}</DisplayString>  
    <Expand>  
        <Item Name="[ptr]">_Ptr</Item>  
    </Expand>  
</Type>  
```  

#### <a name="BKMK_Versioning"></a> Version 要素  
 `Version` 要素を使用して、視覚化の適用範囲を特定のモジュールとそれらのバージョンに制限すると、名前の競合を最小限に抑えることができ、型のバージョンごとに異なる視覚化を使用できます。 例 :  

```xml  
<Type Name="DirectUI::Border">  
  <Version Name="Windows.UI.Xaml.dll" Min="1.0" Max="1.5"/>  
  <DisplayString>{{Name = {*(m_pDO->m_pstrName)}}}</DisplayString>  
  <Expand>  
    <ExpandedItem>*(CBorder*)(m_pDO)</ExpandedItem>  
  </Expand>  
</Type>  
```  

 この例では、視覚化はバージョン 1.0 ～ 1.5 の `DirectUI::Border` で見つかる `Windows.UI.Xaml.dll` 型にのみ適用されます。 Version 要素を追加すると、視覚化の適用範囲が特定のモジュールとバージョンに制限され、不用意な対応付けは減りますが、さまざまなモジュールによって使用される共通のヘッダー ファイルで型を定義している場合、指定したモジュールにその型がないと、バージョン別の視覚化は適用されないことに注意してください。  

#### <a name="optional-attribute"></a>Optional 属性  
 `Optional` 属性はどのノードでも使用できます。 省略可能なノード内の部分式を解析できない場合、そのノードは無視されますが、Type 要素の残りの部分はまだ有効です。 次の型では、 `[State]` は省略不可能ですが、 `[Exception]` は省略可能です。  つまり、 `MyNamespace::MyClass` に _`M_exceptionHolder`という名前のフィールドが含まれている場合は `[State]` ノードおよび `[Exception]` ノードのどちらも依然として表示されますが、 `_M_exceptionHolder` がない場合は `[State]` ノードのみが表示されます。  

```xml  
<Type Name="MyNamespace::MyClass">  
    <Expand>  
      <Item Name="[State]">_M_State</Item>  
      <Item Name="[Exception]" Optional="true">_M_exceptionHolder</Item>  
    </Expand>  
</Type>  
```  

### <a name="BKMK_Condition_attribute"></a> Condition 属性  
 `Condition` 属性は必要に応じて多くの視覚化要素に使用でき、視覚化ルールを適用する条件を指定します。 Condition 属性内の式が `false`と解決された場合、その要素で指定した視覚化ルールは適用されません。 true と評価された場合、または `Condition` 属性が存在しない場合は、視覚化ルールが型に適用されます。 この属性により `if-else` ロジックを視覚化エントリに使用できます。 たとえば次の視覚化では、スマート ポインター型に 2 つの `DisplayString` 要素があります。  

```xml  
<Type Name="std::auto_ptr&lt;*&gt;">  
  <DisplayString Condition="_Myptr == 0">empty</DisplayString>  
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>  
  <Expand>  
    <ExpandedItem>_Myptr</ExpandedItem>  
  </Expand>  
</Type>  

```  

 `_Myptr` メンバーが `null`である場合、最初の `DisplayString` 要素の条件は `true`と解決され、フォームが表示されます。 `_Myptr` メンバーが `null`でない場合、この条件は `false`になり、2 番目の `DisplayString` 要素が表示されます。  

### <a name="includeview-and-excludeview-attributes"></a>IncludeView および ExcludeView 属性  
 これらの属性は、別のビューに表示される、または表示されない要素を指定します。 たとえば、 `std::vector`のNatvis 仕様を次のように指定します。  

```xml  
<Type Name="std::vector&lt;*&gt;">  
    <DisplayString>{{ size={_Mylast - _Myfirst} }}</DisplayString>  
    <Expand>  
        <Item Name="[size]" ExcludeView="simple">_Mylast - _Myfirst</Item>  
        <Item Name="[capacity]" ExcludeView="simple">_Myend - _Myfirst</Item>  
        <ArrayItems>  
            <Size>_Mylast - _Myfirst</Size>  
            <ValuePointer>_Myfirst</ValuePointer>  
        </ArrayItems>  
    </Expand>  
</Type>  
```  

 簡易ビューでは、[size] と [capacity] の項目は表示されません。 `IncludeView="simple"` の代わりに `ExcludeView`が使用されていた場合、 `[size]` と `[capacity]` の項目は既定ビューではなく、簡易ビューで表示されます。  

 `IncludeView` と `ExcludeView` の属性は型だけでなく個々のメンバーにも使用できます。  

### <a name="BKMK_DisplayString"></a> DisplayString  
 `DisplayString` 要素は、変数の値として表示される文字列を指定します。 この要素には、任意の文字列を式と組み合わせて使用できます。 中かっこ内のすべてのものは式として解釈されます。 たとえば、次のような `DisplayString` エントリがあるとします。  

```xml  
<Type Name="CPoint">  
  <DisplayString>{{x={x} y={y}}}</DisplayString>   
</Type>  

```  

 `CPoint` 型の変数は次のように表示されます。  

 ![DisplayString 要素の使用](../debugger/media/dbg-natvis-cpoint-displaystring.png "DBG_NATVIS_CPoint_DisplayString")  

 `DisplayString` 式では、 `x` と `y`は `CPoint`のメンバーであり、中かっこ内にあるため、それらの値は評価されます。 この式では、二重中かっこ ( `{{` または `}}` ) を使用して中かっこをエスケープする方法も示しています。  

> [!NOTE]
> `DisplayString` 要素でのみ、任意の文字列と中かっこ構文を使用できます。 その他のすべての視覚化要素では、デバッガーによって評価される式しか使用できません。  

### <a name="BKMK_StringView"></a> StringView  
 `StringView` 要素は、値が組み込みテキスト ビジュアライザーに渡される式を定義します。 たとえば、 `ATL::CStringT` に次のような視覚化があるとします。  

```xml  
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">  
  <DisplayString>{m_pszData,su}</DisplayString>  
</Type>  

```  

 `CStringT` オブジェクトは次のように表示されます。  

 ![CStringT DisplayString 要素](../debugger/media/dbg-natvis-displaystring-cstringt.png "DBG_NATVIS_DisplayString_CStringT")  

 視覚化により `CStringT` オブジェクトは変数ウィンドウに次のように表示されます。  

 `StringView` 要素を追加して、この値がテキスト ビジュアライザーによって表示できることをデバッガーに指示します。  

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">  
  <DisplayString>{m_pszData,su}</DisplayString>  
  <StringView>m_pszData,su</StringView>  
</Type>  
```  

 次に示している値の横に表示されている虫眼鏡のアイコンに注目してください。 このアイコンをクリックするとテキスト ビジュアライザーが起動され、 `m_pszData` が参照する文字列が表示されます。  

 ![StringView ビジュアライザーを使用した CStringT データ](../debugger/media/dbg-natvis-stringview-cstringt.png "DBG_NATVIS_StringView_CStringT")  

> [!NOTE]
> `{m_pszData,su}` 式に、値を Unicode 文字列として表示する C++ 書式指定子 `su` が含まれていることに注意してください。 詳細については、「 [Format Specifiers in C++](../debugger/format-specifiers-in-cpp.md) 」を参照してください。  

### <a name="BKMK_Expand"></a> Expand  
 `Expand` ノードを使用すると、視覚化された型の子が変数ウィンドウでどのように展開されるかをカスタマイズできます。 このノードでは、子要素を定義する子ノードのリストを使用できます。  

 `Expand` ノードは省略可能です。  

- 視覚化エントリで `Expand` ノードを指定しない場合、Visual Studio の既定の展開規則が使用されます。  

- `Expand` ノードで下位に子ノードを指定しない場合、型はデバッガー ウィンドウで展開されません。  

#### <a name="BKMK_Item_expansion"></a> Item の展開  
 `Item` 要素は、 `Expand` ノードに使用される最も基本的で一般的な要素です。 `Item` は 1 つの子要素を定義します。 たとえば、 `CRect` クラスに `top`、 `left`、 `right`、および `bottom` フィールドがあり、次の視覚化エントリがあるとします。  

```xml  
<Type Name="CRect">  
  <DisplayString>{{top={top} bottom={bottom} left={left} right={right}}}</DisplayString>  
  <Expand>  
    <Item Name="Width">right - left</Item>  
    <Item Name="Height">bottom - top</Item>  
  </Expand>  
</Type>  

```  

 `CRect` 型は次のようになります。  

 ![項目要素の展開を含む CRect](../debugger/media/dbg-natvis-expand-item-crect1.png "DBG_NATVIS_Expand_Item_CRect1")  

 `Width` および `Height` 要素で指定した式が評価され、値の列に表示されています。 `[Raw View]` ノードは、カスタム展開が使用されるたびに、デバッガーによって自動的に作成されます。 前に示したスクリーンショットでこのノードは展開されています。オブジェクトの未加工のビューと視覚化がどのように異なるかがわかります。 Visual Studio の既定の展開では、基底クラスのサブツリーが作成され、基底クラスのすべてのデータ メンバーが子として一覧表示されます。  

> [!NOTE]
> Item 要素の展開により複合型が参照される場合は、 `Item` ノード自体が展開可能です。  

#### <a name="BKMK_ArrayItems_expansion"></a> Size  
 `ArrayItems` ノードを使用すると、Visual Studio デバッガーによって型が配列として解釈され、その個々の要素が表示されるようになります。 `std::vector` の視覚化は良い使用例です。  

```xml  
<Type Name="std::vector&lt;*&gt;">  
  <DisplayString>{{size = {_Mylast - _Myfirst}}}</DisplayString>  
  <Expand>  
    <Item Name="[size]">_Mylast - _Myfirst</Item>  
    <Item Name="[capacity]">(_Myend - _Myfirst)</Item>  
    <ArrayItems>  
      <Size>_Mylast - _Myfirst</Size>  
      <ValuePointer>_Myfirst</ValuePointer>  
    </ArrayItems>  
  </Expand>  
</Type>  

```  

 `std::vector` は、変数ウィンドウで展開されると、その個々の要素が表示されます。  

 ![ArrayItems の展開を使用する std:: vector](../debugger/media/dbg-natvis-expand-arrayitems-stdvector.png "DBG_NATVIS_Expand_ArrayItems_StdVector")  

 少なくとも、 `ArrayItems` ノードには次の式が必要です。  

1. デバッガーが配列の長さを解釈するための `Size` 式 (整数に評価されることが必要)  

2. 最初の要素を参照する `ValuePointer` 式 ( `void*`でない要素型のポインターであることが必要)  

   配列の既定の下限値は 0 です。 この値は `LowerBound` 要素を使用してオーバーライドできます (例については Visual Studio に付属の .natvis ファイルを参照)。  

   `[]` 展開とともに `ArrayItems` 演算子を使用できるようになりました ( `vector[i]`など)。 [] 演算子は、型自体がこの演算子を許可しない場合 (たとえば `ArrayItems` ) であっても、 `IndexListItems`または `CATLArray`を使用する 1 次元配列の視覚エフェクトで使用できます。  

   多次元配列を指定することもできます。 その場合、デバッガーでは、子要素を適切に表示するために、次のように若干追加の情報が必要になります。  

```xml  
<Type Name="Concurrency::array&lt;*,*&gt;">  
  <DisplayString>extent = {_M_extent}</DisplayString>  
  <Expand>  
    <Item Name="extent">_M_extent</Item>  
    <ArrayItems Condition="_M_buffer_descriptor._M_data_ptr != 0">  
      <Direction>Forward</Direction>  
      <Rank>$T2</Rank>  
      <Size>_M_extent._M_base[$i]</Size>  
      <ValuePointer>($T1*) _M_buffer_descriptor._M_data_ptr</ValuePointer>  
    </ArrayItems>  
  </Expand>  
</Type>  

```  

 `Direction` は、配列が行優先であるか列優先であるかを指定します。 `Rank` は配列のランクを指定します。 `Size` 要素は暗黙の `$i` パラメーターを受け取ります。このパラメーターは次元のインデックスに置き換えられて、その次元の配列の長さが特定されます。 前の例では、式 `_M_extent.M_base[0]` で 0 次元の長さ、 `_M_extent._M_base[1]` で 1 次元の長さが特定されます。  

 ここでは、2 次元の `Concurrency::array` オブジェクトがデバッガーでどのように表示されるかを示しています。  

 ![ArrayItems の展開を含む2次元配列](../debugger/media/dbg-natvis-expand-arrayitems-2d.png "DBG_NATVIS_Expand_ArrayItems_2D")  

#### <a name="BKMK_IndexListItems_expansion"></a> IndexListItems の展開  
 配列要素が連続してメモリに配置されている場合にのみ、 `ArrayItems` 展開を使用することができます。 デバッガーは、次の要素を取得するために、ポインターを現在の要素までインクリメントするだけです。 値ノードのインデックスを操作する必要がある場合に対応するには、 `IndexListItems` ノードを使用できます。 ここでは、 `IndexListItems` ノードを使用した視覚化を示しています。  

```xml  
<Type Name="Concurrency::multi_link_registry&lt;*&gt;">  
  <DisplayString>{{size = {_M_vector._M_index}}}</DisplayString>  
  <Expand>  
    <Item Name="[size]">_M_vector._M_index</Item>  
    <IndexListItems>  
      <Size>_M_vector._M_index</Size>  
      <ValueNode>*(_M_vector._M_array[$i])</ValueNode>  
    </IndexListItems>  
  </Expand>  
</Type>  

```  

 `[]` 展開とともに `IndexListItems` 演算子を使用できるようになりました ( `vector[i]`など)。 `[]` 演算子は、型自体がこの演算子を許可しない場合 (たとえば `ArrayItems` ) であっても、 `IndexListItems`または `CATLArray`を使用する 1 次元配列の視覚エフェクトで使用できます。  

 `ArrayItems` と `IndexListItems` の唯一の違いは、 `ValueNode` で暗黙の<sup>パラメーターを使用して i</sup>`$i` 番目の要素を完全に表現していることです。  

#### <a name="BKMK_LinkedListItems_expansion"></a> LinkedListItems の展開  
 視覚化された型がリンク リストを表す場合、デバッガーは `LinkedListItems` ノードを使用してその子を表示できます。 ここでは、この機能を使用した `CAtlList` 型の視覚化を示しています。  

```xml  
<Type Name="ATL::CAtlList&lt;*,*&gt;">  
  <DisplayString>{{Count = {m_nElements}}}</DisplayString>  
  <Expand>  
    <Item Name="Count">m_nElements</Item>  
    <LinkedListItems>  
      <Size>m_nElements</Size>  
      <HeadPointer>m_pHead</HeadPointer>  
      <NextPointer>m_pNext</NextPointer>  
      <ValueNode>m_element</ValueNode>  
    </LinkedListItems>  
  </Expand>  
</Type>  

```  

 `Size` 要素はリストの長さを参照します。 `HeadPointer` は最初の要素を参照し、 `NextPointer` は次の要素を参照し、 `ValueNode` は項目の値を参照します。  

- `NextPointer` および `ValueNode` 式は、親リストの型ではなく、リンク リスト ノード要素のコンテキストで評価されます。 前の例で、 `CAtlList` の `CNode` クラス ( `atlcoll.h`内) はリンク リストのノードを表しています。 `m_pNext` と `m_element` は、 `CNode` クラスではなく `CAtlList` クラスのフィールドです。  

- `ValueNode` は、空にするか `this` を指定すると、リンク リスト ノード自体を参照できます。  

#### <a name="customlistitems-expansion"></a>CustomListItems 展開  
 `CustomListItems` 展開を使用して、ハッシュ テーブルなどのデータ構造を走査する際にカスタム ロジックを記述することができます。 評価すべきものがすべて C++ の式を使用して表現されるデータ構造を視覚化するには、 `CustomListItems` を使用する必要があります。ただし、これは `ArrayItems`, `TreeItems`、または `LinkedListItems.`にあまり適合しません。  

 CAtlMap のビジュアライザーは、 `CustomListItems` が適している場面を示す良い例です。  

```xml  
<Type Name="ATL::CAtlMap&lt;*,*,*,*&gt;">  
    <AlternativeType Name="ATL::CMapToInterface&lt;*,*,*&gt;"/>  
    <AlternativeType Name="ATL::CMapToAutoPtr&lt;*,*,*&gt;"/>  
    <DisplayString>{{Count = {m_nElements}}}</DisplayString>  
    <Expand>  
      <CustomListItems MaxItemsPerView="5000" ExcludeView="Test">  
        <Variable Name="iBucket" InitialValue="-1" />  
        <Variable Name="pBucket" InitialValue="m_ppBins == nullptr ? nullptr : *m_ppBins" />  
        <Variable Name="iBucketIncrement" InitialValue="-1" />  

        <Size>m_nElements</Size>  
        <Exec>pBucket = nullptr</Exec>  
        <Loop>  
          <If Condition="pBucket == nullptr">  
            <Exec>iBucket++</Exec>  
            <Exec>iBucketIncrement = __findnonnull(m_ppBins + iBucket, m_nBins - iBucket)</Exec>  
            <Break Condition="iBucketIncrement == -1" />  
            <Exec>iBucket += iBucketIncrement</Exec>  
            <Exec>pBucket = m_ppBins[iBucket]</Exec>  
          </If>  
          <Item>pBucket,na</Item>  
          <Exec>pBucket = pBucket->m_pNext</Exec>  
        </Loop>  
      </CustomListItems>  
    </Expand>  
</Type>  
```  

#### <a name="BKMK_TreeItems_expansion"></a> TreeItems の展開  
 視覚化された型がツリーを表す場合、デバッガーはツリーをたどり、 `TreeItems` ノードを使用してその子を表示できます。 ここでは、この機能を使用した `std::map` 型の視覚化を示しています。  

```xml  
<Type Name="std::map&lt;*&gt;">  
  <DisplayString>{{size = {_Mysize}}}</DisplayString>  
  <Expand>  
    <Item Name="[size]">_Mysize</Item>  
    <Item Name="[comp]">comp</Item>  
    <TreeItems>  
      <Size>_Mysize</Size>  
      <HeadPointer>_Myhead->_Parent</HeadPointer>  
      <LeftPointer>_Left</LeftPointer>  
      <RightPointer>_Right</RightPointer>  
      <ValueNode Condition="!((bool)_Isnil)">_Myval</ValueNode>  
    </TreeItems>  
  </Expand>  
</Type>  

```  

 構文は `LinkedListItems` ノードとほとんど同じです。 `LeftPointer`、 `RightPointer`、 `ValueNode` は、ツリー ノード クラスのコンテキストで評価されます。 `ValueNode` は、空のままにするか `this` を指定すると、ツリー ノード自体を参照できます。  

#### <a name="BKMK_ExpandedItem_expansion"></a> ExpandedItem の展開  
 `ExpandedItem` 要素を使用すると、基底クラスまたはデータ メンバーのプロパティを視覚化された型の子であるかのように表示することで、子の集約ビューを作成できます。 指定した式が評価され、その結果の子ノードが、視覚化された型の子リストに追加されます。 たとえば、スマートポインター型 `auto_ptr<vector<int>>` があるとします。通常は次のように表示されます。  

 ![自動&#95;ptr&#60;ベクター&#60;int&#62; &#62;の既定の展開](../debugger/media/dbg-natvis-expand-expandeditem-default.png "DBG_NATVIS_Expand_ExpandedItem_Default")  

 vector の値を表示するには、変数ウィンドウで _Myptr メンバーを通って 2 階層下位にたどる必要があります。 `ExpandedItem` 要素を追加することで、階層から `_Myptr` 変数を排除し、vector の要素を直接表示できます。  

```xml  
<Type Name="std::auto_ptr&lt;*&gt;">  
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>  
  <Expand>  
    <ExpandedItem>_Myptr</ExpandedItem>  
  </Expand>  
</Type>  

```  

 ![自動&#95;ptr&#60;ベクター&#60;int&#62; &#62; ExpandedItem 拡張](../debugger/media/dbg-natvis-expand-expandeditem-visualized.png "DBG_NATVIS_Expand_ExpandedItem_Visualized")  

 次の例では、基底クラスのプロパティを派生クラスに集約する方法を示しています。 `CPanel` クラスが `CFrameworkElement`から派生しているとします。 基底クラス `CFrameworkElement` のプロパティを繰り返す代わりに、 `ExpandedItem` ノードでは、これらのプロパティを `CPanel` クラスの子リストに追加できます。 派生クラスの視覚化の対応付けを無効にする **nd** 書式指定子がここで必要になります。 この書式指定子を使用しない場合、式 `*(CFrameworkElement*)this` により `CPanel` の視覚化が再び適用されることになります。型の対応付けルールに一致する既定の視覚化が最適と解釈されるためです。 **nd** 書式指定子を使用して、基底クラスの視覚化を適用するように、または基底クラスに視覚化がない場合は基底クラスの既定の展開を適用するように、デバッガーに指示します。  

```xml  
<Type Name="CPanel">  
  <DisplayString>{{Name = {*(m_pstrName)}}}</DisplayString>  
  <Expand>  
    <Item Name="IsItemsHost">(bool)m_bItemsHost</Item>  
    <ExpandedItem>*(CFrameworkElement*)this,nd</ExpandedItem>  
  </Expand>  
</Type>  

```  

#### <a name="BKMK_Synthetic_Item_expansion"></a> Synthetic Item の展開  
 `ExpandedItem` 要素は階層を排除することでデータ ビューを平坦化しますが、 `Synthetic` ノードはその反対のことを行います。 このノードを使用すると、意図的な子要素 (式の結果ではない子要素) を作成できます。 この子要素には、その要素自体の子要素を格納できます。 次の例では、 `Concurrency::array` 型の視覚化で `Synthetic` ノードを使用して、診断メッセージをユーザーに表示しています。  

```xml  
<Type Name="Concurrency::array&lt;*,*&gt;">  
  <DisplayString>extent = {_M_extent}</DisplayString>  
  <Expand>  
    <Item Name="extent" Condition="_M_buffer_descriptor._M_data_ptr == 0">_M_extent</Item>  
    <ArrayItems Condition="_M_buffer_descriptor._M_data_ptr != 0">  
      <Rank>$T2</Rank>  
      <Size>_M_extent._M_base[$i]</Size>  
      <ValuePointer>($T1*) _M_buffer_descriptor._M_data_ptr</ValuePointer>  
    </ArrayItems>  
    <Synthetic Name="Array" Condition="_M_buffer_descriptor._M_data_ptr == 0">  
      <DisplayString>Array members can be viewed only under the GPU debugger</DisplayString>  
    </Synthetic>  
  </Expand>  
</Type>  

```  

 ![Sythentic 要素を使用した Concurrency:: Array 展開](../debugger/media/dbg-natvis-expand-synthetic.png "DBG_NATVIS_Expand_Synthetic")  

### <a name="BKMK_HResult"></a> HResult  
 `HResult` 要素を使用すると、デバッガー ウィンドウに表示される HRESULT に関する情報をカスタマイズできます。 `HRValue` 要素には、カスタマイズする HRESULT の 32 ビット値を格納する必要があります。 `HRDescription` 要素には、デバッガーに表示される情報を格納します。  

```  

<HResult Name="MY_E_COLLECTION_NOELEMENTS">  
  <HRValue>0xABC0123</HRValue>  
  <HRDescription>No elements in the collection.</HRDescription>  
</HResult>  
```  

### <a name="BKMK_UIVisualizer"></a> UIVisualizer  
 `UIVisualizer` 要素は、グラフィカル ビジュアライザー プラグインをデバッガーに登録するために使用します。 グラフィカル ビジュアライザー プラグインは、ダイアログ ボックスまたはその他のインターフェイスを作成して、データ型に適した方法で変数またはオブジェクトを表示します。 ビジュアライザー プラグインは [VSPackage](../extensibility/internals/vspackages.md) として作成し、デバッガーによって使用可能なサービスを公開する必要があります。 .natvis ファイルには、プラグインに関する登録情報 (その名前、公開されるサービスの GUID、視覚化できる型など) が格納されます。  

 ここでは、UIVisualizer 要素の例を示しています。  

```xml  

<?xml version="1.0" encoding="utf-8"?>  
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">  
    <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}"   
        Id="1" MenuName="Vector Visualizer"/>  
    <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}"   
        Id="2" MenuName="List Visualizer"/>  
.  
.  
</AutoVisualizer>  
```  

 デバッガーが配列の長さを解釈するための `UIVisualizer` は、 `ServiceId` - `Id` という属性のペアによって識別されます。 `ServiceId` は、ビジュアライザー パッケージによって公開されるサービスの GUID です。 `Id` は、サービスが複数のビジュアライザーを提供する場合にビジュアライザーを区別するために使用できる一意の識別子です。 前の例では、同じビジュアライザー サービスに 2 つのビジュアライザーが用意されています。  

 `MenuName` 属性は、デバッガーの変数ウィンドウで虫眼鏡のアイコンの横にあるドロップダウン メニューを開いたときに、ビジュアライザーの名前として表示されます。  

 ![UIVisualizer メニューのショートカットメニュー](../debugger/media/dbg-natvis-vectorvisualizer.png "DBG_NATVIS_VectorVisualizer")  

 .natvis ファイルで定義した各型には、型を表示できる UI ビジュアライザーのリストを明示的に指定する必要があります。 デバッガーは、型エントリ内のビジュアライザーの参照を使用して、型と登録されたビジュアライザーとを対応付けます。 たとえば、次に示している `std::vector` の型エントリは、前の例での UIVisualizer を参照しています。  

```xml
<Type Name="std::vector&lt;int,*&gt;">  
  <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}" Id="1" />  
</Type>  
```  

 メモリ内のビットマップの表示に使用するイメージ ウォッチ拡張機能の UIVisualizer の例については、「 [ImageWatch](https://visualstudiogallery.msdn.microsoft.com/e682d542-7ef3-402c-b857-bbfba714f78d)」をご覧ください。  

### <a name="customvisualizer-element"></a>CustomVisualizer 要素  
 `CustomVisualizer` は、Visual Studio で実行されるコードの中で、視覚エフェクトを制御するために書くことができる VSIX 拡張機能を指定する機能拡張ポイントです。 VSIX 拡張機能の記述方法について詳しくは、「 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)」をご覧ください。 カスタム ビジュアライザーの記述は、XML natvis 定義の記述よりもはるかに多く作業が必要になりますが、natvis がサポートする事柄としない事柄についての制約がありません。 カスタム ビジュアライザーを使用すると、デバッガーの拡張性 API の全セットにアクセスできます。これらの API は、デバッグ対象のプロセスの照会および変更、または Visual Studio の他の部分との通信に使用できます。  

 CustomVisualizer 要素で `Condition`、 `IncludeView`、および `ExcludeView` 属性を使用できます。
