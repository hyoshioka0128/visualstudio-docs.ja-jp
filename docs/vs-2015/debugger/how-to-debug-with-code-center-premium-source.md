---
title: '方法: Code Center Premium Source を使用してデバッグする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Code Center Premium
- debugging [Visual Studio], Code Center Premium
ms.assetid: 18b4769d-b007-4428-9dae-9e72c283ff0d
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: db9a3e08e14e7fadca6df9e32361c0b042f565e9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841417"
---
# <a name="how-to-debug-with-code-center-premium-source"></a>方法: Code Center Premium ソースをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] デバッガーでは、Microsoft MSDN Code Center Premium のセキュリティ保護された共有ソースをデバッグできます。  
  
 このトピックでは、Visual Studio で Code Center Premium ソース コードを設定し、デバッグする方法について説明します。  
  
### <a name="to-prepare-for-debugging-with-code-center-premium"></a>Code Center Premium を使用したデバッグを準備するには  
  
1. スマートカード リーダーを接続し、シェアード ソース イニシアティブから取得したカードを挿入します。  
  
2. Visual Studio を起動します。  
  
3. **[ツール]** メニューの **[オプション]** をクリックします。  
  
4. [ **オプション** ] ダイアログボックスで、[ **デバッグ** ] ノードを開き、[ **全般**] をクリックします。  
  
5. [ **マイコードのみを有効にする (マネージのみ)** ] チェックボックスをオフにします。  
  
6. [ **ソースサーバーのサポートを有効にする**] を選択します。  
  
7. **[元のバージョンと完全に一致するソースファイルが必要**です。  
  
8. [ **デバッグ** ] ノードで、[ **シンボル**] をクリックします。  
  
9. [ **シンボルファイル (.pdb) の場所** ] ボックスで、[ **Microsoft サーバーシンボル** ] チェックボックスをオフにし、次の場所を追加します。  
  
     `https://codepremium.msdn.microsoft.com/symbols`  
  
     `src=https://codepremium.msdn.microsoft.com/source/Visual%20Studio%202010/SP1/`  
  
   > [!NOTE]
   > パスの末尾には、末尾にスラッシュを含めてください <strong>/</strong> 。  
  
     これらの場所を一覧の最上部に移動して、これらのシンボルが最初に読み込まれるようにします。  
  
   > [!NOTE]
   > これらの Code Center Premium の場所が最初に読み込まれる場所になるように、これらが一覧の最初に配置されている必要があります。 Visual Studio 2010 では、[ **Microsoft シンボルサーバー** ] エントリの上にあるサーバーを移動することはできません。このため、このチェックボックスをオフにする必要があります。  
   > 
   >  デバッグ セッション中に Microsoft シンボルからシンボルを読み込むには、次の手順に従います。  
   > 
   > 1. [ **デバッグ** ] メニューの [ **ウィンドウ** ] をポイントし、[ **モジュール**] を選択します。  
   >    2.  シンボルの対象となるモジュールを選択し、ショートカット メニューを開きます。 [ **シンボルの読み込み元** ] を選択し、[ **Microsoft シンボルサーバー**] を選択します。  
  
10. [ **このディレクトリにシンボルサーバーの** シンボルをキャッシュする] ボックスに、 `C:\symbols` コードセンター Premium がシンボルをキャッシュできる場所を入力します。 シンボルをキャッシュすることにより、デバッグ中のパフォーマンスが大幅に向上します。  
  
     この手順を実行した後、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でのソース コードのデバッグに問題が発生する場合は、以前にキャッシュされて古くなったシンボル ファイルがキャッシュの場所にないかどうかを確認してください。 古いシンボル ファイルは削除してください。  
  
11. **[OK]** をクリックします。  
  
12. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を再起動して、設定が保持されていることを確認します。  
  
### <a name="to-debug-your-source-code-using-attach-to-process"></a>[プロセスにアタッチ] を使用してソース コードをデバッグするには  
  
1. スマートカード リーダーを接続し、シェアード ソース イニシアティブから取得したカードを挿入します。  
  
2. Visual Studio を起動します。  
  
3. Visual Studio プロジェクトを開きます。  
  
4. [ **ツール** ] メニューの [ **プロセスにアタッチ**] をクリックします。  
  
5. [ **プロセスにアタッチ** ] ダイアログボックスで、[ **選択**] をクリックします。  
  
6. [**コードの種類の選択**] ダイアログボックスの [次のコードの種類を検出] で、[**ネイティブ**]、[**マネージ**]、[**管理 (v2.0)**] の**いずれ**かを選択します。  
  
7. [ **OK]** をクリックして [ **コードの種類の選択** ] ダイアログボックスを閉じます。  
  
8. [選択 **可能なプロセス** ] ボックスで、デバッグするプロセスを選択します。  
  
9. **[アタッチ]** をクリックします。  
  
10. 証明書の確認を求めるメッセージが表示されたら、[ **OK]** をクリックします。 暗証番号 (PIN) を入力します。 Code Center Premium の使用条件を承諾します (要求された場合)。  
  
     ネットワーク速度によっては、シンボルのダウンロードに時間がかかる場合があります。 すべてのシンボルが正常にダウンロードされると、ステータス バーにその旨が表示されます。  
  
11. ソリューションのすべてのマネージド プロジェクトに対して、アタッチ手順を繰り返します。  
  
### <a name="to-debug-source-code-from-an-existing-solution"></a>既存のソリューションのソース コードをデバッグするには  
  
1. **ソリューションエクスプローラー**で、ソリューションのショートカットメニューを開き、[**プロパティ**] を選択します。  
  
2. [ソリューションプロパティページ] ダイアログボックスで、[**共通プロパティ**] ノードの [**デバッグソースファイル**] を選択します。  
  
3. ソースファイルの一覧を **含むディレクトリ** に次の場所を追加します。  
  
    `https://codepremium.msdn.microsoft.com/source/Visual%20Studio%202010/SP1/`  
  
   > [!NOTE]
   > パスの末尾には、末尾にスラッシュを含めてください <strong>/</strong> 。  
  
4. ソリューション内のマネージド プロジェクトごとに、次の操作を行います。  
  
   1. ソリューションエクスプローラーで、プロジェクトのショートカットメニューを開き、[ **プロパティ**] を選択します。  
  
   2. [ **デバッグ** ] を選択し、[ **再びアンマネージコードデバッグを有効にする**] を選択します。  
  
### <a name="to-debug-your-solution-with-code-center-premium-source"></a>Code Center Premium ソースを使用したソリューションをデバッグするには  
  
1. `Package` クラスで、パッケージ コンストラクターにブレークポイントを設定します。  
  
2. メニューの `Debug` [ **デバッグ開始**] をクリックします。  
  
3. パッケージコンストラクター内のブレークポイントにヒットしたら、[ **呼び出し履歴** ] ウィンドウにアクセスし、シンボルを読み込むアセンブリのスタックフレームを右クリックして、[ **シンボルの読み込み**] をクリックします。  
  
     ソースを読み込むには、呼び出しフレームをダブルクリックします。  
  
### <a name="to-browse-source-code-on-code-center-premium"></a>Code Center Premium のソース コードを参照するには  
  
1. スマートカード リーダーを接続し、シェアード ソース イニシアティブから取得したカードを挿入します。  
  
2. Internet Explorer を起動し、URL として「`https://codepremium.msdn.microsoft.com`」と入力します。  
  
3. 必要なソースを探します。  
  
## <a name="see-also"></a>参照  
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [Code Center Premium](https://www.microsoft.com/en-us/sharedsource/code-center-premium.aspx)
