---
title: C++ オブジェクトのカスタム ビューを作成する
description: Natvis フレームワークを使用して、Visual Studio がデバッガーでネイティブ型を表示する方法をカスタマイズする
ms.date: 03/02/2020
ms.topic: conceptual
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
ms.openlocfilehash: 4f8bdd8d26ba450b1aedd790d644c183607c44af
ms.sourcegitcommit: b4e0cc76d94fe8cf6d238c4cc09512d17131a195
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81224512"
---
# <a name="create-custom-views-of-c-objects-in-the-debugger-using-the-natvis-framework"></a>Natvis フレームワークを使用してデバッガーで C++ オブジェクトのカスタム ビューを作成します。

Visual Studio *Natvis*フレームワークは、**デバッガー**変数ウィンドウ (ローカル ウィンドウ、**ウォッチ**ウィンドウなど) や**DataTips**でネイティブ型が表示される方法をカスタマイズします。 Natvis ビジュアライゼーションは、デバッグ中に作成する型をより見やすくするのに役立ちます。

Natvis は、以前のバージョンの Visual Studio の*autoexp.dat*ファイルを XML 構文、診断、バージョン管理、および複数のファイル サポートに置き換えます。

> [!NOTE]
> Natvis のカスタマイズはクラスと構造体で動作しますが、typedef は使用できません。

## <a name="natvis-visualizations"></a><a name="BKMK_Why_create_visualizations_"></a>ナトビスの視覚化

Natvis フレームワークを使用して、開発者がデバッグ中に簡単に表示できるように、作成する型の視覚化ルールを作成します。

たとえば、次の図は、カスタムビジュアライゼーションが適用されずにデバッガー ウィンドウの[Windows::UI::Xaml:Controls::TextBox](/uwp/api/Windows.UI.Xaml.Controls.TextBox)型の変数を示しています。

![TextBox の既定の視覚表現](../debugger/media/dbg_natvis_textbox_default.png "TextBox の既定の視覚表現")

強調表示された行には `Text` クラスの `TextBox` プロパティが示されています。 複雑なクラス階層では、このプロパティを見つけることが困難になります。 デバッガーはカスタム文字列型の解釈方法を認識しないので、テキスト ボックス内に保持されている文字列を表示できません。

Natvis`TextBox`カスタム ビジュアライザー ルールが適用される場合、変数ウィンドウでも同じ外観が非常に単純になります。 クラスの重要なメンバーが一緒に表示され、デバッガーはカスタム文字列型の基になる文字列値を示します。

![ビジュアライザーを使用した TextBox データ](../debugger/media/dbg_natvis_textbox_visualizer.png "ビジュアライザーを使用した TextBox データ")

## <a name="use-natvis-files-in-c-projects"></a><a name="BKMK_Using_Natvis_files"></a>C++ プロジェクトで .natvis ファイルを使用する

Natvis は *.natvis*ファイルを使用して視覚化ルールを指定します。 *.natvis*ファイルは *、.natvis*拡張子を持つ XML ファイルです。 Natvis スキーマは *、%VSINSTALLDIR%\Xml\スキーマ\natvis.xsd で定義されています*。

*natvis*ファイルの基本構造は、視覚化エントリを表`Type`す 1 つ以上の要素です。 各`Type`要素の完全修飾名は、その`Name`属性で指定されます。

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

Visual Studio は *、%VSINSTALLDIR%\Common7\パッケージ\デバッガー\ビジュアライザー*フォルダーにいくつかの *.natvis*ファイルを提供します。 これらのファイルには、多くの一般的なタイプの視覚化ルールがあり、新しいタイプのビジュアライゼーションを作成する例として役立ちます。

### <a name="add-a-natvis-file-to-a-c-project"></a>C++ プロジェクトに .natvis ファイルを追加する

任意の C++ プロジェクトに *.natvis*ファイルを追加できます。

**新しい *.natvis*ファイルを追加するには、次の手順を実行します。**

1. **ソリューション エクスプローラ**で C++ プロジェクト ノードを選択し、[**プロジェクト** > **の新しい項目の追加**] を選択するか、プロジェクトを右クリックして [**新しい項目**の**追加** > ] を選択します。

1. [**新しい項目の追加]** ダイアログで **、[Visual C++** > **ユーティリティ** > **デバッガ ビジュアライゼーション ファイル (.natvis)]** を選択します。

1. ファイルに名前を付け、[**追加**] を選択します。

   新しいファイルがソリューション**エクスプローラー**に追加され、Visual Studio のドキュメント ウィンドウに開きます。

