---
title: RC タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VC.Project.VCResourceCompilerTool.UndefineProcessorDefinitions
- vc.task.rc
- VC.Project.VCResourceCompilerTool.SuppressStartupBanner
- VC.Project.VCResourceCompilerTool.NullTerminateStrings
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- RC task (MSBuild (C++))
- MSBuild (C++), RC task
ms.assetid: 2fd26c75-a056-4dda-9f7e-2f90d3748d88
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 13ae844759cb73de6dc7bcce6c8898c21132f9d7
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77632915"
---
# <a name="rc-task"></a>RC タスク

Microsoft Windows リソース コンパイラ ツールである *rc.exe* をラップします。 **RC** タスクは、カーソル、アイコン、ビットマップ、ダイアログ ボックス、フォントなどのリソースをコンパイルし、リソース ファイル ( *.res*) を作成します。 詳しくは、「[リソース コンパイラ](/windows/desktop/menurc/resource-compiler)」をご覧ください。

## <a name="parameters"></a>パラメーター

 以下の表で、RC タスクのパラメーターについて説明します。 タスク パラメーターの大部分とパラメーターのいくつかのセットは、コマンド ライン オプションに対応します。

|パラメーター|[説明]|
|---------------|-----------------|
|**AdditionalIncludeDirectories**|省略可能な **String[]** 型のパラメーターです。<br /><br /> インクルード ファイルを検索するディレクトリのリストにディレクトリを追加します。<br /><br /> 詳細については、「**Using RC (The RC Command Line)** 」(RC を使用する (RC コマンド ライン)) の [/I](/windows/win32/menurc/using-rc-the-rc-command-line-) オプションを参照してください。|
|**AdditionalOptions**|省略可能な **String** 型のパラメーターです。<br /><br /> コマンドライン オプションの一覧です。例: /\<option1> /\<option2> /\<option#>。 他の **RC** タスク パラメーターでは表されないコマンド ライン オプションを指定する場合は、このパラメーターを使用します。<br /><br /> 詳細については、「[Using RC (The RC Command Line)](/windows/win32/menurc/using-rc-the-rc-command-line-)」(RC を使用する (RC コマンド ライン)) のオプションを参照してください。|
|**カルチャ**|省略可能な **String** 型のパラメーターです。<br /><br /> リソースで使用されているカルチャを表すロケール ID を指定します。<br /><br /> 詳細については、「**Using RC (The RC Command Line)** 」(RC を使用する (RC コマンド ライン)) の [/l](/windows/win32/menurc/using-rc-the-rc-command-line-) オプションを参照してください。|
|**IgnoreStandardIncludePath**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合、ヘッダー ファイルまたはリソース ファイルの検索時、リソース コンパイラが INCLUDE 環境変数を確認するのを防止します。<br /><br /> 詳細については、「**Using RC (The RC Command Line)** 」(RC を使用する (RC コマンド ライン)) の [/x](/windows/win32/menurc/using-rc-the-rc-command-line-) オプションを参照してください。|
|**NullTerminateStrings**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合、文字列テーブル内のすべての文字列が null 終端されます。<br /><br /> 詳細については、「**Using RC (The RC Command Line)** 」(RC を使用する (RC コマンド ライン)) の [/n](/windows/win32/menurc/using-rc-the-rc-command-line-) オプションを参照してください。|
|**PreprocessorDefinitions**|省略可能な **String[]** 型のパラメーターです。<br /><br /> リソース コンパイラに対して 1 つまたは複数のプリプロセッサ シンボルを定義します。 マクロ シンボルの一覧を指定します。<br /><br /> 詳細については、「**Using RC (The RC Command Line)** 」(RC を使用する (RC コマンド ライン)) の [/d](/windows/win32/menurc/using-rc-the-rc-command-line-) オプションを参照してください。 この表の「**UndefinePreprocessorDefinitions**」も参照してください。|
|**ResourceOutputFileName**|省略可能な **String** 型のパラメーターです。<br /><br /> リソース ファイルの名前を指定します。 リソース ファイル名を指定します。<br /><br /> 詳細については、「**Using RC (The RC Command Line)** 」(RC を使用する (RC コマンド ライン)) の [/fo](/windows/win32/menurc/using-rc-the-rc-command-line-) オプションを参照してください。|
|**ShowProgress**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合、コンパイラの進捗状況について報告するメッセージが表示されます。<br /><br /> 詳細については、「**Using RC (The RC Command Line)** 」(RC を使用する (RC コマンド ライン)) の [/v](/windows/win32/menurc/using-rc-the-rc-command-line-) オプションを参照してください。|
|**ソース**|必須の `ITaskItem[]` 型のパラメーターです。<br /><br /> タスクで使用および生成できる MSBuild ソース ファイル アイテムの配列を定義します。|
|**SuppressStartupBanner**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。<br /><br /> 詳細については、 **/?** コマンドライン オプションを入力し、 **/nologo** オプションを確認してください。|
|**TrackerLogDirectory**|省略可能な **String** 型のパラメーターです。<br /><br /> トラッカー ログのディレクトリを指定します。|
|**UndefinePreprocessorDefinitions**|プリプロセッサ シンボルの定義を解除します。<br /><br /> 詳細については、「**Using RC (The RC Command Line)** 」(RC を使用する (RC コマンド ライン)) の [/u](/windows/win32/menurc/using-rc-the-rc-command-line-) オプションを参照してください。 この表の「**PreprocessorDefinitions**」も参照してください。|

## <a name="see-also"></a>参照

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)