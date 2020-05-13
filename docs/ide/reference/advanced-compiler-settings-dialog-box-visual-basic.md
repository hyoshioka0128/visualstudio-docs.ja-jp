---
title: '[ビルドの詳細設定] ダイアログ ボックス (Visual Basic)'
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesAdvancedCompile
helpviewer_keywords:
- Advanced Compiler Settings dialog box
ms.assetid: 1f81133a-293f-4dba-bc1c-8baafb01d857
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9ebc2da5e71dbdee13df4cf658f3681804879f58
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596932"
---
# <a name="advanced-compiler-settings-dialog-box-visual-basic"></a>[ビルドの詳細設定] ダイアログ ボックス (Visual Basic)

**プロジェクト デザイナー**の **[コンパイラの詳細設定]** ダイアログ ボックスを使用して、プロジェクトの詳細なビルド構成プロパティを指定します。 このダイアログ ボックスは、Visual Basic プロジェクトにのみ適用されます。

## <a name="to-access-this-dialog-box"></a>このダイアログ ボックスを表示するには

1. **ソリューション エクスプローラー**で、 **[ソリューション]** ノードではなくプロジェクト ノードを選びます。

2. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー**が表示されたら、 **[コンパイル]** タブをクリックします。

3. [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) で、 **[構成]** と **[プラットフォーム]** を選択します。 簡易ビルド構成では、 **[構成]** と **[プラットフォーム]** の一覧は表示されません。 詳細については、[デバッグ構成とリリース構成を設定する](../../debugger/how-to-set-debug-and-release-configurations.md)」を参照してください。

4. **[詳細コンパイル オプション]** をクリックします。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="optimizations"></a>最適化

次のオプションは最適化を指定するもので、プログラム ファイルの小型化、プログラムの実行の高速化、またはビルド プロセスの時間短縮を実現できる場合があります。

**整数オーバーフローのチェックを解除**

既定では、このチェック ボックスはオフになっており、整数のオーバーフロー チェックが有効になります。 整数のオーバーフロー チェックを解除するには、このチェック ボックスをオンにします。 このチェック ボックスをオンにすると、整数の計算が高速になる場合があります。 ただし、オーバーフロー チェックを解除し、データ型の容量がオーバーフローした場合、エラーが発生せずに誤った結果が格納される可能性があります。

オーバーフロー状態がチェックされ、整数演算がオーバーフローした場合、<xref:System.OverflowException> 例外がスローされます。 オーバーフロー状態がチェックされていない場合、整数演算のオーバーフロー時に例外はスローされません。

**最適化を有効にする**

既定では、このチェック ボックスはオフになっており、コンパイラの最適化は無効になります。 コンパイラの最適化を有効にするには、このチェック ボックスをオンにします。 コンパイラを最適化すると、出力ファイルのサイズが小さくなり、動作が速くなり、処理の効率が向上します。 ただし、最適化によって出力ファイル内のコードが再配置されるため、コンパイラを最適化するとデバッグが困難になる場合があります。

 **DLL ベース アドレス**

このテキスト ボックスには、既定の DLL ベース アドレスが 16 進形式で表示されます。 クラス ライブラリおよびコントロール ライブラリ プロジェクトでは、このテキスト ボックスを使用して、DLL の作成時に使用されるベース アドレスを指定できます。

 **デバッグ情報を作成**

リストから **[None]** 、 **[Full]** 、または **[pdb-only]** を選択します。 **[None]** を指定すると、デバッグ情報が生成されません。 **[Full]** を指定すると、完全なデバッグ情報が生成され、 **[pdb-only]** を指定すると、PDB デバッグ情報のみが生成されます。 このオプションの既定値は **[Full]** です。

## <a name="compilation-constants"></a>コンパイル定数

条件付きコンパイル定数は、ソース ファイルに [#Const](/dotnet/visual-basic/language-reference/directives/const-directive) のプリプロセッサ ディレクティブを使用する場合と同じような効果がありますが、定義された定数は public で、プロジェクトのすべてのファイルに適用されます。 条件付きコンパイル定数を [#If...Then...#Else](/dotnet/visual-basic/language-reference/directives/if-then-else-directives) ディレクティブと共に使用することで、ソース ファイルを条件付きでコンパイルできます。 「[条件付きコンパイル](/dotnet/visual-basic/programming-guide/program-structure/conditional-compilation)」を参照してください。

 **定数 DEBUG の定義**

既定では、このチェック ボックスはオンになり、DEBUG 定数を設定するように指定されます。

 **定数 TRACE の定義**

既定では、このチェック ボックスはオンになり、TRACE 定数を設定するように指定されます。

 **カスタム定数**

このテキスト ボックスには、アプリケーションのカスタム定数を入力します。 エントリは、**Name1="Value1",Name2="Value2",Name3="Value3"** の形式を使用して、コンマで区切る必要があります。

## <a name="other-settings"></a>その他の設定

**シリアル化アセンブリの生成**

この設定は、コンパイラが XML シリアル化アセンブリを作成するかどうかを指定します。 コード内で型をシリアル化するために <xref:System.Xml.Serialization.XmlSerializer> クラスを使用している場合は、シリアル化アセンブリによってそのクラスの起動効率を改善できます。 このオプションの既定値は **[自動]** です。 **[自動]** の場合、コード内の型を XML にエンコードするために <xref:System.Xml.Serialization.XmlSerializer> を使用している場合にのみシリアル化アセンブリを生成することが指定されます。 **[オフ]** は、コードで <xref:System.Xml.Serialization.XmlSerializer> を使用するかどうかに関係なく、シリアル化アセンブリを生成しないことを指定します。 **[オン]** の場合、シリアル化アセンブリが必ず生成されます。 シリアル化アセンブリには、`TypeName`.XmlSerializers.dll のように名前が付けられます。

## <a name="see-also"></a>関連項目

- [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)
