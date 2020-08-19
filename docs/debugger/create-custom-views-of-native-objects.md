---
title: C++ オブジェクトのカスタム ビューを作成する
description: Natvis フレームワークを使用して、Visual Studio のデバッガーでのネイティブ型の表示方法をカスタマイズします
ms.date: 03/02/2020
ms.topic: how-to
f1_keywords:
- natvis
dev_langs:
- C++
ms.assetid: 2d9a177a-e14b-404f-a6af-49498eff0bd7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 37bfd1ab57fd0e37f32a55d5bfc3787cb0c0cbd2
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88248050"
---
# <a name="create-custom-views-of-c-objects-in-the-debugger-using-the-natvis-framework"></a>Natvis フレームワークを使用してデバッガーで C++ オブジェクトのカスタム ビューを作成する

Visual Studio の *Natvis* フレームワークを使用すると、 **[ローカル]** ウィンドウ、 **[ウォッチ]** ウィンドウ、**データヒント**など、デバッガーの変数ウィンドウでのネイティブ型の表示方法をカスタマイズできます。 Natvis の視覚化は、作成した型をデバッグ中により見やすくするのに役立ちます。

Natvis は、以前のバージョンの Visual Studio で使用されていた *autoexp.dat* ファイルを、XML 構文、より高度な診断、バージョン管理、複数ファイルのサポートで置き換えるものです。

> [!NOTE]
> Natvis のカスタマイズは、クラスと構造体では機能しますが、typedef では使用できません。

## <a name="natvis-visualizations"></a><a name="BKMK_Why_create_visualizations_"></a>Natvis の視覚化

Natvis フレームワークを使用して、自分で作成した型の視覚化ルールを作成すると、開発者がデバッグ中に型を確認しやすくなります。

たとえば、次の図では、カスタム視覚化が適用されていないデバッガー ウィンドウに表示された [Windows::UI::Xaml::Controls::TextBox](/uwp/api/Windows.UI.Xaml.Controls.TextBox) 型の変数が示されています。

![TextBox の既定の視覚化](../debugger/media/dbg_natvis_textbox_default.png "TextBox の既定の視覚表現")

強調表示された行には `Text` クラスの `TextBox` プロパティが示されています。 複雑なクラス階層では、このプロパティを見つけるのが困難になります。 デバッガーではカスタム文字列型を解釈する方法がわからないため、TextBox に保持されている文字列を見ることができません。

同じ `TextBox` でも、Natvis のカスタム視覚化ルールを適用すると、変数ウィンドウで非常に見やすくなります。 クラスの重要なメンバーがまとめて表示され、カスタム文字列型の基になる文字列値がデバッガーに表示されます。

![ビジュアライザーを使用した TextBox のデータ](../debugger/media/dbg_natvis_textbox_visualizer.png "ビジュアライザーを使用した TextBox データ")

## <a name="use-natvis-files-in-c-projects"></a><a name="BKMK_Using_Natvis_files"></a>C++ プロジェクトで .natvis ファイルを使用する

Natvis では、視覚化ルールを指定するために *.natvis* ファイルを使用します。 *.natvis* ファイルは、 *.natvis* という拡張子が付いた XML ファイルです。 Natvis のスキーマは、 *%VSINSTALLDIR%\Xml\Schemas\natvis.xsd* で定義されています。

*.natvis* ファイルの基本構造は、視覚化エントリを表す 1 つ以上の `Type` 要素です。 各 `Type` 要素の完全修飾名は、`Name` 属性で指定されます。

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

Visual Studio の *%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers* フォルダーには、 *.natvis* ファイルがいくつか用意されています。 これらのファイルに多くの一般的な型に対する視覚化ルールが含まれており、新しい型の視覚化を記述するときに例として使用できます。

### <a name="add-a-natvis-file-to-a-c-project"></a>.natvis ファイルを C++ プロジェクトに追加する

任意の C++ プロジェクトに *.natvis* ファイルを追加できます。

**新しい *.natvis* ファイルを追加するには:**

1. **ソリューション エクスプローラー**で C++ プロジェクト ノードを選択し、 **[プロジェクト]**  >  **[新しい項目の追加]** を選択するか、プロジェクトを右クリックして **[追加]**  >  **[新しい項目]** を選択します。

1. **[新しい項目の追加]** ダイアログ ボックスで、 **[Visual C++]**  >  **[ユーティリティ]**  >  **[デバッガー視覚化ファイル (.natvis)]** を選択します。

1. ファイルの名前を指定し、 **[追加]** を選択します。

   新しいファイルが**ソリューション エクスプローラー**に追加され、Visual Studio のドキュメント ペインに表示されます。

