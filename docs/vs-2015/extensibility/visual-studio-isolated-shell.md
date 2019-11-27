---
title: Visual Studio 分離シェル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Shell [Visual Studio], shell-based applications%2C isolated mode
- Visual Studio shell, isolated mode
- isolated shell-based applications [Visual Studio]
- Visual Studio shell, shell-based applications%2C isolated mode
- Shell [Visual Studio], isolated mode
ms.assetid: d2620e71-be9e-44c9-b5b7-03a4c8d9cf0b
caps.latest.revision: 36
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 36491d9d590a45256e297654f71652ab5de5cd98
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299726"
---
# <a name="visual-studio-isolated-shell"></a>Visual Studio の分離シェル
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の分離シェルを使用すると、他のバージョンの Visual Studio とサイドバイサイドで実行できるスタンドアロンアプリケーションを作成できます。 これは主に、Visual Studio サービスを使用できるものの、カスタマイズされた外観とブランド化を持つ特殊なツールをホストするために使用されます。 Visual Studio の機能とメニューコマンドグループは、簡単に有効または無効にすることができます。 アプリケーションタイトル、アプリケーションアイコン、およびスプラッシュスクリーンは完全にカスタマイズできます。 カスタマイズ可能な機能の一覧については、「[分離シェルのカスタマイズ](../extensibility/customizing-the-isolated-shell.md)」を参照してください。  
  
 分離シェルプロジェクトを操作するには、Visual Studio SDK をインストールする必要があります。 Visual Studio 2015 以降、ダウンロード センターから Visual Studio SDK をインストールすることはできません。 これは Visual Studio のセットアップにオプション機能として含まれるようになりました。 また、後から VS SDK をインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
 分離シェルアプリケーションを作成するには、まず Visual Studio シェル分離プロジェクトを使用します。 このプロジェクトには、独自の分離シェルアプリケーションを開発およびテストするために必要なすべてのものが含まれています。 アプリケーションを配置するセットアッププログラムを作成する準備ができたら、 [Microsoft Visual Studio Shell (Isolated) 再頒布可能パッケージ](https://go.microsoft.com/fwlink/?LinkId=616022)から分離シェル再頒布可能パッケージを取得する必要があります。  
  
> [!NOTE]
> 分離シェル再頒布可能パッケージにアクセスする前に、簡単な顧客アンケートにご記入ください。  アンケートに入力すると、再配布可能パッケージのダウンロードリンクを含む Visual Studio の接続ページに移動します。  ダウンロードリンクについては、後で Visual Studio Connect サイトにアクセスするときに、[**プログラム&#124; ] [VISUAL STUDIO 2015 統合および分離シェル**] タブで確認できます。  
  
> [!NOTE]
> 分離シェルベースのアプリケーションを配置する方法の詳細については、「[チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
## <a name="working-with-the-isolated-shell"></a>分離シェルの操作  
 Visual Studio 分離シェルアプリケーションは、Visual Studio サービスへのフルアクセスを持ち、特別なカスタマイズとブランド化をサポートしています。 分離シェルアプリケーションをカスタマイズするには、いくつかの方法があります。  
  
- Vspackage および Managed Extensibility Framework (MEF) コンポーネントパーツを使用して、他の Visual Studio 拡張機能で使用するのと同じように、分離シェルアプリケーションを拡張することができます。 詳細については、「[分離シェルの拡張](../extensibility/extending-the-isolated-shell.md)」を参照してください。  
  
- Visual Studio の機能とメニューコマンドグループを使用可能または使用できないようにするには、アプリケーションのユーザーインターフェイス (UI) プロジェクトで、vsct ファイルを更新します。  
  
- **オプション**ページやその他の Visual Studio シェルコンポーネントをアプリケーションから削除するには、アプリケーションの pkgundef ファイルを更新します。  
  
- シェルの外観や動作の他の側面を変更するには、アプリケーションの pkgdef ファイルを更新します。  
  
- シェルの一部の側面は、アプリケーションの起動時に指定することもできます。 これを行うには、呼び出しのパラメーターを appenvstub の開始エントリポイントに更新します。  
  
  カスタマイズできるさまざまな要素の詳細については、「[分離シェルの要素](../extensibility/elements-of-the-isolated-shell.md)」を参照してください。  
  
## <a name="standard-features-of-the-isolated-shell"></a>分離シェルの標準機能  
 次の機能は、Visual Studio のすべてのエディションに標準で用意されています。  
  
|機能カテゴリ|機能|  
|----------------------|-------------|  
|IDE の機能|インポート/エクスポートの設定<br /><br /> ツールボックスコントロールインストーラー<br /><br /> タスク一覧 & エラー一覧<br /><br /> [出力] ウィンドウ<br /><br /> スタート ページ<br /><br /> プロパティ ウィンドウ<br /><br /> ツールボックス<br /><br /> ソリューション エクスプローラー<br /><br /> [ブックマーク] ウィンドウ<br /><br /> クラス ビュー<br /><br /> オブジェクト ブラウザー<br /><br /> コマンド ウィンドウ<br /><br /> ドキュメント アウトライン<br /><br /> リソース ビュー<br /><br /> 外部ツール<br /><br /> Windows Communication Foundation (WCF) サービス参照の追加<br /><br /> 統合言語クエリ (LINQ) のサポート|  
|エディター/デザイナー|コード参照ツール (統合検索、ソース定義、継承)<br /><br /> IntelliSense<br /><br /> SmartTags<br /><br /> コード スニペット マネージャー<br /><br /> コード スニペット<br /><br /> リファクタリング<br /><br /> 簡単に一覧表示<br /><br /> IntelliSense のフィルター処理<br /><br /> [コード定義ウィンドウ]<br /><br /> アプリケーション デザイナー<br /><br /> Windows フォーム デザイナー<br /><br /> Windows Presentation Foundation (WPF) デザイナー|  
|デバッグ|C#式エバリュエーター<br /><br /> ローカルデバッグ<br /><br /> マネージデバッグ<br /><br /> エディット コンティニュ<br /><br /> スレッド間のデバッグ<br /><br /> 視覚エフェクト<br /><br /> [DataTips] ポップアップ<br /><br /> ネイティブデバッグ<br /><br /> スクリプトのデバッグ<br /><br /> 相互運用機能デバッグ<br /><br /> Just-in-time (JIT) デバッグ<br /><br /> マルチプロセスデバッグ<br /><br /> XSLT のデバッグ<br /><br /> ローカルプロセスにアタッチ<br /><br /> トレース ポイント<br /><br /> ブレークポイントの制約|  
|Data|サーバーエクスプローラー (簡略化されたデータのみ)<br /><br /> ローカルデータにバインドするデータ (.MDF または。MDB<br /><br /> オブジェクトへのデータバインド<br /><br /> Web サービスへのデータバインド<br /><br /> データコントロールの完全なセット<br /><br /> XML エディター<br /><br /> ローカルデータベースサーバーへのデータバインド<br /><br /> [データ ソース] ウィンドウ|  
|[Web]|HTML エディター<br /><br /> Web ブラウザー<br /><br /> Web フォーム デザイナー<br /><br /> Web サイトプロジェクト<br /><br /> Web アプリケーションプロジェクト|  
|機能拡張|Vspackage コンポーネントと MEF コンポーネントを使用する|  
  
## <a name="see-also"></a>関連項目  
 [シェル (分離または統合)](../extensibility/shell-isolated-or-integrated.md)