Visual Studio デバッガーは、C++ プロジェクトに *.natvis*ファイルを自動的に読み込み、既定では、プロジェクトのビルド時に *.pdb*ファイルにも含めます。 ビルドされたアプリをデバッグする場合、プロジェクトを開いていなくても、デバッガーは *.pdb*ファイルから *.natvis*ファイルを読み込みます。 *.pdb に .natvis*ファイルを含めない *.pdb*場合は、ビルドされた *.pdb*ファイルから除外できます。

**.pdb から *.natvis*ファイルを除外するには、次の*手順に従います*。**

1. **ソリューション エクスプローラ**で *.natvis*ファイルを選択し、[**プロパティ]** アイコンを選択するか、ファイルを右クリックして **[プロパティ]** を選択します。

1. [**ビルドから除外**] の横にある矢印を下にドロップし、[**はい**] を選択して **、[OK] を**選択します。

>[!NOTE]
>実行可能プロジェクトをデバッグする場合は、C++ プロジェクトが利用できないので、ソリューション項目を使用して *.pdb*に存在しない *.natvis*ファイルを追加します。

>[!NOTE]
>*pdb*からロードされた Natvis 規則は *、.pdb*が参照するモジュール内の型にのみ適用されます。 たとえば *、Module1.pdb*にという名前`Test`の型の Natvis エントリがある場合、そのエントリ`Test`は*Module1.dll*のクラスにのみ適用されます。 別のモジュールが、 という名前`Test`のクラスも定義している場合 *、Module1.pdb* Natvis エントリは、そのモジュールに適用されません。

**VSIX パッケージを使用して *.natvis*ファイルをインストールして登録するには、次の手順を実行します。**

VSIX パッケージは *、.natvis*ファイルをインストールして登録できます。 どこにインストールされていても、登録されているすべての *.natvis*ファイルはデバッグ中に自動的に取得されます。

1. VSIX パッケージに *.natvis*ファイルを含めます。 たとえば、次のプロジェクト ファイルの場合を考えます。
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ToolsVersion="14.0">
     <ItemGroup>
       <VSIXSourceItem Include="Visualizer.natvis" />
     </ItemGroup>
   </Project>
   ```

2. *.natvis*ファイルを*ソース.extension.vsixmanifest*ファイルに登録します。
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
     <Assets>
       <Asset Type="NativeVisualizer" Path="Visualizer.natvis"  />
     </Assets>
   </PackageManifest>
   ```

### <a name="natvis-file-locations"></a><a name="BKMK_natvis_location"></a>ナトビス ファイルの場所

複数のプロジェクトに .natvis ファイルを適用する場合は、ユーザー ディレクトリまたはシステム ディレクトリに *.natvis*ファイルを追加できます。

*natvis*ファイルは、次の順序で評価されます。

1. デバッグ中の *.pdb*に埋め込まれている *.natvis*ファイル (読み込まれたプロジェクトに同じ名前のファイルが存在しない場合)。

2. 読み込まれた C++ プロジェクトまたはトップレベル ソリューション内の *.natvis*ファイル。 このグループには、クラス ライブラリを含むすべての読み込み済み C++ プロジェクトが含まれますが、他の言語のプロジェクトは含まれません。

3. VSIX パッケージを使用してインストールおよび登録された *.natvis*ファイル。

::: moniker range="vs-2017"

4. ユーザー固有の Natvis ディレクトリ (たとえば *、%USERPROFILE%\ドキュメント\Visual Studio 2017\ビジュアライザー*)。

::: moniker-end

::: moniker range=">= vs-2019"

4. ユーザー固有の Natvis ディレクトリ (たとえば *、%USERPROFILE%\ドキュメント\Visual Studio 2019\ビジュアライザー*)。

::: moniker-end

5. システム全体の Natvis ディレクトリ (*%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers*)。 このディレクトリには、Visual Studio と共にインストールされる *.natvis*ファイルがあります。 管理者権限を持っている場合は、このディレクトリにファイルを追加できます。

## <a name="modify-natvis-files-while-debugging"></a>デバッグ中に .natvis ファイルを変更する

プロジェクトのデバッグ中に IDE で *.natvis*ファイルを変更できます。 デバッグに使用する Visual Studio の同じインスタンスでファイルを開き、変更して保存します。 ファイルが保存されるとすぐに、[**ウォッチ]** ウィンドウと **[ローカル]** ウィンドウが更新され、変更が反映されます。

デバッグ中のソリューションで *.natvis*ファイルを追加または削除したり、Visual Studio によって関連する視覚エフェクトを追加または削除することもできます。

デバッグ中に *.pdb*ファイルに埋め込まれた *.natvis*ファイルは更新できません。