Visual Studio デバッガーによって、 *.natvis* ファイルが C++ プロジェクトに自動的に読み込まれ、既定では、プロジェクトのビルド時に *.pdb* ファイルにも組み込まれます。 ビルドされたアプリをデバッグする場合、プロジェクトを開かなくても、デバッガーによって *.natvis* ファイルが *.pdb* から読み込まれます。 *.natvis* ファイルを *.pdb* に含めたくない場合は、ビルドされる *.pdb* ファイルから除外できます。

***.natvis* ファイルを *.pdb* から除外するには:**

1. **ソリューション エクスプローラー**で *.natvis* ファイルを選択し、 **[プロパティ]** アイコンを選択するか、ファイルを右クリックして **[プロパティ]** を選択します。

1. **[ビルドから除外]** の横にある矢印をドロップダウンして **[はい]** を選択し、 **[OK]** を選択します。

>[!NOTE]
>実行可能プロジェクトをデバッグするときは、使用可能な C++ プロジェクトがないため、ソリューション項目を使用して、 *.pdb* に含まれない *.natvis* ファイルを追加します。

>[!NOTE]
>*.pdb* から読み込まれた Natvis ルールは、 *.pdb* で参照されているモジュールの型に対してのみ適用されます。 たとえば、*Module1.pdb* に `Test` という名前の型に対する Natvis エントリがある場合、それは *Module1.dll* の `Test` クラスにのみ適用されます。 別のモジュールでも `Test` という名前のクラスが定義されている場合、*Module1.pdb* の Natvis エントリはそれには適用されません。

**VSIX パッケージを使用して *.natvis* ファイルをインストールして登録するには:**

VSIX パッケージで *.natvis* ファイルをインストールして登録することができます。 インストールされている場所に関係なく、登録されているすべての *.natvis* ファイルがデバッグ時に自動的に取得されます。

1. VSIX パッケージに *.natvis* ファイルを含めます。 たとえば、次のようなプロジェクト ファイルがあるとします。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ToolsVersion="14.0">
     <ItemGroup>
       <VSIXSourceItem Include="Visualizer.natvis" />
     </ItemGroup>
   </Project>
   ```

2. *source.extension.vsixmanifest* ファイルで *.natvis* ファイルを登録します。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
     <Assets>
       <Asset Type="NativeVisualizer" Path="Visualizer.natvis"  />
     </Assets>
   </PackageManifest>
   ```

### <a name="natvis-file-locations"></a><a name="BKMK_natvis_location"></a> Natvis ファイルの場所

*.natvis* ファイルを複数のプロジェクトに適用する場合は、ファイルをユーザー ディレクトリまたはシステム ディレクトリに追加できます。

*.natvis* ファイルは、次の順序で評価されます。

1. デバッグ中の *.pdb* に埋め込まれている *.natvis* ファイル (読み込まれたプロジェクトに同じ名前のファイルが存在する場合を除く)。

2. 読み込まれた C++ プロジェクトまたはトップレベル ソリューションに含まれる *.natvis* ファイル。 このグループには、クラス ライブラリなどの読み込まれた C++ プロジェクトがすべて含まれますが、他の言語のプロジェクトは含まれません。

3. VSIX パッケージによってインストールおよび登録された *.natvis* ファイル。

::: moniker range="vs-2017"

4. ユーザー固有の Natvis ディレクトリ ( *%USERPROFILE%\Documents\Visual Studio 2017\Visualizers*)。

::: moniker-end

::: moniker range=">= vs-2019"

4. ユーザー固有の Natvis ディレクトリ ( *%USERPROFILE%\Documents\Visual Studio 2019\Visualizers*)。

::: moniker-end

5. システム全体の Natvis ディレクトリ ( *%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers*)。 このディレクトリには、Visual Studio でインストールされた *.natvis* ファイルがあります。 管理者のアクセス許可がある場合は、このディレクトリにファイルを追加できます。

## <a name="modify-natvis-files-while-debugging"></a>デバッグ中に .natvis ファイルを変更する

プロジェクトのデバッグ中に、IDE でその *.natvis* ファイルを変更することができます。 デバッグに使用しているものと同じ Visual Studio のインスタンスでファイルを開き、変更して、保存します。 ファイルを保存するとすぐに、 **[ウォッチ]** ウィンドウと **[ローカル]** ウィンドウに変更が反映されます。

デバッグしているソリューションの *.natvis* ファイルを追加したり、削除したりすることもできます。Visual Studio により、関連する視覚化が追加または削除されます。

*.pdb* ファイルに埋め込まれている *.natvis* ファイルを、デバッグ中に更新することはできません。

Visual Studio の外部で *.natvis* ファイルを変更した場合、変更は自動的には有効になりません。 デバッガーのウィンドウを更新するには、 **[イミディエイト]** ウィンドウで **.natvisreload** コマンドを評価します。 その後は、デバッグ セッションを再度開始しなくても変更が有効になります。

