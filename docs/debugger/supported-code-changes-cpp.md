---
title: サポートされているコード変更 (C++) | Microsoft Docs
description: Visual Studio での C++ プロジェクトのデバッグ中にエディット コンティニュ機能を使用する際に、サポートされるコード変更について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/18/2020
ms.topic: conceptual
dev_langs:
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
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- cplusplus
ms.openlocfilehash: d000d2757321701c2e14427c6bbb4d3e4164d26f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876304"
---
# <a name="supported-code-changes-c"></a>サポートされているコード変更 (C++)
C++ プロジェクトのエディット コンティニュは、大半の種類のコード変更に対応します。 ただし、一部の変更はプログラムの実行中に適用できません。 これらの変更を適用するには、プログラムの実行を中断し、新しいバージョンのコードをビルドする必要があります。

 Visual Studio での C++ のエディット コンティニュを使用する作業の情報については、「[エディット コンティニュ (C++)](../debugger/edit-and-continue-visual-cpp.md)」を参照してください。

## <a name="requirements"></a><a name="BKMK_Requirements"></a> 要件
### <a name="build-settings-project--properties"></a>ビルドの設定 ([プロジェクト] > [プロパティ]):
  1. **[C/C++] > [全般] > [デバッグ情報の形式]** : [エディット コンティニュのプログラム データベース] (`/ZI`)
  2. **[C/C++] > [コード生成] > [最小リビルドを有効にする]** : [はい] (`/Gm`)
  3. **[リンカー] > [全般] > [インクリメンタル リンクを有効にする]** : [はい] (`/INCREMENTAL`)

     互換性のないリンカー設定 (`/SAFESEH`、`/OPT:` など) を使用すると、ビルド中に警告 _LNK4075_ が発生します。  
     例 : `LINK : warning LNK4075: ignoring '/INCREMENTAL' due to '/OPT:ICF' specification`

### <a name="debugger-settings-debug--options--general"></a>デバッガーの設定 ([デバッグ] > [オプション] > [全般]):
  - [ネイティブのエディット コンティニュを有効にする]

     コンパイラまたはリンカーの互換性のない設定では、エディット コンティニュ中にエラーが発生します。  
     例 : `Edit and Continue : error  : ‘file.cpp’ in ‘MyApp.exe’ was not compiled with Edit and Continue enabled. Ensure that the file is compiled with the Program Database for Edit and Continue (/ZI) option.`

## <a name="unsupported-changes"></a><a name="BKMK_Unsupported_changes"></a> サポートされていない変更
 デバッグ セッション中に適用できない C/C++ の変更は、次のとおりです。 上のいずれかの変更を行った後にコード変更の適用を試みると、 **[出力]** ウィンドウにエラー メッセージまたは警告メッセージが表示されます。

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

* 次のようなラムダの変更:
  - 静的メンバーまたはグローバル メンバーがある。
  - std::function に渡される。 これにより、正規の ODR 違反が発生し、C1092 が生成されます。

- エディット コンティニュでは、スタティック ライブラリは更新されません。 スタティック ライブラリに変更を加えた場合、変更前のスタティック ライブラリで実行が継続され、警告は表示されません。

## <a name="unsupported-scenarios"></a><a name="BKMK_Unsupported_scenarios"></a> サポートされていないシナリオ
 次のデバッグ シナリオでは、C/C++ のエディット コンティニュを使用できません。

- [(強化に最適化されたデータのデバッグ)/Zo](/cpp/build/reference/zo-enhance-optimized-debugging)でコンパイルしたネイティブ アプリのデバッグ

- Visual Studio 2015 の Update 1 より前の Visual Studio のバージョンにおける、UWP アプリまたはコンポーネントのデバッグ。 Visual Studio 2015 の Update 1 以降、UWP C++ アプリと DirectX アプリでは、`/ZI` コンパイラ スイッチと `/bigobj` スイッチがサポートされているので、エディット コンティニュを使用できます。 `/FASTLINK` スイッチがサポートされているので、エディット コンティニュを使用できます。

- 8/8.1 ストア アプリのデバッグ。 これらのプロジェクトでは、VC 120 ツールセットと C/C++ `/bigobj` スイッチが使用されます。 `/bigobj` でのエディット コンティニュは、VC 140 ツールセットでのみサポートされます。

- Windows 98 でのデバッグ

- 混合モードでの (ネイティブ/マネージ) デバッグ

- JavaScript のデバッグ。

- SQL デバッグ

- ダンプ ファイルのデバッグ。

- 未処理の例外を受け取った後のコード編集 ( **[ハンドルされていない例外で呼び出し履歴をアンワインドする]** オプションがオンでない場合)

- **[デバッグ]** メニューの **[開始]** をクリックしてアプリケーションを実行する代わりに **[アタッチ先]** を使用してアプリケーションをデバッグ。

- 最適化されたコードのデバッグ

- ビルド エラーによって新しいバージョンのビルドが失敗した後の旧バージョンのデバッグ