*.natvis*ファイルを Visual Studio の外部で変更した場合、その変更は自動的には反映されません。 デバッガー ウィンドウを更新するには、**イミディエイト**ウィンドウで **.natvisreload**コマンドを再評価できます。 その後、デバッグ セッションを再開せずに変更が有効になります。

また **、.natvisreload**コマンドを使用して *、.natvis*ファイルを新しいバージョンにアップグレードします。 たとえば *、.natvis*ファイルがソース管理にチェックインされ、他のユーザーが行った最近の変更を取り出す場合があります。

## <a name="expressions-and-formatting"></a><a name="BKMK_Expressions_and_formatting"></a>式と書式
Natvis 視覚化では、C++ 式を使用して、表示するデータ項目を指定します。 デバッガーでの C++ 式の機能強化と制限に加えて、[コンテキスト演算子 (C++)](../debugger/context-operator-cpp.md)で説明されている、次の点に注意してください。

- Natvis 式は、現在のスタック フレームではなく視覚化されるオブジェクトのコンテキストで評価されます。 たとえば、Natvis 式では、`x`現在の関数の**x**という名前のローカル変数ではなく、視覚化されるオブジェクトの**x**という名前のフィールドを参照します。 Natvis 式ではローカル変数にはアクセスできませんが、グローバル変数にはアクセスできます。

- Natvis 式では、関数の評価や副作用は許可されません。 関数呼び出しと代入演算子は無視されます。 [デバッガーの組み込み関数](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state) は、他の関数とは異なり副作用がないため、Natvis 式からは自由に呼び出すことができます。