また、 *.natvis* ファイルを新しいバージョンにアップグレードする場合も、 **.natvisreload** コマンドを使用します。 たとえば、 *.natvis* ファイルがソース管理にチェックインされていて、他のユーザーが最近行った変更を取得する場合などです。

## <a name="expressions-and-formatting"></a><a name="BKMK_Expressions_and_formatting"></a> 式と書式
Natvis 視覚化では、C++ 式を使用して、表示するデータ項目を指定します。 デバッガーでの C++ 式の拡張機能と制限 ([コンテキスト演算子 (C++)](../debugger/context-operator-cpp.md) に関するページを参照) に加えて、次の点に注意する必要があります。

- Natvis 式は、現在のスタック フレームではなく視覚化されるオブジェクトのコンテキストで評価されます。 たとえば、Natvis 式の `x` では、視覚化されているオブジェクト内の **x** という名前のフィールドが参照されるのであり、現在の関数内の **x** という名前のローカル変数ではありません。 Natvis 式内のローカル変数にアクセスすることはできませんが、グローバル変数にはアクセスできます。

- Natvis 式では、関数の評価や副作用は許可されません。 関数呼び出しと代入演算子は無視されます。 [デバッガーの組み込み関数](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state) は、他の関数とは異なり副作用がないため、Natvis 式からは自由に呼び出すことができます。

