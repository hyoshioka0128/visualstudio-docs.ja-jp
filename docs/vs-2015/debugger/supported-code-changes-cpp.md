---
title: サポートされているコード変更 (C++) | Microsoft Docs
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
- Edit and Continue, limitations
- supported code changes
- object files, limitations of Edit and Continue
- C++ language, supported code changes
- coding, supported code changes
- resource files, limitations of Edit and Continue
- code changes, handling in Edit and Continue
- what's new [C++], supported code changes
- code changes
ms.assetid: f5754363-8a56-417b-b904-b05d9dd26d03
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f167b3e9d27145284defa2ff491bb9ce0085f2a3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684907"
---
# <a name="supported-code-changes-c"></a>サポートされているコード変更 (C++)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual C++ のエディット コンティニュは、大半の種類のコード変更に対応します。 ただし、一部の変更はプログラムの実行中に適用できません。 これらの変更を適用するには、プログラムの実行を中断し、新しいバージョンのコードをビルドする必要があります。  
  
 Visual Studio での C++ のエディット コンティニュを使用する作業の情報については、「 [Edit and Continue (Visual C++)](../debugger/edit-and-continue-visual-cpp.md) 」を参照してください。  
  
## <a name="unsupported-changes"></a><a name="BKMK_Unsupported_changes"></a> サポートされていない変更  

デバッグ セッション中に適用できない C/C++ の変更は、次のとおりです。  
  
- グローバル データまたは静的データに対するほとんどの変更  
  
- ほかのコンピューターからコピーし、ローカルにビルドしていない実行可能ファイルに対する変更  
  
- オブジェクトのレイアウトに影響を与えるデータ型に対する変更 (クラスのデータ メンバーなど)  
  
- 64 KB を超える新しいコードまたはデータの追加  
  
- 命令ポインターの前にコンストラクターを必要とする変数の追加  
  
- ランタイム初期化を必要とするコードに影響を与える変更  
  
- 一部のインスタンスでの例外ハンドラーの追加  
  
- リソース ファイルに対する変更  
  
- 読み取り専用ファイル内のコードに対する変更  
  
- 対応する PDB ファイルを持たないコードに対する変更  
  
- オブジェクト ファイルのないコードに対する変更  
  
上のいずれかの変更を行った後にコード変更の適用を試みると、 **[出力]** ウィンドウにエラー メッセージまたは警告メッセージが表示されます。  
  
- エディット コンティニュでは、スタティック ライブラリは更新されません。 スタティック ライブラリに変更を加えた場合、変更前のスタティック ライブラリで実行が継続され、警告は表示されません。  
  
## <a name="unsupported-scenarios"></a><a name="BKMK_Unsupported_scenarios"></a> サポートされていないシナリオ  
 次のデバッグ シナリオでは、C/C++ のエディット コンティニュを使用できません。  
  
