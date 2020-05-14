---
title: 外部ツールの管理 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.externaltools
helpviewer_keywords:
- Create GUID tool
- RC (Resource Compiler)
- ReBase tool
- Windows NT Message Compiler
- Windows NT C++ Symbol Undecorator
- tstcon32.exe
- Type Library Generator
- Windows NT Image Binder
- tools [Visual Studio], external
- RowsetViewer tool
- utilities, external tools
- Local Test Manager
- OLE DB Rowset Viewer
- Midlc (IDL Compiler)
- ATL Trace Tool
- Odbcte32w.exe
- IDL Compiler
- HCW (Help Workshop)
- Message Compiler [Visual Studio]
- UUID Generator
- MIDL, external tools
- ErrLook tool
- MAKEHM tool
- Error lookup tool
- OLEVIEW (Object Viewer)
- Uuidgen.exe
- WebDbg tool
- OLE/COM Object Viewer
- LTM (Local Test Manager)
- ATLTraceTool.exe
- Bind tool
- Vsvars32.bat
- external tools [Visual Studio]
- ODBC Test
- Windows NT Image Rebaser
- undname.exe
- Vcspawn.exe
- ActiveX Control Test Container
- mc (Message Compiler)
- GUIDGEN tool
- Odbcte32.exe
- DisableMsg tool
- MkTypLib tool
- Help Workshop
- Resource Compiler
ms.assetid: f382fd40-a98f-4934-8c9a-5aeae881acde
caps.latest.revision: 41
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7a9ebda81f013f42aeac23c9c0a8cc5a0a41f5f0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651350"
---
# <a name="managing-external-tools"></a>Visual Studio の外部ツール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio から、外部ツールを呼び出すことができます。 いくつかの既定ツールは **[ツール]** メニューで使用できますが、他の実行可能ファイルを独自に追加することもできます。

## <a name="tools-available-on-the-visual-studio-tools-menu"></a>Visual Studio の [ツール] メニューで使用できるツール
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の **[ツール]** メニューでは、次のツールを呼び出すことができます。 これらは、名前を指定して **[クイック起動]** ウィンドウから呼び出すこともできます。 たとえば、GuidGen.exe を呼び出すには、「**GUID の作成**」と入力します。

1. GUID の作成: GUID を生成します。

2. エラー検索: 入力された値からエラー メッセージを取得します。 詳細については、「[ERRLOOK リファレンス](https://msdn.microsoft.com/library/6040ffc1-2355-4a45-8998-84cbcba4ca91)」を参照してください。

3. ATL/MFC トレース ツール: ATL および ATL のソースに含まれているデバッグ トレース メッセージを表示します。

4. PreEmptive Protection - Dotfuscator: .NET プログラムをリバース エンジニアリングから保護します。

5. SPY++: プロセス、スレッド、ウィンドウ、およびウィンドウ メッセージをグラフィカル表示します。

6. WCF サービス構成エディター: WCF サービスの構成設定を作成および変更できます。

> [!WARNING]
> 表示される外部ツールの一覧は、インストールされている Visual Studio のエディションおよび適用されている設定プロファイルによって異なります。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="adding-new-tools"></a>新しいツールの追加
 **[ツール]** メニューに外部ツールを追加することができます。 **[外部ツール]** ダイアログ ボックスを開き、 **[追加]** をクリックして、情報を入力します。 たとえば、次のエントリを指定すると、Visual Studio で現在開いているファイルのディレクトリでエクスプローラーが開きます。

1. タイトル: 開いているファイルの場所

2. コマンド: explorer.exe

3. 引数: /root、"$(ItemDir)"

## <a name="arguments-for-external-tools"></a>外部ツールの引数
 次の引数は、外部ツールを起動するときに割り当てられる、Visual Studio の変数です。 [外部ツール] ダイアログ ボックスを使用して、メモ帳や Spy++ などの外部ツールへのリンクを **[ツール]** メニューでリストできます。

> [!NOTE]
> IDE のステータス バーに、アクティブなコード エディターの挿入位置を示す、Current Line 変数および Current Column 変数が表示されます。 Current Text 変数は、その場所で選択されているテキストまたはコードを返します。

|名|引数|説明|
|----------|--------------|-----------------|
|項目のパス|$(ItemPath)|現在のファイルの完全なファイル名 (ドライブ + パス + ファイル名)。|
|項目のディレクトリ|$(ItemDir)|現在のファイルのディレクトリ (ドライブ + パス)。|
|項目のファイル名|$(ItemFilename)|現在のファイルのファイル名 (ファイル名)。|
|項目の拡張子|$(ItemExt)|現在のファイルのファイル名拡張子。|
|カレント行|$(CurLine)|コード ウィンドウ内のカーソルの現在の行位置。|
|カレント列|$(CurCol)|コード ウィンドウ内のカーソルの現在の列位置。|
|カレント テキスト|$(CurText)|選択されているテキスト。|
|ターゲット パス|$(TargetPath)|作成するアイテムの完全なファイル名 (ドライブ + パス + ファイル名)。|
|ターゲット ディレクトリ|$(TargetDir)|作成するアイテムのディレクトリ。|
|ターゲット名|$(TargetName)|作成するアイテムのファイル名。|
|ターゲットの拡張子|$(TargetExt)|作成するアイテムのファイル名拡張子。|
|バイナリ ディレクトリ|$(BinDir)|作成中のバイナリの最終的な場所 (ドライブ + パスとして定義されます)。 例: **\\...\My Documents\Visual Studio \<Version>\\<ProjectName\>\bin\debug**|
|プロジェクト ディレクトリ|$(ProjDir)|現在のプロジェクトのディレクトリ (ドライブ + パス)。|
|プロジェクト ファイル名|$(ProjFileName)|現在のプロジェクトのファイル名 (ドライブ + パス + ファイル名)。|
|ソリューション ディレクトリ|$(SolutionDir)|現在のソリューションのディレクトリ (ドライブ + パス)。|
|ソリューション ファイル名|$(SolutionFileName)|現在のソリューションのファイル名 (ドライブ + パス + ファイル名)。|

## <a name="see-also"></a>参照
 [C/C++ のビルド ツール](https://msdn.microsoft.com/library/48d9daf4-6bbf-473a-8ce2-bf2923b69f80)