- 式の表示方法を制御するには、[C++ での書式指定子](format-specifiers-in-cpp.md#BKMK_Visual_Studio_2012_format_specifiers)に関するページで説明されている書式指定子のいずれかを使用できます。 書式指定子は、エントリが Natvis によって内部的に使用されるときは無視されます。たとえば、[ArrayItems の展開](../debugger/create-custom-views-of-native-objects.md#BKMK_ArrayItems_expansion)での `Size` 式のような場合です。

## <a name="natvis-views"></a>Natvis ビュー

異なる Natvis ビューを定義して、さまざまな方法で型を表示できます。 たとえば、`simple` という名前の簡易ビューを定義する `std::vector` の視覚化を次に示します。 `DisplayString` 要素と `ArrayItems` 要素は既定のビューと `simple` ビューに表示されますが、`[size]` 項目と `[capacity]` 項目は `simple` ビューには表示されません。

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

**[ウォッチ]** ウィンドウでは、 **,view** 書式指定子を使用して、別のビューを指定できます。 simple ビューは、**vec,view(simple)** と表示されます。

![simple ビューが含まれる [ウォッチ] ウィンドウ](../debugger/media/watch-simpleview.png "単純なビューを備えた [ウォッチ] ウィンドウ")

## <a name="natvis-errors"></a><a name="BKMK_Diagnosing_Natvis_errors"></a> Natvis のエラー

デバッガーでは、視覚化エントリで検出されたエラーは無視されます。 生の形式で型が表示されるか、別の適切な視覚化が選択されます。 Natvis 診断を使用して、デバッガーで視覚化エントリが無視された理由を理解し、基になっている構文と解析のエラーを確認することができます。

**Natvis 診断を有効にするには:**

- **[ツール]**  >  **[オプション]** (または **[デバッグ]**  >  **[オプション]** ) > **[デバッグ]**  >  **[出力ウィンドウ]** で、 **[Natvis 診断メッセージ (C++ のみ)]** を **[エラー]** 、 **[警告]** 、または **[詳細]** に設定して、 **[OK]** を選択します。

エラーは **[出力]** ウィンドウに表示されます。

## <a name="natvis-syntax-reference"></a><a name="BKMK_Syntax_reference"></a> Natvis 構文のリファレンス

### <a name="autovisualizer-element"></a><a name="BKMK_AutoVisualizer"></a> AutoVisualizer の要素
`AutoVisualizer` 要素は *.natvis* ファイルのルート ノードであり、名前空間 `xmlns:` 属性を含みます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">
.
.
</AutoVisualizer>
```

`AutoVisualizer` 要素では、[Type](#BKMK_Type)、[HResult](#BKMK_HResult)、[UIVisualizer](#BKMK_UIVisualizer)、[CustomVisualizer](#BKMK_CustomVisualizer) の子要素を使用できます。

### <a name="type-element"></a><a name="BKMK_Type"></a> Type 要素

基本的な `Type` は、次の例のようになります。

```xml
<Type Name="[fully qualified type name]">
  <DisplayString Condition="[Boolean expression]">[Display value]</DisplayString>
  <Expand>
    ...
  </Expand>
</Type>
```

 `Type` 要素では次のことを指定します。

1. その視覚化がどの型に対して適用されるか ( `Name` 属性)。

2. その型のオブジェクトの値がどのように表示されるか ( `DisplayString` 要素)。

3. ユーザーが変数ウィンドウで型を展開したとき、その型のメンバーをどのように表示するか (`Expand` ノード)。

#### <a name="templated-classes"></a>テンプレート クラス
`Type` 要素の `Name` 属性では、テンプレート クラス名に使用できるワイルドカード文字としてアスタリスク `*` を使用できます。

次の例では、オブジェクトが `CAtlArray<int>` であっても `CAtlArray<float>`であっても、同じ視覚化が使用されます。 `CAtlArray<float>` に固有の視覚化エントリがある場合、そのエントリは汎用のエントリより優先されます。

```xml
<Type Name="ATL::CAtlArray&lt;*&gt;">
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>
</Type>
```

マクロ $T1、$T2 などを使用することにより、視覚化エントリでテンプレート パラメーターを参照できます。 これらのマクロの例を見つけるには、Visual Studio に付属の *.natvis* ファイルをご覧ください。

#### <a name="visualizer-type-matching"></a><a name="BKMK_Visualizer_type_matching"></a> ビジュアライザーと型の対応付け
視覚化エントリの検証が失敗した場合は、次に使用可能な視覚化が使用されます。

#### <a name="inheritable-attribute"></a>継承可能な属性
オプションの `Inheritable` 属性では、視覚エフェクトを基本型のみに適用するか、それとも基本型とすべての派生型に適用するかを指定します。 `Inheritable` の既定値は `true`です。

次の例の視覚化は、`BaseClass` 型にのみ適用されます。

```xml
<Type Name="Namespace::BaseClass" Inheritable="false">
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>
</Type>
```

#### <a name="priority-attribute"></a>Priority 属性

オプションの `Priority` 属性では、定義が解析に失敗した場合、代替の定義が使用される順序を指定します。 `Priority` に指定できる値は、`Low`、`MediumLow`、`Medium`、`MediumHigh`、`High` です。 既定値は `Medium` です。 `Priority` 属性では、同じ *.natvis* ファイル内での優先順位のみが区別されます。

次の例では、2015 STL と一致するエントリが最初に解析されます。 その解析が失敗した場合、2013 バージョンの STL に対する代替エントリが使用されます。

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

### <a name="optional-attribute"></a>Optional 属性
`Optional` 属性は、任意のノードに配置できます。 オプションのノード内にある部分式の解析が失敗した場合、デバッガーではそのノードは無視されますが、残りの `Type` ルールは適用されます。 次の型では、 `[State]` は省略不可能ですが、 `[Exception]` は省略可能です。  `MyNamespace::MyClass` に _`M_exceptionHolder` という名前のフィールドがある場合は、`[State]` ノードと `[Exception]` ノードの両方が表示されますが、`_M_exceptionHolder` フィールドがない場合は、`[State]` ノードだけが表示されます。

```xml
<Type Name="MyNamespace::MyClass">
    <Expand>
      <Item Name="[State]">_M_State</Item>
      <Item Name="[Exception]" Optional="true">_M_exceptionHolder</Item>
    </Expand>
</Type>
```

### <a name="condition-attribute"></a><a name="BKMK_Condition_attribute"></a> Condition 属性

オプションの `Condition` 属性は多くの視覚化要素に使用でき、視覚化ルールを適用する条件を指定します。 Condition 属性内の式が `false` に解決された場合、視覚化ルールは適用されません。 `true` と評価された場合、または `Condition` 属性がない場合は、視覚化が適用されます。 この属性を、視覚化エントリの if-else ロジックとして使用できます。

たとえば、次の視覚化には、スマート ポインター型に対する 2 つの `DisplayString` 要素があります。 `_Myptr` メンバーが空のときは、最初の `DisplayString` 要素の条件が `true` と解決されるので、フォームが表示されます。 `_Myptr` メンバーが空でないときは、この条件は `false` と評価され、2 番目の `DisplayString` 要素が表示されます。

```xml
<Type Name="std::auto_ptr&lt;*&gt;">
  <DisplayString Condition="_Myptr == 0">empty</DisplayString>
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>
  <Expand>
    <ExpandedItem>_Myptr</ExpandedItem>
  </Expand>
</Type>
```

### <a name="includeview-and-excludeview-attributes"></a>IncludeView および ExcludeView 属性

`IncludeView` 属性と `ExcludeView` 属性では、特定のビューに表示する要素または表示しない要素を指定します。 たとえば、`std::vector` の次の Natvis 指定では、`simple` ビューには `[size]` 項目と `[capacity]` 項目は表示されません。

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

`IncludeView` 属性と `ExcludeView` 属性は、型と個々のメンバーで使用できます。

### <a name="version-element"></a><a name="BKMK_Versioning"></a> Version 要素
`Version` 要素では、視覚化エントリのスコープを、特定のモジュールとバージョンに指定します。 `Version` 要素を使用すると、名前の競合を回避し、偶発的な不一致を減らし、型の異なるバージョンに対して異なる視覚化を使用することができます。

異なるモジュールで使用される共通のヘッダー ファイルで型を定義する場合、バージョン管理された視覚化は、その型が指定したモジュールのバージョン内にある場合にのみ表示されます。

次の例では、視覚化はバージョン 1.0 から 1.5 の `DirectUI::Border` で見つかる `Windows.UI.Xaml.dll` 型にのみ適用されます。

```xml
<Type Name="DirectUI::Border">
  <Version Name="Windows.UI.Xaml.dll" Min="1.0" Max="1.5"/>
  <DisplayString>{{Name = {*(m_pDO->m_pstrName)}}}</DisplayString>
  <Expand>
    <ExpandedItem>*(CBorder*)(m_pDO)</ExpandedItem>
  </Expand>
</Type>
```

`Min` と `Max` の両方を指定する必要はありません。 これらはオプションの属性です。 ワイルドカード文字はサポートされていません。

`Name` 属性の形式は " *<ファイル名>.<拡張子>* " です (例: *hello.exe*、*some.dll*)。 パス名は使用できません。

### <a name="displaystring-element"></a><a name="BKMK_DisplayString"></a> DisplayString 要素
`DisplayString` 要素では、変数の値として表示する文字列を指定します。 この要素には、任意の文字列を式と組み合わせて使用できます。 中かっこ内のすべてのものは式として解釈されます。 たとえば、次のような `DisplayString` エントリがあるとします。

```xml
<Type Name="CPoint">
  <DisplayString>{{x={x} y={y}}}</DisplayString>
</Type>
```

これは、`CPoint` 型の変数が次の図のように表示されることを意味します。

 ![DisplayString 要素を使用する](../debugger/media/dbg_natvis_cpoint_displaystring.png "DisplayString 要素を使用する")

この `DisplayString` 式では、`CPoint` のメンバーである `x` と `y` が中かっこ内にあるため、それらの値が評価されます。 この例では、二重中かっこ (`{{` または `}}`) を使用して中かっこをエスケープする方法も示されています。

> [!NOTE]
> `DisplayString` 要素でのみ、任意の文字列と中かっこ構文を使用できます。 他のすべての視覚化要素では、デバッガーで評価できる式しか受け付けられません。

### <a name="stringview-element"></a><a name="BKMK_StringView"></a> StringView 要素

`StringView` 要素では、デバッガーで組み込みのテキスト ビジュアライザーに送信できる値を定義します。 たとえば、`ATL::CStringT` 型に対する次のような視覚化があるとします。

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">
  <DisplayString>{m_pszData,su}</DisplayString>
</Type>
```

`CStringT` オブジェクトは、次の例のような変数ウィンドウに表示されます。

![CStringT の DisplayString 要素](../debugger/media/dbg_natvis_displaystring_cstringt.png "CStringT DisplayString 要素")

`StringView` 要素を追加すると、その値をテキストの視覚化として表示できることがデバッガーに通知されます。

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">
  <DisplayString>{m_pszData,su}</DisplayString>
  <StringView>m_pszData,su</StringView>
</Type>
```

デバッグ中に、変数の横にある虫眼鏡アイコンを選択し、 **[テキスト ビジュアライザー]** を選択して、**m_pszData** でポイントされている文字列を表示できます。

 ![StringView ビジュアライザーを含む CStringT データ](../debugger/media/dbg_natvis_stringview_cstringt.png "StringView ビジュアライザーを含む CStringT データ")

式 `{m_pszData,su}` には、値を Unicode 文字列として表示する C++ 書式指定子 **su** が含まれています。 詳細については、[C++ での書式指定子](../debugger/format-specifiers-in-cpp.md)に関するページを参照してください。

### <a name="expand-element"></a><a name="BKMK_Expand"></a> Expand 要素

オプションの `Expand` ノードでは、変数ウィンドウで型が展開されたときの、視覚化された型の子をカスタマイズします。 `Expand` ノードでは、子要素を定義する子ノードのリストを使用できます。

- 視覚化エントリで `Expand` ノードを指定しないと、子では既定の展開規則が使用されます。

- `Expand` ノードで下位に子ノードを指定しない場合、型はデバッガー ウィンドウで展開されません。

#### <a name="item-expansion"></a><a name="BKMK_Item_expansion"></a> Item の展開

 `Item` 要素は、 `Expand` ノードでの最も基本的で一般的な要素です。 `Item` は 1 つの子要素を定義します。 たとえば、フィールド `top`、`left`、`right`、`bottom` を持つ `CRect` クラスに、次の視覚化エントリがあるとします。

```xml
<Type Name="CRect">
  <DisplayString>{{top={top} bottom={bottom} left={left} right={right}}}</DisplayString>
  <Expand>
    <Item Name="Width">right - left</Item>
    <Item Name="Height">bottom - top</Item>
  </Expand>
</Type>
```

デバッガー ウィンドウでは、`CRect` 型は次の例のようになります。

![Item 要素の展開を含む CRect](../debugger/media/dbg_natvis_expand_item_crect1.png "Item 要素の展開を含む CRect")

デバッガーにより、`Width` 要素と `Height` 要素で指定されている式が評価され、変数ウィンドウの **[値]** 列に値が表示されます。

デバッガーによって、すべてのカスタム展開に対して **[[未加工ビュー]]** ノードが自動的に作成されます。 上のスクリーンショットでは、 **[[未加工ビュー]]** ノードが展開表示され、オブジェクトの既定の未加工ビューが Natvis の視覚化とどのように異なるかが示されています。 既定の展開では、基底クラスのサブツリーが作成され、基底クラスのすべてのデータ メンバーが子として一覧表示されます。

> [!NOTE]
> Item 要素の展開により複合型が参照される場合は、**Item** ノード自体が展開可能です。

#### <a name="arrayitems-expansion"></a><a name="BKMK_ArrayItems_expansion"></a> Size
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

![ArrayItems の展開を使用した std::vector](../debugger/media/dbg_natvis_expand_arrayitems_stdvector.png "ArrayItems の展開を使用した std::vector")

`ArrayItems` ノードには次のものが必要です。

- デバッガーが配列の長さを解釈するための `Size` 式 (整数に評価されることが必要)。
- 最初の要素を参照する `ValuePointer` 式 (`void*` ではない要素型のポインターであることが必要)。

配列の既定の下限値は 0 です。 値をオーバーライドするには、`LowerBound` 要素を使用します。 Visual Studio に付属する *.natvis* ファイルに例があります。

>[!NOTE]
>`[]` 演算子 (`vector[i]` など) は、型自体でこの演算子が許可されていない場合でも (たとえば `CATLArray`)、`ArrayItems` を使用する 1 次元配列の視覚化で使用できます。

多次元配列を指定することもできます。 その場合、デバッガーでは、子要素を適切に表示するために、次のような若干の追加情報が必要になります。

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

- `Direction` では、配列が行優先であるか列優先であるかを指定します。
- `Rank` は配列のランクを指定します。
- `Size` 要素は暗黙の `$i` パラメーターを受け取ります。このパラメーターは次元のインデックスに置き換えられて、その次元の配列の長さが特定されます。 前の例では、式 `_M_extent.M_base[0]` で 0 番目の次元の長さ、`_M_extent._M_base[1]` で 1 番目の次元の長さが指定されます。

2 次元の `Concurrency::array` オブジェクトがデバッガー ウィンドウでどのように表示されるかを次に示します。

![ArrayItems の展開を含む 2 次元配列](../debugger/media/dbg_natvis_expand_arrayitems_2d.png "ArrayItems の展開を含む 2 次元配列")

#### <a name="indexlistitems-expansion"></a><a name="BKMK_IndexListItems_expansion"></a> IndexListItems の展開

`ArrayItems` の展開は、配列要素がメモリ内に連続して配置されている場合にのみ使用できます。 デバッガーでは、ポインターをインクリメントするだけで、次の要素が取得されます。 値ノードのインデックスを操作する必要がある場合は、`IndexListItems` ノードを使用します。 `IndexListItems` ノードによる視覚化を次に示します。

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

`ArrayItems` と `IndexListItems` の唯一の違いである `ValueNode` では、暗黙の <sup> パラメーターを使用して i</sup>`$i` 番目の要素に対する完全な式を指定します。

>[!NOTE]
>`[]` 演算子 (`vector[i]` など) は、型自体でこの演算子が許可されていない場合でも (たとえば `CATLArray`)、`IndexListItems` を使用する 1 次元配列の視覚化で使用できます。

#### <a name="linkedlistitems-expansion"></a><a name="BKMK_LinkedListItems_expansion"></a> LinkedListItems の展開

視覚化された型がリンク リストを表す場合、デバッガーは `LinkedListItems` ノードを使用してその子を表示できます。 `CAtlList` 型に対する次の視覚化では、`LinkedListItems` が使用されています。

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

デバッガーでの `NextPointer` および `ValueNode` の式の評価は、親のリスト型ではなく、`LinkedListItems` ノード要素のコンテキストで行われます。 前の例で、`CAtlList` には、リンク リストのノードである `CNode` クラス (`atlcoll.h` 内) があります。 `m_pNext` と `m_element` は、`CNode` クラスではなく、その `CAtlList` クラスのフィールドです。

`ValueNode` は空のままにすることも、`this` を使用して `LinkedListItems` ノード自体を参照することもできます。

#### <a name="customlistitems-expansion"></a>CustomListItems 展開

`CustomListItems` 展開を使用して、ハッシュ テーブルなどのデータ構造を走査する際にカスタム ロジックを記述することができます。 評価する必要のあるすべてのものに C++ の式を使用できるデータ構造を視覚化するには、`CustomListItems` を使用します。ただし、これは `ArrayItems`、`IndexListItems`、または `LinkedListItems` にはあまり適しません。

`Exec` を使用すると、展開内で定義されている変数とオブジェクトを使用して、`CustomListItems` の展開の内部でコードを実行できます。 `Exec` では、論理演算子、算術演算子、代入演算子を使用できます。 C++ の式エバリュエーターによってサポートされている[デバッガー組み込み関数](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state)を除き、`Exec` を使用して関数を評価することはできません。

`CAtlMap` に対する次の視覚化は、`CustomListItems` が適しているよい例です。

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

#### <a name="treeitems-expansion"></a><a name="BKMK_TreeItems_expansion"></a> TreeItems の展開
 視覚化された型がツリーを表す場合、デバッガーはツリーをたどり、 `TreeItems` ノードを使用してその子を表示できます。 `TreeItems` ノードを使用した `std::map` 型の視覚化を次に示します。

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

構文は `LinkedListItems` ノードと似ています。 `LeftPointer`、`RightPointer`、`ValueNode` は、ツリー ノード クラスのコンテキストで評価されます。 `ValueNode` は空のままにすることも、`this` を使用して `TreeItems` ノード自体を参照することもできます。

#### <a name="expandeditem-expansion"></a><a name="BKMK_ExpandedItem_expansion"></a> ExpandedItem の展開
 `ExpandedItem` 要素では、基底クラスまたはデータ メンバーのプロパティを視覚化された型の子であるかのように表示することで、子の集約ビューが生成されます。 デバッガーにより、指定した式が評価され、結果の子ノードが、視覚化された型の子リストに追加されます。

たとえば、スマート ポインター型 `auto_ptr<vector<int>>` は通常、次のように表示されます。

 ![auto&#95;ptr&#60;vector&#60;int&#62;&#62; の既定の展開](../debugger/media/dbg_natvis_expand_expandeditem_default.png "既定の展開")

 vector の値を表示するには、変数ウィンドウで `_Myptr` メンバーを通って 2 階層下にドリルダウンする必要があります。 `ExpandedItem` 要素を追加することで、階層から `_Myptr` 変数を排除し、vector の要素を直接表示できます。

```xml
<Type Name="std::auto_ptr&lt;*&gt;">
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>
  <Expand>
    <ExpandedItem>_Myptr</ExpandedItem>
  </Expand>
</Type>
```

 ![auto&#95;ptr&#60;vector&#60;int&#62;&#62; の ExpandedItem の展開](../debugger/media/dbg_natvis_expand_expandeditem_visualized.png "ExpandedItem の展開")

次の例では、基底クラスのプロパティを派生クラスに集約する方法を示します。 `CPanel` クラスが `CFrameworkElement`から派生しているとします。 基底クラス `CFrameworkElement` のプロパティを繰り返す代わりに、`ExpandedItem` ノードの展開により、それらのプロパティが `CPanel` クラスの子リストに追加されます。

```xml
<Type Name="CPanel">
  <DisplayString>{{Name = {*(m_pstrName)}}}</DisplayString>
  <Expand>
    <Item Name="IsItemsHost">(bool)m_bItemsHost</Item>
    <ExpandedItem>*(CFrameworkElement*)this,nd</ExpandedItem>
  </Expand>
</Type>
```

派生クラスの視覚化の対応付けを無効にする **nd** 書式指定子がここで必要になります。 そうしないと、既定の視覚化型一致ルールによってそれが最適と解釈され、式 `*(CFrameworkElement*)this` により `CPanel` の視覚化が再び適用されます。 基底クラスの視覚化を使用するように、または基底クラスに視覚化がない場合は既定の展開を適用するように、デバッガーに指示するには、**nd** 書式指定子を使用します。

#### <a name="synthetic-item-expansion"></a><a name="BKMK_Synthetic_Item_expansion"></a> Synthetic Item の展開
 `ExpandedItem` 要素は階層を排除することでデータ ビューを平坦化しますが、`Synthetic` ノードはその反対のことを行います。 それを使用すると、式の結果ではない人工の子要素を作成できます。 人工の要素には、独自の子要素を含めることができます。 次の例では、 `Concurrency::array` 型の視覚化で `Synthetic` ノードを使用して、診断メッセージをユーザーに表示しています。

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

 ![Synthetic 要素の展開を含む Concurrency::Array](../debugger/media/dbg_natvis_expand_synthetic.png "Synthetic 要素の展開を含む Concurrency::Array")

### <a name="hresult-element"></a><a name="BKMK_HResult"></a> HResult 要素
 `HResult` 要素を使用すると、デバッガー ウィンドウに表示される **HRESULT** に関する情報をカスタマイズできます。 `HRValue` 要素には、カスタマイズする **HRESULT** の 32 ビット値を格納する必要があります。 `HRDescription` 要素には、デバッガー ウィンドウに表示する情報を格納します。

```xml

<HResult Name="MY_E_COLLECTION_NOELEMENTS">
  <HRValue>0xABC0123</HRValue>
  <HRDescription>No elements in the collection.</HRDescription>
</HResult>
```

### <a name="uivisualizer-element"></a><a name="BKMK_UIVisualizer"></a> UIVisualizer 要素
`UIVisualizer` 要素は、グラフィカル ビジュアライザー プラグインをデバッガーに登録するために使用します。 グラフィカル ビジュアライザーでは、データ型と一貫性のある方法で変数またはオブジェクトが表示されるダイアログ ボックスまたは他のインターフェイスが作成されます。 ビジュアライザー プラグインは、[VSPackage](../extensibility/internals/vspackages.md) として作成し、デバッガーで使用できるサービスを公開する必要があります。 *.natvis* ファイルには、プラグインに関する登録情報 (その名前、公開されるサービスの GUID、視覚化できる型など) が格納されます。

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

- `ServiceId` - `Id` の属性ペアでは、`UIVisualizer` が示されます。 `ServiceId` は、ビジュアライザー パッケージで公開されるサービスの GUID です。 `Id` は、サービスで複数のビジュアライザーが提供される場合に、ビジュアライザーを区別する一意の識別子です。 前の例では、同じビジュアライザー サービスで 2 つのビジュアライザーが提供されています。

- `MenuName` 属性では、デバッガーの虫眼鏡アイコンの横にあるドロップダウンに表示されるビジュアライザーの名前を定義します。 次に例を示します。

  ![UIVisualizer メニューのショートカット メニュー](../debugger/media/dbg_natvis_vectorvisualizer.png "UIVisualizer メニューのショートカット メニュー")

*.natvis* ファイルで定義されている各型に対し、それを表示できる UI ビジュアライザーのリストを明示的に指定する必要があります。 デバッガーでは、型エントリ内のビジュアライザーの参照と、登録されているビジュアライザーが照合されます。 たとえば、`std::vector` に対する次の型エントリでは、前の例の `UIVisualizer` が参照されています。

```xml
<Type Name="std::vector&lt;int,*&gt;">
  <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}" Id="1" />