- [(強化に最適化されたデータのデバッグ)/Zo](https://msdn.microsoft.com/library/eea8d89a-7fe0-4fe1-86b2-7689bbebbd7f)でコンパイルしたネイティブ アプリのデバッグ  
  
- Visual Studio 2015 の Update 1 より前の Visual Studio のバージョンにおける、Windows ストア アプリまたはコンポーネントのデバッグ。 Visual Studio 2015 の Update 1 以降、Windows ストア C++ アプリと DirectX アプリでは、 `/ZI` コンパイラ スイッチと  `/bigobj` スイッチがサポートされているので、エディット コンティニュを使用できます。 `/FASTLINK` スイッチがサポートされているので、エディット コンティニュを使用できます。  
  
- Windows 98 でのデバッグ  
  
- 混合モードでの (ネイティブ/マネージ) デバッグ  
  
- JavaScript のデバッグ。  
  
- SQL デバッグ  
  
- ダンプ ファイルのデバッグ。  
  
- 未処理の例外を受け取った後のコード編集 ( **[ハンドルされていない例外で呼び出し履歴をアンワインドする]** オプションがオンでない場合)  
  
- **[デバッグ]** メニューの **[開始]** をクリックしてアプリケーションを実行する代わりに **[アタッチ先]** を使用してアプリケーションをデバッグ。  
  
- 最適化されたコードのデバッグ  
  
- ビルド エラーによって新しいバージョンのビルドが失敗した後の旧バージョンのデバッグ  
  
## <a name="linking-limitations"></a><a name="BKMK_Linking_limitations"></a> リンクに関する制限事項  
  
### <a name="linker-options-that-disable-edit-and-continue"></a><a name="BKMK_Linker_options_that_disable_Edit_and_Continue"></a> エディット コンティニュを無効にするリンカー オプション  
 次のリンカー オプションを使用すると、エディット コンティニュが無効になります。  
  
- **/OPT:REF**、 **/OPT:ICF**、または **/INCREMENTAL:NO** を設定すると、次の警告が表示されてエディット コンティニュが無効になります。  
  
     リンク : 警告 LNK4075:/OPT が指定されているため /EDITANDCONTINUE が無視されます  
  
     specification  
  
- **/ORDER**、 **/RELEASE**、または **/FORCE** を設定すると、次の警告が表示されてエディット コンティニュが無効になります。  
  
     リンク : 警告 LNK4075:/ オプションが指定されているため /INCREMENTAL が無視されます  
  
     specification  
  
- プログラム データベース (.pdb) ファイルの作成を禁止するオプションを設定すると、特定の警告は表示されずにエディット コンティニュが無効になります。  
  
### <a name="auto-relinking-limitations"></a><a name="BKMK_Auto_relinking_limitations"></a> 自動再リンクの制限事項  
 既定では、エディット コンティニュはデバッグ セッションの最後でプログラムを再リンクして、最新の実行可能ファイルを作成します。  
  
 エディット コンティニュでは、元のビルド位置とは異なる位置でデバッグすると、プログラムを再リンクできません。 手動でリビルドする必要があることを示すメッセージが表示されます。  
  
 エディット コンティニュでは、スタティック ライブラリはリビルドされません。 エディット コンティニュを使用してスタティック ライブラリに変更を加えた場合は、手動でライブラリをリビルドし、それを使用してアプリケーションを再リンクする必要があります。  
  
 エディット コンティニュは、カスタム ビルド ステップを呼び出しません。 プログラムがカスタム ビルドのステップを使用する場合は、カスタム ビルドのステップを呼び出せるように、手動でリビルドすることもできます。 この場合は、エディット コンティニュから手動によるリビルドの確認を受けた後、再リンクを無効にできます。  
  
 **エディット コンティニュの後に再リンクを無効にするには**  
  
1. **[デバッグ]** メニューの **[オプションと設定]** をクリックします。  
  
2. **[オプション]** ダイアログ ボックスの **[デバッグ]** ノードの下で、 **[エディット コンティニュ]** ノードをクリックします。  
  
3. **[デバッグ後にコードの変更点を再リンクする]** チェック ボックスをオフにします。  
  
## <a name="precompiled-header-limitations"></a><a name="BKMK_Precompiled_Header_Limitations"></a> プリコンパイル済みヘッダーの制限事項  
 既定では、エディット コンティニュがプリコンパイル済みヘッダーをバックグラウンドで読み込みおよび処理して、コード変更の処理を高速化します。 プリコンパイル済みヘッダーを読み込むには、物理メモリを割り当てる必要があります。このため、RAM が不足しているコンピューターでコンパイルする場合、問題が発生する可能性があります。 デバッグ時に Windows タスク マネージャーを使って使用できる物理メモリの量を確認することにより、メモリの量が問題になるかどうかを調べることができます。 使用できる物理メモリの量がプリコンパイル済みヘッダーのサイズを超える場合、エディット コンティニュに問題は生じません。 この量がプリコンパイル済みヘッダーのサイズより小さい場合は、エディット コンティニュがプリコンパイル済みヘッダーをバックグラウンドで読み込まないようにできます。  
  
 **エディット コンティニュがプリコンパイル済みヘッダーをバックグラウンドで読み込まないようにするには**  
  
1. **[デバッグ]** メニューの **[オプションと設定]** をクリックします。  
  
2. **[オプション]** ダイアログ ボックスの **[デバッグ]** ノードの下で、 **[エディット コンティニュ]** ノードをクリックします。  
  
3. **[プリコンパイルを許可する]** チェック ボックスをオフにします。  
  
## <a name="idl-attribute-limitations"></a><a name="BKMK_IDL_Attribute_Limitations"></a> IDL 属性の制限事項  
 エディット コンティニュでは、インターフェイス定義 (IDL) ファイルは再生成されません。 このため、デバッグ時に IDL 属性への変更は反映されません。 IDL 属性の変更結果を表示するには、デバッグを停止し、アプリをリビルドする必要があります。 エディット コンティニュでは、IDL 属性が変更されているとエラーや警告は生成されません。 詳細については、「 [IDL 属性](https://msdn.microsoft.com/library/04c596f4-c97b-4952-8053-316678b1d0b6)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エディットコンティニュ (Visual C++)](../debugger/edit-and-continue-visual-cpp.md)
