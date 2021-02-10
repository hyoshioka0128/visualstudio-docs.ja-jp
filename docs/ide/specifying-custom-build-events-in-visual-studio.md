---
title: カスタム ビルド イベントを指定する
description: ビルドの開始前またはビルドの終了後に Visual Studio で自動的にコマンドを実行する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- build events, customizing
ms.assetid: 69e935a5-e208-4bcd-865c-3e5f9b047ca8
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d0728154e21893ac45fc0e17cc3d0407551dbb3a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99951031"
---
# <a name="specify-custom-build-events-in-visual-studio"></a>Visual Studio でのカスタム ビルド イベントの指定

カスタム ビルド イベントを指定することで、ビルドの開始前またはビルドの終了後に自動的にコマンドを実行できます。 たとえば、ビルドの開始前に *.bat* ファイルを実行したり、ビルドの完了後に新しいファイルをフォルダーにコピーしたりできます。 ビルド イベントは、ビルド プロセスにおいてビルドがこれらのポイントに正常に達する場合にのみ実行します。

使用するプログラミング言語に関する具体的な情報については、次のトピックを参照してください。

- Visual Basic -- [方法 : ビルド イベントを指定する (Visual Basic)](../ide/how-to-specify-build-events-visual-basic.md)。

- C# および F# -- [方法: ビルド イベントを指定する (C#)](../ide/how-to-specify-build-events-csharp.md)。

- Visual C++ -- [ビルド イベントを指定する](/cpp/build/specifying-build-events)。

## <a name="syntax"></a>構文

ビルド イベントは、DOS コマンドと同じ構文に従いますが、マクロを使用すると、ビルド イベントをより簡単に作成することができます。 使用可能なマクロの一覧については、「[[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)」を参照してください。

最適な結果を得るには、次のような書式のヒントに従います。

- *.bat* ファイルを実行するすべてのビルド イベントの前に `call` ステートメントを追加します。

   例: `call C:\MyFile.bat`

   例 : `call C:\MyFile.bat call C:\MyFile2.bat`

- ファイルのパスを引用符で囲みます。

   例 ([!INCLUDE[win8](../debugger/includes/win8_md.md)] の場合): "%ProgramFiles(x86)%\Microsoft SDKs\Windows\v8.0A\Bin\NETFX 4.0 Tools\gacutil.exe" -if "$(TargetPath)"

- 改行を使用して、複数のコマンドを区切ります。

- 必要に応じて、ワイルドカードを挿入します。

   例: `for %I in (*.txt *.doc *.html) do copy %I c:\`*mydirectory*`\`

  > [!NOTE]
  > 上記のコードの `%I` は、バッチ スクリプトでは `%%I` になります。

## <a name="see-also"></a>関連項目

- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
- [[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)
- [MSBuild の特殊文字](../msbuild/msbuild-special-characters.md)
- [チュートリアル: アプリケーションを構築する](../ide/walkthrough-building-an-application.md)