</Type>
```

 `UIVisualizer` の例は、メモリ内のビットマップの表示に使用される [Image Watch](https://marketplace.visualstudio.com/search?term=%22Image%20Watch%22&target=VS&category=All%20categories&vsVersion=&sortBy=Relevance) で確認できます。

### <a name="customvisualizer-element"></a><a name="BKMK_CustomVisualizer"></a>CustomVisualizer 要素
 `CustomVisualizer` は、Visual Studio のコードで視覚化を制御するために作成する VSIX 拡張機能を指定する拡張ポイントです。 VSIX 拡張機能の記述方法について詳しくは、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」をご覧ください。

カスタム ビジュアライザーを記述するには、XML Natvis の定義より多くの作業が必要になりますが、Natvis でサポートできることとできないことについての制約はありません。 カスタム ビジュアライザーを使用すると、デバッガーの拡張性 API の全セットにアクセスできます。これらの API は、デバッグ対象のプロセスの照会および変更、または Visual Studio の他の部分との通信に使用できます。

 `CustomVisualizer` 要素では、`Condition`、`IncludeView`、および `ExcludeView` 属性を使用できます。

## <a name="limitations"></a>制限事項

Natvis のカスタマイズは、クラスと構造体では機能しますが、typedef では使用できません。

Natvis では、プリミティブ型 (`int`、`bool` など) またはプリミティブ型へのポインターに対するビジュアライザーはサポートされていません。 このシナリオでの 1 つのオプションは、ユース ケースに適した[書式指定子](../debugger/format-specifiers-in-cpp.md)を使用することです。 たとえば、コードで `double* mydoublearray` を使用する場合は、デバッガーの **[ウォッチ]** ウィンドウで配列書式指定子を使用できます。`mydoublearray, [100]` という式では、最初の 100 要素が表示されます。
