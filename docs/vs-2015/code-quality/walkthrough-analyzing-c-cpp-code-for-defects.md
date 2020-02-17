---
title: 'チュートリアル: CC++コードを分析して欠陥を分析するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- C/C++, code analysis
- code analysis, walkthroughs
- code, analyzing C/C++
- code analysis tool, walkthroughs
ms.assetid: eaee55b8-85fe-47c7-a489-9be0c46ae8af
caps.latest.revision: 37
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: c822dbcc6a1ece2040da22a3442dd584c3926d97
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77272437"
---
# <a name="walkthrough-analyzing-cc-code-for-defects"></a>チュートリアル : C/C++ コード分析による障害の検出
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、C/C++ C++ code 用のコード分析ツールを使用して、コードの欠陥の可能性について c/コードを分析する方法について説明します。  
  
 このチュートリアルでは、コード分析を使用して C/C++コードを分析し、コードの欠陥の可能性を確認する手順を説明します。  
  
 次の手順を実行します。  
  
- ネイティブコードでコード分析を実行します。  
  
- コード障害の警告を分析します。  
  
- 警告をエラーとして扱います。  
  
- コード障害分析を改善するためにソースコードに注釈を付けます。  
  
## <a name="prerequisites"></a>前提条件  
  
- [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] または [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]。  
  
- [デモサンプル](../code-quality/demo-sample.md)のコピー。  
  
- C/C++の基本を理解している。  
  
### <a name="to-run-code-defect-analysis-on-native-code"></a>ネイティブコードでコードの欠陥分析を実行するには  
  
1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]でデモソリューションを開きます。  
  
     デモソリューションで**ソリューションエクスプローラー**が設定されるようになりました。  
  
2. **[ビルド]** メニューで、 **[ソリューションのリビルド]** をクリックします。  
  
     エラーや警告なしでソリューションがビルドされます。  
  
3. **ソリューションエクスプローラー**で、codedefects プロジェクトを選択します。  
  
4. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
     **[Codedefects プロパティページ]** ダイアログボックスが表示されます。  
  
5. **[コード分析]** をクリックします。  
  
6. **[C/C++ビルド時にコード分析を有効にする]** チェックボックスをオンにします。  
  
7. CodeDefects プロジェクトをリビルドします。  
  
     コード分析の警告が**エラー一覧**に表示されます。  
  
### <a name="to-analyze-code-defect-warnings"></a>コード障害の警告を分析するには  
  
1. **[表示]** メニューの **[エラー一覧]** をクリックします。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で選択した開発者プロファイルによっては、 **[表示]** メニューの **[その他のウィンドウ]** をポイントし、 **[エラー一覧]** をクリックすることが必要になる場合があります。  
  
2. **エラー一覧**で、次の警告をダブルクリックします。  
  
     警告 C6230: 意味の異なる型の間の暗黙的なキャストです: ブール値のコンテキストで HRESULT を使用しています。  
  
     コードエディターでは、関数 `bool``ProcessDomain()`で警告の原因となった行が表示されます。 この警告は、ブール型の結果が想定される ' if ' ステートメントで HRESULT が使用されていることを示します。  
  
3. SUCCEEDED マクロを使用して、この警告を修正します。 コードは次のコードのようになります。  
  
    ```  
    if (SUCCEEDED (ReadUserAccount()) )  
    ```  
  
4. **エラー一覧**で、次の警告をダブルクリックします。  
  
     警告 C6282: 不適切な演算子です: テストコンテキストで定数に割り当てられています。 Was = = 意図されていますか?  
  
5. 等しいかどうかをテストして、この警告を修正します。 コードは次のコードのようになります。  
  
    ```  
    if ((len == ACCOUNT_DOMAIN_LEN) || (g_userAccount[len] != '\\'))  
    ```  
  
### <a name="to-treat-warning-as-an-error"></a>警告をエラーとして扱うには  
  
1. バグの .cpp ファイルで、次の `#pragma` ステートメントをファイルの先頭に追加し、警告 C6001 をエラーとして扱います。  
  
    ```  
    #pragma warning (error: 6001)  
    ```  
  
2. CodeDefects プロジェクトをリビルドします。  
  
     **エラー一覧**では、C6001 がエラーとして表示されるようになりました。  
  
3. `i` を初期化し、を0に `j` して、**エラー一覧**の残りの2つの C6001 エラーを修正します。  
  
4. CodeDefects プロジェクトをリビルドします。  
  
     プロジェクトがビルドされ、警告やエラーは発生しません。  
  
### <a name="to-correct-the-source-code-annotation-warnings-in-annotationc"></a>注釈のソースコードの注釈の警告を修正するには  
  
1. ソリューションエクスプローラーで、[注釈] プロジェクトを選択します。  
  
2. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
     **[注釈のプロパティページ]** ダイアログボックスが表示されます。  
  
3. **[コード分析]** をクリックします。  
  
4. **[C/C++ビルド時にコード分析を有効にする]** チェックボックスをオンにします。  
  
5. Annotations プロジェクトをリビルドします。  
  
6. **エラー一覧**で、次の警告をダブルクリックします。  
  
     警告 C6011: NULL ポインター ' newNode ' を逆参照しています。  
  
     この警告は、呼び出し元が戻り値を確認するのに失敗したことを示します。 この場合、 **allocatenode**呼び出しによって NULL 値が返される可能性があります (allocatenode 関数宣言については、「annotations ヘッダーファイル」を参照してください)。  
  
7. Annotations ファイルを開きます。  
  
8. この警告を解決するには、' if ' ステートメントを使用して戻り値をテストします。 コードは次のコードのようになります。  
  
     `if (NULL != newNode)`  
  
     `{`  
  
     `newNode->data = value;`  
  
     `newNode->next = 0;`  
  
     `node->next = newNode;`  
  
     `}`  
  
9. Annotations プロジェクトをリビルドします。  
  
     プロジェクトがビルドされ、警告やエラーは発生しません。  
  
### <a name="to-use-source-code-annotation"></a>ソースコードの注釈を使用するには  
  
1. 次の例に示すように、Pre および Post 条件を使用して、関数 `AddTail` の仮パラメーターと戻り値に注釈を設定します。  
  
     `[returnvalue:SA_Post (Null=SA_Maybe)] LinkedList* AddTail`  
  
     `(`  
  
     `[SA_Pre(Null=SA_Maybe)] LinkedList* node,`  
  
     `int value`  
  
     `)`  
  
2. コメントプロジェクトを再構築します。  
  
3. **エラー一覧**で、次の警告をダブルクリックします。  
  
     警告 C6011: NULL ポインター ' node ' を逆参照しています。  
  
     この警告は、関数に渡されたノードが null である可能性があることを示し、警告が発生した行番号を示します。  
  
4. この警告を解決するには、' if ' ステートメントを使用して戻り値をテストします。 コードは次のコードのようになります。  
  
    ```  
    . . .  
    LinkedList *newNode = NULL;   
    if (NULL == node)  
    {  
         return NULL;  
        . . .  
    }  
    ```  
  
5. コメントプロジェクトを再構築します。  
  
     プロジェクトがビルドされ、警告やエラーは発生しません。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: マネージド コードの分析によるコード障害の検出](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)