- 式の表示方法を制御するには[、「C++](format-specifiers-in-cpp.md#BKMK_Visual_Studio_2012_format_specifiers)の Format 指定子」で説明されている書式指定子を使用できます。 `Size` [ArrayItems 拡張](../debugger/create-custom-views-of-native-objects.md#BKMK_ArrayItems_expansion)の式など、Natvis によって内部的に使用される場合、書式指定子は無視されます。

## <a name="natvis-views"></a>Natvis ビュー

異なる Natvis ビューを定義して、さまざまな方法でタイプを表示できます。 たとえば、 という名前の`std::vector`簡易ビューを定義する視覚化を次に`simple`示します。 要素`DisplayString`と要素`ArrayItems`は既定のビューとビュー`simple`に表示されますが、`[size]`および`[capacity]`の項目はビューに`simple`表示されません。

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

[**ウォッチ**] ウィンドウで **、.view**書式指定子を使用して代替ビューを指定します。 単純なビューは**vec,view(単純)** として表示されます。

![単純なビューを備えた [ウォッチ] ウィンドウ](../debugger/media/watch-simpleview.png "単純なビューを備えた [ウォッチ] ウィンドウ")

## <a name="natvis-errors"></a><a name="BKMK_Diagnosing_Natvis_errors"></a>ナトビスエラー

デバッガーは、ビジュアライゼーション エントリでエラーを検出すると、無視されます。 タイプを生の形式で表示するか、別の適切なビジュアライゼーションを選択します。 Natvis 診断を使用すると、デバッガーがビジュアライゼーション エントリを無視した理由を理解し、基になる構文と解析エラーを確認できます。

**Natvis 診断をオンにするには:**

- [**ツール** > **オプション**] (または [**デバッグ** > **オプション**] ) > **[デバッグ** > **出力ウィンドウ**] で **、Natvis 診断メッセージ (C++ のみ)** を **[エラー**]、[**警告**]、[**詳細]** に設定し **、[OK] を**選択します。

エラーは**出力**ウィンドウに表示されます。

## <a name="natvis-syntax-reference"></a><a name="BKMK_Syntax_reference"></a>ナトビス構文リファレンス

### <a name="autovisualizer-element"></a><a name="BKMK_AutoVisualizer"></a> AutoVisualizer の要素
`AutoVisualizer` 要素は *.natvis* ファイルのルート ノードであり、名前空間 `xmlns:` 属性を含みます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">
.
.
</AutoVisualizer>
```

要素`AutoVisualizer`には、[型](#BKMK_Type)[、HResult、UI](#BKMK_HResult)[ビジュアライザー](#BKMK_UIVisualizer)、および[カスタム ビジュアライザー](#BKMK_CustomVisualizer)の子を持つことができます。

### <a name="type-element"></a><a name="BKMK_Type"></a>型要素

基本的な`Type`例は次のようになります。

```xml
<Type Name="[fully qualified type name]">
  <DisplayString Condition="[Boolean expression]">[Display value]</DisplayString>
  <Expand>
    ...
  </Expand>
</Type>
```

 要素`Type`は次の項目を指定します。

1. 視覚化を使用する必要があるタイプ (`Name`属性)。

2. その型のオブジェクトの値がどのように表示されるか ( `DisplayString` 要素)。

3. ユーザーが変数ウィンドウ (ノード) で型を展開したときの型のメンバーの`Expand`外観。

#### <a name="templated-classes"></a>テンプレート化されたクラス
要素`Name`の`Type`属性は、テンプレート化されたクラス`*`名に使用できるワイルドカード文字としてアスタリスクを使用します。

次の例では、オブジェクトが a`CAtlArray<int>`または a のどちらであるか`CAtlArray<float>`に関係なく、同じビジュアリゼーションが使用されます。 に対して特定の視覚化エントリ`CAtlArray<float>`がある場合は、ジェネリックエントリよりも優先されます。

```xml
<Type Name="ATL::CAtlArray&lt;*&gt;">
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>
</Type>
```

マクロ $T1、$T2 などを使用して、ビジュアライゼーション エントリ内のテンプレート パラメーターを参照できます。 これらのマクロの例を見つけるには、Visual Studio に付属の *.natvis* ファイルをご覧ください。

#### <a name="visualizer-type-matching"></a><a name="BKMK_Visualizer_type_matching"></a>ビジュアライザーの種類の一致
視覚化エントリが検証に失敗した場合は、次に使用可能なビジュアライゼーションが使用されます。

#### <a name="inheritable-attribute"></a>継承可能な属性
オプション`Inheritable`の属性は、視覚エフェクトを基本型だけに適用するか、基本型とすべての派生型に適用するかを指定します。 `Inheritable` の既定値は `true` です。

次の例では、ビジュアライゼーション`BaseClass`はタイプにのみ適用されます。

```xml
<Type Name="Namespace::BaseClass" Inheritable="false">
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>
</Type>
```

#### <a name="priority-attribute"></a>Priority 属性

オプション`Priority`の属性は、定義が解析に失敗した場合に、代替定義を使用する順序を指定します。 の値は`Priority``Low`、 、 `MediumLow`、`Medium` `MediumHigh`、 `High`、 、 、 です。 既定値は `Medium` です。 この`Priority`属性は、同じ *.natvis*ファイル内の優先順位のみを区別します。

次の例では、最初に 2015 STL に一致するエントリを解析します。 これが解析に失敗した場合は、STL の 2013 バージョンの代替エントリを使用します。

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
任意のノードに`Optional`属性を設定できます。 オプションノード内の部分式が解析に失敗すると、デバッガーはそのノードを無視しますが、残りのルールを適用`Type`します。 次の型では、 `[State]` は省略不可能ですが、 `[Exception]` は省略可能です。  _`MyNamespace::MyClass``M_exceptionHolder`という名前のフィールドがある場合、`[State]`ノードとノード`[Exception]`の両方が表示されますが、フィールドがない`_M_exceptionHolder`場合は`[State]`ノードのみが表示されます。

```xml
<Type Name="MyNamespace::MyClass">
    <Expand>
      <Item Name="[State]">_M_State</Item>
      <Item Name="[Exception]" Optional="true">_M_exceptionHolder</Item>
    </Expand>
</Type>
```

### <a name="condition-attribute"></a><a name="BKMK_Condition_attribute"></a> Condition 属性

オプション`Condition`の属性は、多くの視覚化エレメントで使用でき、視覚化ルールを使用するタイミングを指定します。 条件属性内の式が`false`に解決される場合、視覚化ルールは適用されません。 に評価される`true`場合、または属性がない`Condition`場合は、ビジュアライゼーションが適用されます。 この属性は、視覚化エントリの if-else ロジックに使用できます。

たとえば、次の視覚化には、スマート`DisplayString`ポインター型の 2 つの要素があります。 メンバーが`_Myptr`空の場合、最初`DisplayString`の要素の条件は`true`に解決され、フォームが表示されます。 メンバーが`_Myptr`空でない場合、条件は`false`に評価され、2 番目`DisplayString`の要素が表示されます。

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

属性`IncludeView`と`ExcludeView`属性は、特定のビューに表示する要素を指定します。 たとえば、`std::vector`次の Natvis 仕様では、`simple`ビューには`[size]`と`[capacity]`の項目は表示されません。

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

属性と 属性`IncludeView``ExcludeView`は、型と個々のメンバーに対して使用できます。

### <a name="version-element"></a><a name="BKMK_Versioning"></a>バージョン要素
この`Version`要素は、視覚化エントリを特定のモジュールとバージョンにスコープします。 この`Version`要素は、名前の競合を回避し、不一致を減らし、タイプ別のバージョンごとに異なる視覚化を可能にします。

異なるモジュールで使用される共通のヘッダー ファイルで型が定義されている場合、バージョン対応のビジュアライゼーションは、そのタイプが指定されたモジュール バージョンにある場合にのみ表示されます。

次の例では、ビジュアライゼーションは`DirectUI::Border`バージョン 1.0`Windows.UI.Xaml.dll`から 1.5 の型にのみ適用できます。

```xml
<Type Name="DirectUI::Border">
  <Version Name="Windows.UI.Xaml.dll" Min="1.0" Max="1.5"/>
  <DisplayString>{{Name = {*(m_pDO->m_pstrName)}}}</DisplayString>
  <Expand>
    <ExpandedItem>*(CBorder*)(m_pDO)</ExpandedItem>
  </Expand>
</Type>
```

と の`Min``Max`両方は必要ありません。 これらはオプションの属性です。 ワイルドカード文字はサポートされていません。

属性`Name`は *、hello.exe*や*some.dll*などの*ファイル名.ext*形式です。 パス名は使用できません。

### <a name="displaystring-element"></a><a name="BKMK_DisplayString"></a>文字列要素を表示します。
要素`DisplayString`は、変数の値として表示する文字列を指定します。 この要素には、任意の文字列を式と組み合わせて使用できます。 中かっこ内のすべてのものは式として解釈されます。 たとえば、次のエントリ`DisplayString`を使用します。

```xml
<Type Name="CPoint">
  <DisplayString>{{x={x} y={y}}}</DisplayString>
</Type>
```

次の図のように、`CPoint`型の変数が表示されることを意味します。

 ![要素を使用します。](../debugger/media/dbg_natvis_cpoint_displaystring.png "要素を使用します。")

および`y``DisplayString`のメンバー`x``CPoint`である 式では、中かっこ内に含まれるため、値が評価されます。 また、この例では、中かっこ (`{{`または`}}`) を使用して中かっこをエスケープする方法も示しています。

> [!NOTE]
> `DisplayString` 要素でのみ、任意の文字列と中かっこ構文を使用できます。 その他の視覚化要素はすべて、デバッガーが評価できる式のみを受け入れます。

### <a name="stringview-element"></a><a name="BKMK_StringView"></a>要素を表示します。

要素`StringView`は、デバッガーが組み込みのテキスト ビジュアライザーに送信できる値を定義します。 たとえば、タイプに対して次のような視覚化`ATL::CStringT`を行います。

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">
  <DisplayString>{m_pszData,su}</DisplayString>
</Type>
```

オブジェクト`CStringT`は、次の例のように変数ウィンドウに表示されます。

![CStringT DisplayString 要素](../debugger/media/dbg_natvis_displaystring_cstringt.png "CStringT DisplayString 要素")

要素を`StringView`追加すると、デバッガーは値をテキストビジュアライゼーションとして表示できます。

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">
  <DisplayString>{m_pszData,su}</DisplayString>
  <StringView>m_pszData,su</StringView>
</Type>
```

デバッグ中に、変数の横にある虫眼鏡アイコンを選択し、**テキスト ビジュアライザー**を選択して **、m_pszData**が指す文字列を表示できます。

 ![StringView ビジュアライザーを含む CStringT データ](../debugger/media/dbg_natvis_stringview_cstringt.png "StringView ビジュアライザーを含む CStringT データ")

式`{m_pszData,su}`には、値を Unicode 文字列として表示する C++ 書式指定子**su**が含まれています。 詳細については、「 [C++ での書式指定子](../debugger/format-specifiers-in-cpp.md)」を参照してください。

### <a name="expand-element"></a><a name="BKMK_Expand"></a>要素を展開

オプション`Expand`のノードは、変数ウィンドウで型を展開するときに、視覚化された型の子をカスタマイズします。 ノード`Expand`は、子要素を定義する子ノードのリストを受け入れます。

- ノードが`Expand`ビジュアライゼーション エントリに指定されていない場合、子は既定の展開規則を使用します。

- ノードの`Expand`下に子ノードが指定されていない場合、デバッガー ウィンドウで型を展開することはできません。

#### <a name="item-expansion"></a><a name="BKMK_Item_expansion"></a>アイテム展開

 要素`Item`は、ノード内で最も基本的で一`Expand`般的な要素です。 `Item` は 1 つの子要素を定義します。 たとえば`CRect`、フィールド`top`、 、、`left``right`および`bottom`、 を持つクラスには、次の視覚化エントリがあります。

```xml
<Type Name="CRect">
  <DisplayString>{{top={top} bottom={bottom} left={left} right={right}}}</DisplayString>
  <Expand>
    <Item Name="Width">right - left</Item>
    <Item Name="Height">bottom - top</Item>
  </Expand>
</Type>
```

デバッガー ウィンドウでは、型`CRect`は次の例のようになります。

![Item 要素の展開を含む CRect](../debugger/media/dbg_natvis_expand_item_crect1.png "Item 要素の展開を含む CRect")

デバッガーは、 要素と`Width``Height`要素で指定された式を評価し、変数ウィンドウの **[値**] 列に値を表示します。

デバッガーは、カスタム展開ごとに **[Raw View]** ノードを自動的に作成します。 上のスクリーンショットでは **、[Raw View]** ノードが展開され、オブジェクトの既定の未加工ビューと Natvis の視覚化がどのように異なるかを示しています。 既定の展開では、基本クラスのサブツリーが作成され、基本クラスのすべてのデータ メンバーが子として一覧表示されます。

> [!NOTE]
> 項目要素の式が複合型を指している場合 **、Item**ノード自体は展開可能です。

#### <a name="arrayitems-expansion"></a><a name="BKMK_ArrayItems_expansion"></a>配列アイテムの展開
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

ノード`ArrayItems`には以下が必要です。

- デバッガーが配列の長さを解釈するための `Size` 式 (整数に評価されることが必要)。
- 最初`ValuePointer`の要素を指す式です ( 要素`void*`型のポインターでない必要があります)。

配列の既定の下限値は 0 です。 値をオーバーライドするには、要素を`LowerBound`使用します。 Visual Studio に付属の *.natvis*ファイルには、例があります。

>[!NOTE]
>`[]`演算子`vector[i]`を使用する場合は、型自体 (たとえば`ArrayItems``CATLArray`) でこの演算子を許可しない場合でも、 を使用する 1 次元配列の視覚化を使用できます。

多次元配列を指定することもできます。 その場合、デバッガは子要素を正しく表示するために少し多くの情報を必要とします。

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

- `Direction`配列が行メジャーまたは列メジャーのどちらの順序であるかを指定します。
- `Rank` は配列のランクを指定します。
- `Size` 要素は暗黙の `$i` パラメーターを受け取ります。このパラメーターは次元のインデックスに置き換えられて、その次元の配列の長さが特定されます。 前の例では、式`_M_extent.M_base[0]`は 0 番目の次元の長さ、1`_M_extent._M_base[1]`番目の次元などを指定する必要があります。

2 次元`Concurrency::array`オブジェクトがデバッガー ウィンドウでどのように表示されるかを次に示します。

![配列項目拡張を持つ 2 次元配列](../debugger/media/dbg_natvis_expand_arrayitems_2d.png "配列項目拡張を持つ 2 次元配列")

#### <a name="indexlistitems-expansion"></a><a name="BKMK_IndexListItems_expansion"></a> IndexListItems の展開

配列要素が`ArrayItems`メモリ内に連続して配置されている場合にのみ、展開を使用できます。 デバッガーは、ポインターをインクリメントするだけで次の要素に到達します。 値ノードへのインデックスを操作する必要がある場合は、ノード`IndexListItems`を使用します。 ノードを使用したビジュア`IndexListItems`ライゼーションを次に示します。

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

と`ArrayItems`の`IndexListItems`唯一`ValueNode`の違いは、暗黙的な`$i`パラメーターを持つ i<sup>番目</sup>の要素に完全な式を期待する です。

>[!NOTE]
>`[]`演算子`vector[i]`を使用する場合は、型自体 (たとえば`IndexListItems``CATLArray`) でこの演算子を許可しない場合でも、 を使用する 1 次元配列の視覚化を使用できます。

#### <a name="linkedlistitems-expansion"></a><a name="BKMK_LinkedListItems_expansion"></a>展開されたリストアイテム

視覚化された型がリンク リストを表す場合、デバッガーは `LinkedListItems` ノードを使用してその子を表示できます。 この型の次の`CAtlList`視覚化では`LinkedListItems`、 が使用されます。

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

デバッガーは、親リスト`NextPointer`型`ValueNode`ではなく、ノード要素の`LinkedListItems`コンテキストで and 式を評価します。 前の例では、`CAtlList`リンク リスト`CNode`のノードであるクラス`atlcoll.h`( に含まれる ) があります。 `m_pNext`クラス`m_element`のフィールドではなく、`CNode`そのクラスの`CAtlList`フィールドです。

`ValueNode`は空のままにすることも、`this``LinkedListItems`ノード自体を参照するために使用することもできます。

#### <a name="customlistitems-expansion"></a>CustomListItems 展開

`CustomListItems` 展開を使用して、ハッシュ テーブルなどのデータ構造を走査する際にカスタム ロジックを記述することができます。 評価`CustomListItems`する必要があるすべてのものに C++ 式を使用できるが、 、`IndexListItems`または`LinkedListItems`の型に合わないデータ構造を`ArrayItems`視覚化するために使用します。

を使用`Exec`して、展開で定義された変数`CustomListItems`とオブジェクトを使用して、展開の内部でコードを実行できます。 論理演算子、算術演算子、および代入演算子を 使用できます`Exec`。 C++ 式エ`Exec`バリュエーターでサポートされている[デバッガー組み込み関数](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state)を除き、関数の評価に使用することはできません。

以下のビジュア`CAtlMap`ライザーは、適切な`CustomListItems`場合の優れた例です。

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

#### <a name="treeitems-expansion"></a><a name="BKMK_TreeItems_expansion"></a>ツリーアイテムの展開
 視覚化された型がツリーを表す場合、デバッガーはツリーをたどり、 `TreeItems` ノードを使用してその子を表示できます。 ノードを使用した型の視覚化`std::map`を次に`TreeItems`示します。

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

構文は`LinkedListItems`ノードに似ています。 `LeftPointer`、、`RightPointer`および`ValueNode`はツリーノードクラスのコンテキストで評価されます。 `ValueNode`は空のままにすることも`this``TreeItems`、ノード自体を参照するために使用することもできます。

#### <a name="expandeditem-expansion"></a><a name="BKMK_ExpandedItem_expansion"></a> ExpandedItem の展開
 要素`ExpandedItem`は、視覚化された型の子であるかのように、基本クラスまたはデータ メンバーのプロパティを表示することによって、集計された子ビューを生成します。 デバッガーは、指定された式を評価し、結果の子ノードを視覚化された型の子リストに追加します。

たとえば、スマート ポインター型`auto_ptr<vector<int>>`は通常次のように表示されます。

 ![自動&#95;ptr&#60;ベクトル&#60;デフォルトの拡張&#62;&#62; しません](../debugger/media/dbg_natvis_expand_expandeditem_default.png "既定の展開")

 ベクトルの値を確認するには、変数ウィンドウでメンバーを通過する 2 つのレベルをドリルダウンする`_Myptr`必要があります。 `ExpandedItem` 要素を追加することで、階層から `_Myptr` 変数を排除し、vector の要素を直接表示できます。

```xml
<Type Name="std::auto_ptr&lt;*&gt;">
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>
  <Expand>
    <ExpandedItem>_Myptr</ExpandedItem>
  </Expand>
</Type>
```

 ![自動&#95;ptr&#60;ベクトル&#60;展開&#62;&#62; 拡張](../debugger/media/dbg_natvis_expand_expandeditem_visualized.png "ExpandedItem の展開")

次の例は、派生クラスの基本クラスからプロパティを集計する方法を示しています。 `CPanel` クラスが `CFrameworkElement`から派生しているとします。 ノードビジュアライゼーションでは、基本`CFrameworkElement`クラスから取得したプロパティを繰り返す代わりに、クラスの子リストにこれらのプロパティが`CPanel`追加されます。 `ExpandedItem`

```xml
<Type Name="CPanel">
  <DisplayString>{{Name = {*(m_pstrName)}}}</DisplayString>
  <Expand>
    <Item Name="IsItemsHost">(bool)m_bItemsHost</Item>
    <ExpandedItem>*(CFrameworkElement*)this,nd</ExpandedItem>
  </Expand>
</Type>
```

派生クラスの視覚化の対応付けを無効にする **nd** 書式指定子がここで必要になります。 それ以外の場合`*(CFrameworkElement*)this`、既定の`CPanel`ビジュアリゼーション タイプの一致ルールが最も適切であると見なされるため、式によって再びビジュアライゼーションが適用されます。 基本クラスのビジュアライゼーションを使用するようにデバッガーに指示するには **、nd**書式指定子を使用します。

#### <a name="synthetic-item-expansion"></a><a name="BKMK_Synthetic_Item_expansion"></a>合成品目展開
 `ExpandedItem` 要素は階層を排除することでデータ ビューを平坦化しますが、`Synthetic` ノードはその反対のことを行います。 式の結果ではない人工子要素を作成できます。 人工要素は、それ自体の子要素を持つことができます。 次の例では、 `Concurrency::array` 型の視覚化で `Synthetic` ノードを使用して、診断メッセージをユーザーに表示しています。

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

 ![同時実行::合成要素の拡張を伴う配列](../debugger/media/dbg_natvis_expand_synthetic.png "同時実行::合成要素の拡張を伴う配列")

### <a name="hresult-element"></a><a name="BKMK_HResult"></a>要素の結果
 要素`HResult`を使用すると、デバッガー ウィンドウで**HRESULT**に表示される情報をカスタマイズできます。 `HRValue` 要素には、カスタマイズする **HRESULT** の 32 ビット値を格納する必要があります。 要素`HRDescription`には、デバッガー ウィンドウに表示する情報が含まれています。

```xml

<HResult Name="MY_E_COLLECTION_NOELEMENTS">
  <HRValue>0xABC0123</HRValue>
  <HRDescription>No elements in the collection.</HRDescription>
</HResult>
```

### <a name="uivisualizer-element"></a><a name="BKMK_UIVisualizer"></a>UI ビジュアライザー要素
`UIVisualizer` 要素は、グラフィカル ビジュアライザー プラグインをデバッガーに登録するために使用します。 グラフィカル ビジュアライザーは、変数またはオブジェクトをそのデータ型と一致する方法で表示するダイアログ ボックスまたはその他のインターフェイスを作成します。 ビジュアライザー プラグインは[、VSPackage](../extensibility/internals/vspackages.md)として作成する必要があり、デバッガーが使用できるサービスを公開する必要があります。 *natvis*ファイルには、プラグインの名前、公開されたサービスの GUID、視覚化できる型など、プラグインの登録情報が含まれています。

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

- 属性`ServiceId` - `Id`ペアは、 を`UIVisualizer`識別します。 `ServiceId`は、ビジュアライザー パッケージが公開するサービスの GUID です。 `Id`は、サービスが複数のサービスを提供する場合に、ビジュアライザーを区別する一意の識別子です。 前の例では、同じビジュアライザー サービスが 2 つのビジュアライザーを提供します。

- この`MenuName`属性は、デバッガーの虫眼鏡アイコンの横にあるドロップダウンリストに表示するビジュアライザー名を定義します。 次に例を示します。

  ![UIVisualizer メニューのショートカット メニュー](../debugger/media/dbg_natvis_vectorvisualizer.png "UIVisualizer メニューのショートカット メニュー")

*natvis*ファイルで定義されている各型は、それを表示できる UI ビジュアライザーを明示的に一覧表示する必要があります。 デバッガーは、登録されたビジュアライザーと型エントリ内のビジュアライザー参照を照合します。 たとえば、前の例の参照に`std::vector`対して`UIVisualizer`次の型エントリを指定します。

```xml
<Type Name="std::vector&lt;int,*&gt;">
  <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}" Id="1" />
