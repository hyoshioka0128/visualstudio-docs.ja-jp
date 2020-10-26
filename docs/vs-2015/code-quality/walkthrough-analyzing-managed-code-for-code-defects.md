---
title: 'チュートリアル: マネージコードの分析によるコード障害の分析 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis, walkthroughs
- managed code, analyzing
- code analysis tool, walkthroughs
ms.assetid: 22b99f49-1924-4fb5-a421-c8b23e5d5cd4
caps.latest.revision: 47
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9478394162051fc08c33047cf1ac24275aff75e2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72609331"
---
# <a name="walkthrough-analyzing-managed-code-for-code-defects"></a>チュートリアル : マネージド コードの分析によるコード障害の検出
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、コード分析ツールを使用して、マネージプロジェクトのコード障害を分析します。

 このチュートリアルでは、コード分析を使用して .NET マネージコードアセンブリを分析し、Microsoft .NET Framework のデザインガイドラインに準拠する手順について説明します。

 このチュートリアルでは次を行います。

- コード障害の警告を分析して修正します。

## <a name="prerequisites"></a>必須コンポーネント

- [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)].

## <a name="create-a-class-library"></a>クラス ライブラリを作成する

#### <a name="to-create-a-class-library"></a>クラス ライブラリを作成するには

1. の [ **ファイル** ] メニューの [ [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] **新規作成** ] をクリックし、[ **プロジェクト**] をクリックします。

