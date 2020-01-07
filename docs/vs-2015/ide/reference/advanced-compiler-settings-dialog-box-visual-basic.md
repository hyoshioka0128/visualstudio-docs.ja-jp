---
title: '[コンパイラの詳細設定] ダイアログ ボックス (Visual Basic) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesAdvancedCompile
helpviewer_keywords:
- Advanced Compiler Settings dialog box
ms.assetid: 1f81133a-293f-4dba-bc1c-8baafb01d857
caps.latest.revision: 52
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ba666b0ff5544b185f82a66c78d6259e9f1268fd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651767"
---
# <a name="advanced-compiler-settings-dialog-box-visual-basic"></a>[ビルドの詳細設定] ダイアログ ボックス (Visual Basic)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**プロジェクト デザイナー**の **[コンパイラの詳細設定]** ダイアログ ボックスを使用して、プロジェクトの詳細なビルド構成プロパティを指定します。 このダイアログ ボックスは、Visual Basic プロジェクトにのみ適用されます。

### <a name="to-access-this-dialog-box"></a>このダイアログ ボックスを表示するには

1. **ソリューション エクスプローラー**で、 **[ソリューション]** ノードではなくプロジェクト ノードを選びます。

2. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー**が表示されたら、 **[コンパイル]** タブをクリックします。

3. [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) で、 **[構成]** と **[プラットフォーム]** を選択します。 簡易ビルド構成では、 **[構成]** と **[プラットフォーム]** の一覧は表示されません。 詳細については、「[デバッグ構成およびリリース プロジェクト構成](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e)」を参照してください。

4. **[詳細コンパイル オプション]** をクリックします。

   [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]

## <a name="optimizations"></a>最適化
 次のオプションは最適化を指定するもので、プログラム ファイルの小型化、プログラムの実行の高速化、またはビルド プロセスの時間短縮を実現できる場合があります。

 **整数オーバーフローのチェックを解除**既定では、整数のオーバーフローチェックを有効にするために、このチェックボックスはオフになっています。 整数のオーバーフロー チェックを解除するには、このチェック ボックスをオンにします。 このチェック ボックスをオンにすると、整数の計算が高速になる場合があります。 ただし、オーバーフロー チェックを解除し、データ型の容量がオーバーフローした場合、エラーが発生せずに誤った結果が格納される可能性があります。

 オーバーフロー状態がチェックされ、整数演算がオーバーフローした場合、<xref:System.OverflowException> 例外がスローされます。 オーバーフロー状態がチェックされていない場合、整数演算のオーバーフロー時に例外はスローされません。

 **最適化を有効にする**既定では、コンパイラの最適化を無効にするために、このチェックボックスはオフになっています。 コンパイラの最適化を有効にするには、このチェック ボックスをオンにします。 コンパイラを最適化すると、出力ファイルのサイズが小さくなり、動作が速くなり、処理の効率が向上します。 ただし、最適化によって出力ファイル内のコードが再配置されるため、コンパイラを最適化するとデバッグが困難になる場合があります。

 **DLL のベースアドレス**このテキストボックスには、既定の DLL ベースアドレスが16進形式で表示されます。 クラス ライブラリおよびコントロール ライブラリ プロジェクトでは、このテキスト ボックスを使用して、DLL の作成時に使用されるベース アドレスを指定できます。

 **デバッグ情報の生成**一覧から **[なし]** 、 **[フル]** 、または [ **pdb] のみ**を選択します。 **[None]** を指定すると、デバッグ情報が生成されません。 **[Full]** を指定すると、完全なデバッグ情報が生成され、 **[pdb-only]** を指定すると、PDB デバッグ情報のみが生成されます。 既定では、このオプションは **[Full]** に設定されます。

## <a name="compilation-constants"></a>コンパイル定数
 条件付きコンパイル定数は、ソース ファイルに [#Const](https://msdn.microsoft.com/library/707669e5-23f9-4f17-8622-a0d534429386) のプリプロセッサ ディレクティブを使用する場合と同じような効果がありますが、定義された定数は public で、プロジェクトのすべてのファイルに適用されます。 条件付きコンパイル定数を [#If...Then...#Else](https://msdn.microsoft.com/library/10bba104-e3fd-451b-b672-faa472530502) ディレクティブと共に使用することで、ソース ファイルを条件付きでコンパイルできます。 「[条件付きコンパイル](https://msdn.microsoft.com/library/9c35e55e-7eee-44fb-a586-dad1f1884848)」を参照してください。

 **DEBUG 定数の定義**既定では、このチェックボックスはオンになっており、デバッグ定数を設定するように指定されています。

 **TRACE 定数の定義**既定では、このチェックボックスはオンになっており、トレース定数を設定することを指定します。

 **カスタム定数**アプリケーションのカスタム定数をこのテキストボックスに入力します。 エントリは、**Name1="Value1",Name2="Value2",Name3="Value3"** の形式を使用して、コンマで区切る必要があります。

## <a name="other-settings"></a>その他の設定
 **シリアル化アセンブリの生成**この設定は、コンパイラが XML シリアル化アセンブリを作成するかどうかを指定します。 コード内で型をシリアル化するために <xref:System.Xml.Serialization.XmlSerializer> クラスを使用している場合は、シリアル化アセンブリによってそのクラスの起動効率を改善できます。 既定では、このオプションは **[自動]** に設定されています。これは、コード内の型を XML にエンコードするために <xref:System.Xml.Serialization.XmlSerializer> を使用している場合にのみシリアル化アセンブリを生成することを指定します。 **[オフ]** は、コードで <xref:System.Xml.Serialization.XmlSerializer> を使用するかどうかに関係なく、シリアル化アセンブリを生成しないことを指定します。 **[オン]** の場合、シリアル化アセンブリが必ず生成されます。 シリアル化アセンブリには、`TypeName`.XmlSerializers.dll のように名前が付けられます。

## <a name="see-also"></a>関連項目
 [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)
