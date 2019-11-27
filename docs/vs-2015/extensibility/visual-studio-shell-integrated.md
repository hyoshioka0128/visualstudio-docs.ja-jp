---
title: Visual Studio Shell (Integrated) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, integrated mode features
- Shell [Visual Studio], integrated mode features
ms.assetid: 0b40d495-f17f-4bb9-ace8-b365a7172784
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 78ccba3ab8c2dda531614fa791eac3100813840a
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299690"
---
# <a name="visual-studio-shell-integrated"></a>Visual Studio Shell (統合)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 統合シェルには、統合開発環境 (IDE)、デバッガー、およびソース管理の統合が含まれています。 プログラミング言語は含まれていません。 ただし、統合シェルには、プログラミング言語を追加するためのフレームワークが用意されています。  
  
 Visual Studio 統合シェルは、実際には、Visual Studio の分離シェルと、統合されたシェル固有のコンポーネントを含む追加のインストールを組み合わせたものです。  統合シェルアプリケーションには[Microsoft Visual Studio Shell (Isolated) 再](https://go.microsoft.com/fwlink/?LinkId=616022)頒布可能パッケージからの分離シェル再頒布可能パッケージと、 [Microsoft Visual Studio Shell (Integrated) 再](https://go.microsoft.com/fwlink/?LinkId=616021)頒布可能パッケージからの統合シェル再配布可能パッケージの両方を含める必要があります。  
  
> [!NOTE]
> 分離された、または統合されたシェル再頒布可能パッケージにアクセスする前に、簡単なお客様のアンケートにご記入ください。  アンケートに入力すると、再配布可能パッケージのダウンロードリンクを含む Visual Studio の接続ページに移動します。  ダウンロードリンクについては、後で Visual Studio Connect サイトにアクセスするときに、[**プログラム&#124; ] [VISUAL STUDIO 2015 統合および分離シェル**] タブで確認できます。  
  
 統合シェルアプリケーションを完全なバージョンの Visual Studio と同じコンピューターにインストールすると、アプリケーションのコンポーネントが Visual Studio に直接統合されます。  
  
## <a name="features-in-the-integrated-shell"></a>統合シェルの機能  
  
|||  
|-|-|  
|機能分野|機能|  
|言語サポート|-なし|  
|IDE|<ul><li>設定<br /><br /> <ul><li>設定の作成</li><li>設定のインポートとエクスポート</li><li>設定をリセットする</li></ul></li><li>**ツールボックス**の統合</li><li>**タスク一覧**の統合</li><li>ヘルプの統合</li><li>**[オプション]** ダイアログボックス</li><li>フォントおよび色の管理</li><li>**出力**ウィンドウ</li><li>**コマンド**ウィンドウ</li><li>ウィンドウの管理</li><li>コマンド、メニュー、およびキーのバインド</li><li>ドメイン固有言語 (DSL) ランタイム</li></ul>|  
|プロジェクトシステムとプロジェクトの種類|-ソリューションとソリューションフォルダー<br />-ソリューション構成マネージャー<br />-項目管理<br />-単一プロジェクトと複数プロジェクトのソリューション<br />-アプリケーションデザイナー (簡略化されたプロジェクトプロパティ)<br />-Web 参照の追加<br />-サービス参照の追加<br />-単一プロジェクト<br />-Web サイトプロジェクトの種類<br />-Web アプリケーションプロジェクト|  
|ビルド|-IDE でのカスタムビルドステップ<br />-知的財産 (IP) 保護の事前コンパイル<br />-コード署名<br />     MSBuild|  
|エディター|-コード参照ツール (統合検索、ソース定義、継承)<br />-コードナビゲーション<br />-IntelliSense<br />-SmartTags<br />-リファクタリング<br />-非常に一覧表示<br />-IntelliSense のフィルター処理<br />-   **コード定義**ウィンドウ|  
|Designer|-Windows Presentation Foundation デザイナー<br />-Windows フォームデザイナー<br />-Web デザイナーおよび HTML エディター|  
|Data|-   **サーバーエクスプローラー** (簡: データのみ)。 注 1 を参照してください。<br />-   **データソース** ウィンドウ<br />-データコントロールの完全なセット<br />-XML エディター<br />-ローカルデータソース () にデータをバインドします。MDF または。MDB<br />-オブジェクトへのデータバインド<br />-Web サービスへのデータバインド<br />-ローカルデータベースサーバーへのデータバインド<br />-リモートデータベースサーバーへのデータバインド<br />-リモートデータ用の DDL ツール<br />-   **サーバーエクスプローラー**の拡張機能 ([!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] サンプル)|  
|デバッガー|-ローカルデバッグ。 メモ2を参照してください。<br />-マネージデバッグ<br />-ローカルデバッグ<br />-ローカルプロセスにアタッチ<br />-リモートプロセスにアタッチ<br />-匿名デリゲート<br />-アプリケーションドメイン<br />-ASPX デバッグ<br />-属性<br />-Func-eval の実行中に中断します。<br />-ブレークポイント<br />-ブレークポイントの制約<br />-呼び出し履歴<br />-   **コマンド**ウィンドウ<br />-スレッド間のデバッグ<br />-データのヒント<br />-データビジュアライザー<br />-マネージデバッグアシスタント (Mda) のデバッガーサポート<br />-フォワーダーの型のサポート<br />: OTB の DTEEvents サポート<br />-JMC ステッパ<br />-デバッガー AppID テスト (DBGCLR)<br />-デバッガープロファイル<br />-デバッガーのツールとオプション<br />-デバッグ反復子<br />-デザイン時の式の評価<br />- C#式エバリュエーター<br />-逆アセンブリ<br />-エディットコンティニュ<br />-式エバリュエーターウィンドウ (ウォッチ、ローカル、自動変数)<br />-Exception ヘルパー<br />-例外<br />-実行<br />- ジェネリック<br />-正しいソースを取得しています<br />-HPC/クラスターデバッグ<br />-統合された複数言語のデバッグ<br />-相互運用機能デバッグ<br />-Just-in-time デバッグ<br />-ローカルデバッグ<br />-マネージデバッグ<br />-手動制御 (プロセスウィンドウ)<br />-メモリ<br />-ミニダンプサポート<br />-モジュール<br />-マルチプロセスデバッグ<br />-ネイティブデバッグ<br />-新しいデバッグエンジンのサポート<br />-最適化されたコードのデバッグ<br />-出力 windows フィルター処理<br />-マネージデバッグのプロセスホスティング<br />-プロセス<br />-[クイックウォッチ]<br />-レジスタ<br />-スタック内のレジスタ<br />-リモートデバッグ<br />-戻り値<br />-スクリプトのデバッグ<br />-ソースサービスのサポート<br />-セキュリティ<br />-サイドバイサイド<br />-SQL<br />-シンボルサーバー<br />-トレースポイント<br />-スレッド<br />-視覚エフェクト<br />拡張スタイルシート言語変換 (XSLT) デバッガー|  
|64ビットのサポート|-マネージコードとネイティブコードの両方での64ビットデバッグ、すべての言語<br />-x64 ネイティブサポート|  
|ソースコード管理 (SCC)|-基本的な SCC 統合。 注 3 を参照してください。<br />-ツールとオプションの検証|  
|機能拡張|-Vspackage コンポーネントと MEF コンポーネントの使用|  
  
## <a name="notes"></a>説明  
  
#### <a name="1-data-tools"></a>1. データツール  
 統合シェルには、データ拡張機能のサポートや簡略化された**ソリューションエクスプローラー**などのデータベース開発ツールが含まれています。 ただし、SQL Server Express、SQL Reporting、および Crystal レポートは、統合シェルには含まれていません。  
  
#### <a name="2-debugging-support"></a>2. デバッグサポート  
 Integrated shell には、Visual Studio の Community バージョンに含まれているのと同じデバッグエンジンが含まれています。 デバッグエンジンには、マネージコード用の共通デバッガーと、実行、アタッチ、ブレークポイントの設定、エディットコンティニュなどの関連機能が含まれています。 ただし、デバッグエンジンでは SQL Server データベースデバッグはサポートされていません。  
  
 ネイティブデバッグのサポートは基本デバッガーパッケージに含まれていますが、追加の言語をサポートするために拡張することはできません。  
  
#### <a name="3-source-code-control-integration"></a>3. ソースコード管理の統合  
 Integrated shell は、ソースコード管理 (SCC) を実装するための Api と、MSSCCI ベースの共通ソース管理統合コンポーネントを提供するための Api を提供します。  
  
 SCC 統合は Visual Studio の Pro エディションの通常の機能ではありませんが、SCC 統合は統合シェルで提供されています。  
  
#### <a name="4-build-support"></a>4. ビルドのサポート  
 統合シェルは、ビルドのサポートを提供します。 ビルドに関する情報については、 [MSBuild リファレンスを参照](../msbuild/msbuild-reference.md)してください。  
  
## <a name="features-not-included-in-the-integrated-shell"></a>統合シェルに含まれていない機能  
 次に示すのは、統合シェルに含まれていない機能の一覧です。  
  
- クラス デザイナー  
  
- PreEmptive Protection - Dotfuscator  
  
- 言語機能  
  
- Vshost.exe  
  
- 統合シェルには、Visual Studio 言語またはそれに関連付けられているプロジェクトテンプレートまたはプロジェクト項目テンプレートは含まれません。 コードスニペット Visual Basic など、他の機能の言語固有の実装は含まれません。  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio の拡張の概要](https://msdn.microsoft.com/library/3e9078d7-2763-4cc4-8e20-fac69d747f59)