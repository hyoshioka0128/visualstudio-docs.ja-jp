---
title: VSIX 色コンパイラ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5059a15c483f648c2248321c7ba8271a634d0c69
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536098"
---
# <a name="vsix-color-compiler"></a>VSIX カラー コンパイラ
Visual Studio 拡張機能の色コンパイラツールは、既存の Visual Studio テーマの色を表す .xml ファイルを取得し、それを pkgdef ファイルに反映して、それらの色を Visual Studio で使用できるようにするコンソールアプリケーションです。 このツールは、.xml ファイル間の違いを簡単に比較できるため、ソース管理でカスタムカラーを管理する場合に便利です。 また、ビルド環境にフックして、ビルドの出力が有効な pkgdef ファイルであるようにすることもできます。

 **テーマ XML スキーマ**

 完成したテーマ .xml ファイルは次のようになります。

```xml
<Themes>
      <!—one or Theme elements -->
      <Theme>
        <!-- one or more Category elements -->
        <Category>
          <!-- one or more Color elements -->
          <Color>
            <!-- zero or one Background element -->
            <Background />
            <!-- zero or one Foreground element -->
            <Foreground />
          </Color>
        </Category>
      </Theme>
</Themes>
```

 **テーマ**

 要素は、 \<Theme> テーマ全体を定義します。 テーマには、少なくとも1つの要素が含まれている必要があり \<Category> ます。 テーマ要素は次のように定義されます。

```xml
<Theme Name="name" GUID="guid">
      <!-- one or more Category elements -->
</Theme>
```

|**属性**|**定義**|
|-|-|
|名前|必要テーマの名前|
|GUID|必要テーマの GUID (GUID の書式設定と一致する必要があります)|

 Visual Studio のカスタム色を作成する場合は、次のテーマに対してこれらの色を定義する必要があります。 特定のテーマに対して色が存在しない場合、Visual Studio は、淡色テーマから不足している色の読み込みを試みます。

|**テーマ名**|**テーマ GUID**|
|-|-|
|白|{de3dbbcd-f642-433c-8353-8f1df4370aba}|
|黒|{1ded0138-47ce-435e-84ef-9ec1f439b749}|
|青|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|
|ハイコントラスト|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|

 **カテゴリ**

 要素は、 \<Category> テーマの色のコレクションを定義します。 カテゴリ名は論理グループを提供します。可能な限り狭くするように定義する必要があります。 カテゴリには、少なくとも1つの要素が含まれている必要があり \<Color> ます。 Category 要素は次のように定義されます。

```xml
<Category Name="name" GUID="guid">
      <!-- one or more Color elements -->
 </Category>
```

|**属性**|**定義**|
|-|-|
|名前|必要カテゴリの名前|
|GUID|必要カテゴリの GUID (GUID の書式設定と一致する必要があります)|

 **色**

 要素は、 \<Color> コンポーネントまたは UI の状態の色を定義します。 色には [UI の種類] [状態] という名前を付けることをお勧めします。 重複しているため、"color" という語は使用しないでください。 色は、要素の種類と、その色が適用される状況 ("状態") を明確に示す必要があります。 色を空にすることはできません。また、要素と要素のいずれかまたは両方を含める必要があり \<Background> \<Foreground> ます。 Color 要素は次のように定義されます。

```xml
<Color Name="name">
        <Background /> <!-- zero or one Background element -->
        <Foreground /> <!-- zero or one Foreground element -->
 </Color>
```

|**属性**|**定義**|
|-|-|
|名前|必要色の名前|

 **背景または前景**

 \<Background>要素と \<Foreground> 要素は、UI 要素の背景または前景の色の値と型を定義します。 これらの要素には子がありません。

```xml
<Background Type="type" Source="int" />
<Foreground Type="type" Source="int" />
```

|**属性**|**定義**|
|-|-|
|Type|必要色の種類。 次のいずれかを指定できます。<br /><br /> *CT_INVALID:* 色が無効であるか、設定されていません。<br /><br /> *CT_RAW:* 生の ARGB 値。<br /><br /> *CT_COLORINDEX:* 使用しないでください。<br /><br /> *CT_SYSCOLOR:* SysColor からの Windows システム色。<br /><br /> *CT_VSCOLOR:*__VSSYSCOLOREX からの Visual Studio の色。<br /><br /> *CT_AUTOMATIC:* 自動色。<br /><br /> *CT_TRACK_FOREGROUND:* 使用しないでください。<br /><br /> *CT_TRACK_BACKGROUND:* 使用しないでください。|
|source|必要16進数で表される色の値|

 __VSCOLORTYPE 列挙体によってサポートされるすべての値は、Type 属性のスキーマでサポートされています。 ただし、CT_RAW と CT_SYSCOLOR のみを使用することをお勧めします。

 **すべてをまとめて**

 有効な theme ファイルの簡単な例を次に示します。

```xml
<Themes>
  <Theme Name="Light" GUID="{de3dbbcd-f642-433c-8353-8f1df4370aba}">
    <Category Name="MyCategory" GUID="{0A96238B-70CE-4479-9170-EECEAA3FCD58}">
      <Color Name="MyActiveBorder">
        <Background Type="CT_RAW" Source="FFCCCEDB" />
      </Color>
    </Category>
  </Theme>
</Themes>
```

## <a name="how-to-use-the-tool"></a>ツールの使用方法
 **構文**

 VsixColorCompiler \<XML file> \<PkgDef file>\<Optional Args>

 **引数**

|**スイッチ名**|**ノート**|**必須またはオプション**|
|-|-|-|
|名前のない (.xml ファイル)|これは、最初の名前のないパラメーターで、は変換する XML ファイルへのパスです。|必須|
|名前のない (pkgdef ファイル)|これは2番目の名前のないパラメーターで、は生成された pkgdef ファイルの出力パスです。<br /><br /> 既定値: \<XML Filename> pkgdef|オプション|
|/noLogo|このフラグを設定すると、製品および著作権情報は印刷されなくなります。|オプション|
|/?|ヘルプ情報を印刷します。|オプション|
|/help|ヘルプ情報を印刷します。|オプション|

 **例**

- VsixColorCompiler D:\xml\colors.xml D:\pkgdef\colors.pkgdef

- VsixColorCompiler D:\xml\colors.xml/noLogo

## <a name="notes"></a>メモ

- このツールを使用するには、最新バージョンの VC + + ランタイムがインストールされている必要があります。

- サポートされているファイルは1つだけです。 フォルダーパスを使用した一括変換はサポートされていません。

## <a name="sample-output"></a>サンプル出力
 ツールによって生成される pkgdef ファイルは、次のキーに似ています。

```
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff

[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff
```
