---
title: Visual Studio ソリューションの一部ではないアプリをデバッグする
titleSuffix: ''
ms.custom: ''
ms.date: 02/21/2020
ms.topic: conceptual
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
ms.openlocfilehash: 740af718a2928991d46bedbd6709337b9b20a254
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557907"
---
# <a name="debug-an-app-that-isnt-part-of-a-visual-studio-solution-c-c-visual-basic-f"></a>Visual Studio ソリューションの一部ではないアプリをデバッグするC++( C#、、Visual Basic F#、)

Visual Studio ソリューションに含まれていないアプリ ( *.exe*ファイル) をデバッグすることができます。 開いている[フォルダー](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)プロジェクトの可能性があります。または、Visual Studio の外部でアプリを作成したか、他の場所からアプリを取得した可能性があります。

- Visual Studio の開いているフォルダープロジェクト (プロジェクトファイルまたはソリューションファイルがない場合) については、「コードのC++[実行とデバッグ](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md#run-and-debug-your-code)」を参照するか、「launch.[と json を使用してデバッグパラメーターを構成](/cpp/build/open-folder-projects-cpp#configure-debugging-parameters-with-launchvsjson)する」を参照してください。

- Visual Studio に存在しないアプリの場合、通常、デバッグするには、visual studio の外部でアプリを起動し、Visual Studio デバッガーの **[プロセスにアタッチ]** を使用してアタッチします。 詳細については、「[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)」を参照してください。

   アプリにアタッチするには、数秒かかる手動操作が必要です。 この遅延のため、アタッチはスタートアップの問題のデバッグや、ユーザーの入力を待機せずに迅速に完了するアプリのデバッグには役立ちません。

   このような状況では、アプリの Visual Studio EXE プロジェクトを作成するか、既存C#の、Visual Basic、またはC++ソリューションにインポートすることができます。 EXE プロジェクトをサポートしていないプログラミング言語もあります。

>[!IMPORTANT]
>アプリにアタッチするか、Visual Studio ソリューションに追加するかにかかわらず、Visual Studio でビルドされていないアプリのデバッグ機能は制限されます。
>
>ソースコードがある場合は、コードを Visual Studio プロジェクトにインポートすることをお勧めします。 次に、アプリのデバッグビルドを実行します。
>
>ソースコードがなく、アプリに互換性のある形式の[デバッグ情報](../debugger/how-to-set-debug-and-release-configurations.md)がない場合、利用可能なデバッグ機能はほとんどありません。

### <a name="to-create-a-new-exe-project-for-an-existing-app"></a>既存のアプリの新しい EXE プロジェクトを作成するには

1. Visual Studio で、 **[ファイル]** を選択して > **プロジェクト** > **開き**ます。

1. **[プロジェクトを開く]** ダイアログボックスで、 **[ファイル名]** の横にあるドロップダウンで、 **[すべてのプロジェクトファイル]** を選択します (まだ選択されていない場合)。

1. *.Exe*ファイルに移動して選択し、 **[開く]** を選択します。

   新しい一時的な Visual Studio ソリューションにファイルが表示されます。

1. **[デバッグ]** メニューの **[デバッグの開始]** などの実行コマンドを選択して、アプリのデバッグを開始します。

### <a name="to-import-an-app-into-an-existing-visual-studio-solution"></a>既存の Visual Studio ソリューションにアプリをインポートするには

1. C#、、 C++または Visual Basic ソリューションを Visual Studio で開いている状態で、**ファイル** > **既存のプロジェクト**の**追加** >  を選択します。

1. **[プロジェクトを開く]** ダイアログボックスで、 **[ファイル名]** の横にあるドロップダウンで、 **[すべてのプロジェクトファイル]** を選択します (まだ選択されていない場合)。

1. *.Exe*ファイルに移動して選択し、 **[開く]** を選択します。

   ファイルは、現在のソリューションの下に新しいプロジェクトとして表示されます。

1. 新しいファイルを選択した状態で、 **[デバッグ] メニューの**[デバッグの**開始**] などの実行コマンドを選択して、アプリのデバッグを開始します。

### <a name="see-also"></a>参照
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [DBG ファイル](/previous-versions/visualstudio/visual-studio-2010/da528y14(v=vs.100))