- カスタム コンパイラ (*cl.exe*) パスの使用。 セキュリティ上の理由から、エディット コンティニュ中のファイルの再コンパイルの場合、Visual Studio では常に、インストールされているコンパイラが使用されます。 カスタム コンパイラ パスを使用している場合 (たとえば、`*.props` ファイル内のカスタム `$(ExecutablePath)` 変数により)、警告が表示され、Visual Studio は同じバージョンとアーキテクチャのインストール済みコンパイラを使用するようにフォールバックします。

- FASTBuild ビルド システム。 FASTBuild は、現在、"最小リビルドを有効にする (`/Gm`)" コンパイラ スイッチと互換性がないため、エディット コンティニュはサポートされません。

- レガシ アーキテクチャ、VC ツールセット。 VC 140 ツールセットの既定のデバッガーでは、X86 と X64 の両方のアプリケーションでエディット コンティニュがサポートされます。 レガシ ツールセットでは、X86 アプリケーションのみがサポートされます。 VC 120 より古いツールセットでは、エディット コンティニュを使用するには、 _[デバッグ] > [オプション] > [全般] >_ [ネイティブ互換モードの使用] をオンにして、レガシ デバッガーを使用する必要があります。

## <a name="linking-limitations"></a><a name="BKMK_Linking_limitations"></a> リンクに関する制限事項

### <a name="linker-options-that-disable-edit-and-continue"></a><a name="BKMK_Linker_options_that_disable_Edit_and_Continue"></a> エディット コンティニュを無効にするリンカー オプション
 次のリンカー オプションを使用すると、エディット コンティニュが無効になります。

- **/OPT:REF**、 **/OPT:ICF**、または **/INCREMENTAL:NO** を設定すると、次の警告が表示されてエディット コンティニュが無効になります。  
     `LINK : warning LNK4075: ignoring /EDITANDCONTINUE due to /OPT specification`

- **/ORDER**、 **/RELEASE**、または **/FORCE** を設定すると、次の警告が表示されてエディット コンティニュが無効になります。  
     `LINK : warning LNK4075: ignoring /INCREMENTAL due to /option specification`

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

## <a name="precompiled-header-limitations"></a><a name="BKMK_Precompiled_header_limitations"></a> プリコンパイル済みヘッダーに関する制限事項
 既定では、エディット コンティニュがプリコンパイル済みヘッダーをバックグラウンドで読み込みおよび処理して、コード変更の処理を高速化します。 プリコンパイル済みヘッダーを読み込むには、物理メモリを割り当てる必要があります。このため、RAM が不足しているコンピューターでコンパイルする場合、問題が発生する可能性があります。 デバッグ時に Windows タスク マネージャーを使って使用できる物理メモリの量を確認することにより、メモリの量が問題になるかどうかを調べることができます。 使用できる物理メモリの量がプリコンパイル済みヘッダーのサイズを超える場合、エディット コンティニュに問題は生じません。 この量がプリコンパイル済みヘッダーのサイズより小さい場合は、エディット コンティニュがプリコンパイル済みヘッダーをバックグラウンドで読み込まないようにできます。

 **エディット コンティニュがプリコンパイル済みヘッダーをバックグラウンドで読み込まないようにするには**

1. **[デバッグ]** メニューの **[オプションと設定]** をクリックします。

2. **[オプション]** ダイアログ ボックスの **[デバッグ]** ノードの下で、 **[エディット コンティニュ]** ノードをクリックします。

3. **[プリコンパイルを許可する]** チェック ボックスをオフにします。

## <a name="idl-attribute-limitations"></a><a name="BKMK_IDL_attribute_limitations"></a> IDL 属性に関する制限事項
 エディット コンティニュでは、インターフェイス定義 (IDL) ファイルは再生成されません。 このため、デバッグ時に IDL 属性への変更は反映されません。 IDL 属性の変更結果を表示するには、デバッグを停止し、アプリをリビルドする必要があります。 エディット コンティニュでは、IDL 属性が変更されているとエラーや警告は生成されません。 詳細については、「 [IDL 属性](/cpp/windows/idl-attributes)」を参照してください。

## <a name="diagnosing-issues"></a><a name="BKMK_Diagnosing_issues"></a> 問題の診断
 上記の条件のいずれにも該当しないシナリオの場合は、次の DWORD レジストリ値を設定して詳細を収集できます。
 1. 開発者コマンド プロンプトを開きます。
 2. 次のコマンドを実行します。  
     `VsRegEdit.exe set “C:\Program Files (x86)\Microsoft Visual Studio\[Version]\[YOUR EDITION]” HKCU Debugger NativeEncDiagnosticLoggingLevel DWORD 1`

 デバッグ セッションの開始時にこの値を設定すると、エディット コンティニュのさまざまなコンポーネントから、**出力ウィンドウ** >  **[デバッグ]** ペインに詳細ログが出力されます。

## <a name="see-also"></a>関連項目
- [エディット コンティニュ (C++)](../debugger/edit-and-continue-visual-cpp.md)