2. [ **新しいプロジェクト** ] ダイアログボックスの [ **プロジェクトの種類**] で、[ **Visual C#**] をクリックします。

3. **[テンプレート]** で、 **[クラス ライブラリ]** をクリックします。

4. [ **名前** ] テキストボックスに「 **CodeAnalysisManagedDemo** 」と入力し、[ **OK]** をクリックします。

5. プロジェクトが作成されたら、Class1.cs ファイルを開きます。

6. Class1.cs の既存のテキストを次のコードに置き換えます。

     `//CodeAnalysisManagedDemo //Class1.cs using System;  namespace testCode {          public class demo : Exception     {                  public static void Initialize(int size) { }         protected static readonly int _item;         public static int item { get { return _item; } }     } }`

7. Class1.cs ファイルを保存します。

## <a name="analyze-the-project"></a>プロジェクトを分析する

#### <a name="to-analyze-a-managed-project-for-code-defects"></a>マネージプロジェクトでコード障害を分析するには

1. **ソリューションエクスプローラー**で CodeAnalysisManagedDemo プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

     [CodeAnalysisManagedDemo のプロパティ] ページが表示されます。

3. [ **Codeanalysis**] をクリックします。

4. **[ビルドでのコード分析を有効にする (CODE_ANALYSIS 定数を定義**する)] がオンになっていることを確認します。

5. [ **この規則セットを実行** ] ドロップダウンリストで、[ **Microsoft すべての規則**] を選択します。

6. [ **ファイル** ] メニューの [ **選択した項目を保存**] をクリックし、ManagedDemo のプロパティページを閉じます。

7. [ **ビルド** ] メニューの [ **ManagedDemo のビルド**] をクリックします。

     CodeAnalysisManagedDemo プロジェクトのビルド警告は、[ **コード分析** ] ウィンドウと [ **出力** ] ウィンドウで報告されます。

     [ **コード分析** ] ウィンドウが表示されない場合は、[ **分析** ] メニューで [ **ウィンドウ** ] を選択し、[ **コード分析] を選択**します。

## <a name="correct-the-code-analysis-issues"></a>コード分析の問題を修正する

#### <a name="to-correct-code-analysis-rule-violations"></a>コード分析規則の違反を修正するには

1. **[表示]** メニューの **[エラー一覧]** をクリックします。

     選択した開発者プロファイルによっては、[**表示**] メニューの [**その他のウィンドウ**] をポイントし、[**エラー一覧**] をクリックすることが必要になる場合があります。

2. **ソリューション エクスプローラー**で、 **[すべてのファイルを表示]** をクリックします。

3. 次に、[プロパティ] ノードを展開し、AssemblyInfo.cs ファイルを開きます。

4. 警告を修正するには、次のようにします。

- [CA1014: CLSCompliantAttribute](../code-quality/ca1014-mark-assemblies-with-clscompliantattribute.md): ' demo ' によるアセンブリのマークは CLSCompliantAttribute でマークする必要があり、その値は true である必要があります。

  - `using``System;`AssemblyInfo.cs ファイルにコードを追加します。

       次に、コードを `[assembly: CLSCompliant(true)]` AssemblyInfo.cs ファイルの末尾に追加します。

       プロジェクトをリビルドします。

- [CA1032: 標準の例外コンストラクターを実装](../code-quality/ca1032-implement-standard-exception-constructors.md)します: Microsoft Design: 次のコンストラクターをこのクラスに追加します: パブリックデモ (String)

  - コンストラクター `public demo (String s) : base(s) { }` をクラスに追加 `demo` します。

- [CA1032: 標準の例外コンストラクターを実装](../code-quality/ca1032-implement-standard-exception-constructors.md)します: Microsoft Design: 次のコンストラクターをこのクラスに追加します: パブリックデモ (文字列、例外)

  - コンストラクター `public demo (String s, Exception e) : base(s, e) { }` をクラスに追加 `demo` します。

- [CA1032: 標準の例外コンストラクターを実装](../code-quality/ca1032-implement-standard-exception-constructors.md)します: Microsoft Design: 次のコンストラクターをこのクラスに追加します: 保護されたデモ (SerializationInfo、StreamingContext)

  - `using System.Runtime.Serialization;`Class1.cs ファイルの先頭にコードを追加します。

       次に、コンストラクターを追加します。 `protected demo (SerializationInfo info, StreamingContext context) : base(info, context) { } to the class demo.`

       プロジェクトをリビルドします。

- [CA1032: 標準の例外コンストラクターを実装](../code-quality/ca1032-implement-standard-exception-constructors.md)します: Microsoft Design: 次のコンストラクターをこのクラスに追加します: public demo ()

  - コンストラクター `public demo () : base() { }` をクラスに追加 `demo` **します。**

       プロジェクトをリビルドします。

- [CA1709: 識別子](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)の大文字と小文字が正しく指定されている必要があります。名前空間名 ' testcode ' を ' testcode ' に変更して、名前空間の名前を修正してください。

  - 名前空間の大文字と小文字の区別 `testCode` をに変更し `TestCode` ます。

- [CA1709: 識別子は正しく入力されている必要があり](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)ます: Microsoft. 名前付け: ' demo ' に変更して、型名 ' demo ' の大文字と小文字の指定を訂正してください。

  - メンバーの名前をに変更 `Demo` します。

- [CA1709: 識別子は大文字にする必要があり](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)ます: Microsoft. 名前付け: ' item ' に変更して、メンバー名 ' item ' の大文字と小文字の指定を訂正してください。

  - メンバーの名前をに変更 `Item` します。

- [CA1710: 識別子は正しいサフィックスを持つ必要があり](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)ます: Microsoft. 名前付け: ' testcode. demo ' を ' Exception ' で終了するには名前を変更してください。

  - クラスの名前とそのコンストラクターをに変更し `DemoException` ます。

- [CA2210: アセンブリには有効な厳密な名前が必要](../code-quality/ca2210-assemblies-should-have-valid-strong-names.md)です。厳密な名前のキーを持つ ' ManagedDemo ' に署名してください。

  - [ **プロジェクト** ] メニューの [ **ManagedDemo のプロパティ**] をクリックします。

       プロジェクトのプロパティが表示されます。

       [ **署名**] をクリックします。

       [ **アセンブリの署名** ] チェックボックスをオンにします。

       [ **文字列名キーファイルを選択** してください] ボックスの一覧で、を選択し **\<New…>** ます。

       **[厳密な名前キーの作成]** ダイアログ ボックスが表示されます。

       [ **キーファイル名**] に「testkey」と入力します。

       パスワードを入力し、[ **OK]** をクリックします。

       [ **ファイル** ] メニューの [ **選択した項目を保存**] をクリックし、プロパティページを閉じます。

       プロジェクトをリビルドします。

- [CA2237: iserializable 型を SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md): Microsoft. Usage でマークします。この型は iserializable を実装するため、型 ' demo ' に [Serializable] 属性を追加します。

  - `[Serializable ()]`属性をクラスに追加 `demo` します。

       プロジェクトをリビルドします。

  変更が完了すると、Class1.cs ファイルは次のようになります。

```
//CodeAnalysisManagedDemo
//Class1.cs
using System;
using System.Runtime.Serialization;

namespace TestCode
{

    [Serializable()]
    public class DemoException : Exception
    {
        public DemoException () : base() { }
        public DemoException(String s) : base(s) { }
        public DemoException(String s, Exception e) : base(s, e) { }
        protected DemoException(SerializationInfo info, StreamingContext context) : base(info, context) { }

        public static void Initialize(int size) { }
        protected static readonly int _item;
        public static int Item { get { return _item; } }
    }
}
```

## <a name="exclude-code-analysis-warnings"></a>コード分析の警告を除外する

#### <a name="to-exclude-code-defect-warnings"></a>コード障害の警告を除外するには

1. 残りの各警告について、次の操作を行います。

   1. [コード分析] ウィンドウで、警告を選択します。

   2. [ **アクション**] を選択し、[ **メッセージの非**表示] をクリックして、[ **プロジェクトの抑制ファイル**] をクリックします。

      詳細については、「[方法: メニュー項目を使用して警告を非](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md)表示にする」を参照してください。

2. プロジェクトをリビルドします。

    プロジェクトがビルドされ、警告やエラーは発生しません。