</Type>
```

 メモリ内のビットマップを表示するために`UIVisualizer`使用される[Image Watch](https://marketplace.visualstudio.com/search?term=%22Image%20Watch%22&target=VS&category=All%20categories&vsVersion=&sortBy=Relevance)拡張機能の例を確認できます。

### <a name="customvisualizer-element"></a><a name="BKMK_CustomVisualizer"></a>CustomVisualizer 要素
 `CustomVisualizer`は、Visual Studio コードで視覚化を制御するために作成する VSIX 拡張機能を指定する機能拡張ポイントです。 VSIX 拡張機能の作成の詳細については、[次](../extensibility/visual-studio-sdk.md)を参照してください。

カスタム ビジュアライザーを作成する作業は、XML Natvis 定義よりも多くの作業ですが、Natvis がサポートする内容やサポートしていない内容に関する制約はありません。 カスタム ビジュアライザーは、デバッグ対象プロセスのクエリと変更、または Visual Studio の他の部分との通信を行うことができる、デバッガーの機能拡張 API の完全なセットにアクセスできます。

 要素には`Condition`、 、 `IncludeView`、`ExcludeView`および`CustomVisualizer`属性を使用できます。

 ## <a name="limitations"></a>制限事項

Natvis のカスタマイズはクラスと構造体で動作しますが、typedef は使用できません。

Natvis は、プリミティブ型 (`int`など`bool`) またはプリミティブ型へのポインターのビジュアライザーをサポートしていません。 このシナリオでは、1 つのオプションは、ユース ケースに適した[書式指定子](../debugger/format-specifiers-in-cpp.md)を使用することです。 たとえば、コードで使用`double* mydoublearray`する場合は、デバッガーの **[ウォッチ]** ウィンドウで配列書式指定子 (最初の 100 要素`mydoublearray, [100]`を示す式など) を使用できます。
