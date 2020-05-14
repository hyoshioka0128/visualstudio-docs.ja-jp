---
title: VSIX カラー コンパイラ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f414a56bb05a23b6efef19aa7c99292b8a40038a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703895"
---
# <a name="vsix-color-compiler"></a>VSIX カラー コンパイラ
Visual Studio 拡張機能の色コンパイラ ツールは、既存の Visual Studio テーマの色を表す .xml ファイルを受け取り、.pkgdef ファイルに隠して、それらの色を Visual Studio で使用できるようにコンソール アプリケーションです。 xml ファイル間の違いを比較するのは簡単なので、このツールはソース管理のカスタム カラーを管理する場合に便利です。 ビルド環境にフックして、ビルドの出力を有効な .pkgdef ファイルにすることもできます。

 **テーマ XML スキーマ**

 完全なテーマ .xml ファイルは次のようになります。

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

 テーマ\<>要素は、テーマ全体を定義します。 テーマには、少なくとも 1\<つのカテゴリ>要素が含まれている必要があります。 テーマ要素は次のように定義されます。

```xml
<Theme Name="name" GUID="guid">
      <!-- one or more Category elements -->
</Theme>
```

|||
|-|-|
|**属性**|**定義**|
|名前|[必須]テーマの名前|
|GUID|[必須]テーマの GUID (GUID の書式設定と一致する必要があります)|

 Visual Studio のカスタム色を作成する場合、次のテーマに対してこれらの色を定義する必要があります。 特定のテーマに色が存在しない場合、Visual Studio は、淡いテーマから不足している色を読み込もうとします。

|||
|-|-|
|**テーマ名**|**テーマ GUID**|
|浅煎り|{de3dbbcd-f642-433c-8353-8f1df4370aba}|
|ダーク|{1ded0138-47ce-435e-84ef-9ec1f439b749}|
|青|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|
|ハイコントラスト|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|

 **カテゴリ**

 カテゴリ\<>要素は、テーマの色のコレクションを定義します。 カテゴリ名は論理的なグループ化を提供し、できるだけ狭く定義する必要があります。 カテゴリには、少なくとも 1\<つの Color>要素が含まれている必要があります。 カテゴリ要素は次のように定義されます。

```xml
<Category Name="name" GUID="guid">
      <!-- one or more Color elements -->
 </Category>
```

|||
|-|-|
|**属性**|**定義**|
|名前|[必須]カテゴリの名前|
|GUID|[必須]カテゴリの GUID (GUID の書式と一致する必要があります)|

 **Color**

 色\<>要素は、コンポーネントまたは UI の状態の色を定義します。 色の推奨される名前付けスキームは、[UI の種類] [状態]です。 「色」という言葉は冗長なので使用しないでください。 色は、要素の種類と、色が適用される状態、つまり "状態" を明確に示す必要があります。 色は空にしてはならず、背景>と\<\<前景>要素の一方または両方を含める必要があります。 色要素は次のように定義されます。

```xml
<Color Name="name">
        <Background /> <!-- zero or one Background element -->
        <Foreground /> <!-- zero or one Foreground element -->
 </Color>
```

|||
|-|-|
|**属性**|**定義**|
|名前|[必須]色の名前|

 **背景および/または前景**

 背景\<>と\<前景>要素は、UI 要素の背景色または前景の色の値と種類を定義します。 これらの要素には子がありません。

```xml
<Background Type="type" Source="int" />
<Foreground Type="type" Source="int" />
```

|||
|-|-|
|**属性**|**定義**|
|種類|[必須]色の種類。 次のいずれかを指定できます。<br /><br /> *CT_INVALID:* 色が無効か、設定されていません。<br /><br /> *CT_RAW:* 生の ARGB 値。<br /><br /> *CT_COLORINDEX:* 使用しないでください。<br /><br /> *CT_SYSCOLOR:* SysColor から Windows のシステムの色。<br /><br /> *CT_VSCOLOR:*__VSSYSCOLOREXのビジュアル スタジオの色。<br /><br /> *CT_AUTOMATIC:* 自動色。<br /><br /> *CT_TRACK_FOREGROUND:* 使用しないでください。<br /><br /> *CT_TRACK_BACKGROUND:* 使用しないでください。|
|source|[必須]16 進数で表される色の値|

 __VSCOLORTYPE列挙体でサポートされるすべての値は、Type 属性のスキーマでサポートされます。 ただし、CT_RAWとCT_SYSCOLORのみを使用することをお勧めします。

 **すべて一緒に**

 これは、有効なテーマ .xml ファイルの簡単な例です。

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

 オプションの\<引数>> \<PkgDef ファイル>\<のファイルを生成します。

 **引数**

||||
|-|-|-|
|**スイッチ名**|**メモ**|**必須またはオプション**|
|名前なし (.xml ファイル)|これは、最初の名前のないパラメータで、変換する XML ファイルへのパスです。|必須|
|名前なし (.pkgdef ファイル)|これは、2 番目の無名パラメーターで、生成された .pkgdef ファイルの出力パスです。<br /><br /> デフォルト: \<XML ファイル名>.pkgdef|Optional|
|/noLogo|このフラグを設定すると、製品および著作権情報の印刷が停止します。|Optional|
|/?|ヘルプ情報を印刷します。|Optional|
|/help|ヘルプ情報を印刷します。|Optional|

 **使用例**

- D:\xml\色.xml D:\pkgdef\色.pkgdef

- D:\xml\色.xml /noLogo

## <a name="notes"></a>Notes

- このツールでは、最新バージョンの VC++ ランタイムがインストールされている必要があります。

- 単一のファイルのみがサポートされます。 フォルダ パスによる一括変換はサポートされていません。

## <a name="sample-output"></a>サンプル出力
 このツールによって生成される .pkgdef ファイルは、次のキーのようになります。

```
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff

[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff
```
