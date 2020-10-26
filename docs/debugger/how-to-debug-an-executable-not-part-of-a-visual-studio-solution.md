---
title: Visual Studio ソリューションの一部ではないアプリをデバッグする
titleSuffix: ''
ms.custom: ''
ms.date: 02/21/2020
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], executables
- executable files, importing
- executable files, debugging outside of projects
ms.assetid: 3ea176e8-1ce5-42c4-b7a2-abe3a2765033
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c8cb71acb9c1c332f269f77129fa2d11a9a874f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85350148"
---
# <a name="debug-an-app-that-isnt-part-of-a-visual-studio-solution-c-c-visual-basic-f"></a>Visual Studio ソリューションの一部ではないアプリをデバッグする (C++、C#、Visual Basic、F#)

Visual Studio ソリューションの一部ではないアプリ ( *.exe* ファイル) をデバッグすることができます。 [フォルダーを開く](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)プロジェクトの場合、自分または他のユーザーが Visual Studio の外部でアプリを作成した場合、または他の場所からアプリを取得した場合があります。

- Visual Studio のフォルダーを開くプロジェクト (プロジェクト ファイルまたはソリューション ファイルがない場合) については、「[コードを実行してデバッグする](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md#run-and-debug-your-code)」または「[launch.vs.json でデバッグ パラメーターを構成する](/cpp/build/open-folder-projects-cpp#configure-debugging-parameters-with-launchvsjson)」 (C++ の場合) を参照してください。

- Visual Studio に存在しないアプリの場合、一般的なデバッグ方法としては、Visual Studio の外部でアプリを起動した後、Visual Studio デバッガーの **[プロセスにアタッチ]** を使用してアタッチします。 詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。

   アプリにアタッチするには、数秒かかる手動手順が必要です。 この遅延のため、アタッチは、スタートアップの問題のデバッグや、ユーザーの入力を待機せずにすぐに完了するアプリのデバッグには役立ちません。

   このような状況では、アプリの Visual Studio EXE プロジェクトを作成するか、既存の C#、Visual Basic、または C++ ソリューションにインポートすることができます。 EXE プロジェクトをサポートしていないプログラミング言語もあります。

>[!IMPORTANT]
>アプリにアタッチするか、Visual Studio ソリューションに追加するかにかかわらず、Visual Studio でビルドされていないアプリのデバッグ機能は制限されます。
>
>ソース コードがある場合の最善の方法は、コードを Visual Studio プロジェクトにインポートすることです。 その後、アプリのデバッグ ビルドを実行します。
>
>ソース コードがなく、アプリに互換性のある形式の[デバッグ情報](../debugger/how-to-set-debug-and-release-configurations.md)がない場合、利用可能なデバッグ機能はほとんどありません。

### <a name="to-create-a-new-exe-project-for-an-existing-app"></a>既存のアプリ用に新しい EXE プロジェクトを作成するには

1. Visual Studio で、 **[ファイル]**  >  **[開く]**  >  **[プロジェクト]** を選択します。

1. **[プロジェクトを開く]** ダイアログ ボックスの **[ファイル名]** の横にあるドロップダウンで、 **[すべてのプロジェクト ファイル]** を選択します (まだ選択されていない場合)。

1. *.exe* ファイルに移動してそれを選択し、 **[開く]** を選択します。

   新しい一時的な Visual Studio ソリューションにファイルが表示されます。

1. **[デバッグ]** メニューから **[デバッグの開始]** などの実行コマンドを選択して、アプリのデバッグを始めます。

### <a name="to-import-an-app-into-an-existing-visual-studio-solution"></a>既存の Visual Studio ソリューションにアプリをインポートするには

1. C++、C#、または Visual Basic ソリューションを Visual Studio で開き、 **[ファイル]**  >  **[追加]**  >  **[既存のプロジェクト]** を選択します。

1. **[プロジェクトを開く]** ダイアログ ボックスの **[ファイル名]** の横にあるドロップダウンで、 **[すべてのプロジェクト ファイル]** を選択します (まだ選択されていない場合)。

1. *.exe* ファイルに移動してそれを選択し、 **[開く]** を選択します。

   ファイルが、現在のソリューションの下に新しいプロジェクトとして表示されます。

1. 新しいファイルを選択し、 **[デバッグ]** メニューから **[デバッグの開始]** などの実行コマンドを選択して、アプリのデバッグを始めます。

### <a name="see-also"></a>関連項目
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [DBG ファイル](/previous-versions/visualstudio/visual-studio-2010/da528y14(v=vs.100))