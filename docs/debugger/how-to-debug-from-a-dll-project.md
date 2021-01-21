---
title: DLL プロジェクトからデバッグする | Microsoft Docs
Description: プロジェクト自体から DLL プロジェクトのデバッグを開始するには、プロジェクトのプロパティで呼び出し元のアプリを指定します。 詳しくは、この記事をご覧ください。
ms.custom: SEO-VS-2020
ms.date: 10/10/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- DLL projects, debugging
- debugging DLLs
- DLLs, debugging projects
- debugging [Visual Studio], DLLs
ms.assetid: 40a94339-d3f7-4ab9-b8a1-b8cf82942f44
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 723f35142ec125c016caa3653be450b61fb05d02
ms.sourcegitcommit: 40d758f779d42c66cb02ae7face8a62763a8662b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97398559"
---
# <a name="how-to-debug-from-a-dll-project-in-visual-studio-c-c-visual-basic-f"></a>方法: Visual Studio で DLL プロジェクトからデバッグする (C#、C++、Visual Basic、F#)

DLL プロジェクトをデバッグする 1 つの方法は、DLL プロジェクトのプロパティで呼び出し元のアプリを指定することです。 その後、DLL プロジェクト自体からデバッグを開始できます。 この方法を使用するには、アプリにより、構成した場所と同じ場所にある同じ DLL を呼び出す必要があります。 アプリによって、DLL の異なるバージョンが検出されて読み込まれた場合、そのバージョンにブレークポイントは含まれません。 DLL をデバッグするその他の方法については、[DLL プロジェクトのデバッグ](../debugger/debugging-dll-projects.md)に関するページを参照してください。

お使いのマネージド アプリでネイティブ DLL を呼び出すか、ネイティブ アプリでマネージド DLL を呼び出す場合、DLL と呼び出し元のアプリの両方をデバッグできます。 詳細については、[混合モードでデバッグする](../debugger/how-to-debug-in-mixed-mode.md)

ネイティブ DLL プロジェクトとマネージド DLL プロジェクトでは、呼び出し元のアプリを指定する設定が異なります。

## <a name="specify-a-calling-app-in-a-native-dll-project"></a>ネイティブ DLL プロジェクトで呼び出し元のアプリを指定する

1. **[ソリューション エクスプローラー]** で C++ DLL プロジェクトを選択します。 **[プロパティ]** アイコンを選択して **Alt**+**Enter** キーを押すか、右クリックして **[プロパティ]** を選択します。

1. **[\<Project> プロパティ ページ]** ダイアログ ボックスで、ウィンドウの上部にある **[構成]** フィールドが **[デバッグ]** に設定されていることを確認します。

1. **[構成プロパティ]**  >  **[デバッグ]** を選択します。

1. **[起動するデバッガー]** の一覧で、 **[ローカル Windows デバッガー]** または **[リモート Windows デバッガー]** のいずれかを選択します。

1. **[コマンド]** ボックスまたは **[リモート コマンド]** ボックスで、呼び出し元のアプリの完全修飾パスとファイル名 (たとえば、 *.exe* ファイル) を追加します。

   ![[デバッグ プロパティ] ウィンドウ](../debugger/media/dbg-debugging-properties-dll.png "[デバッグ プロパティ] ウィンドウ")

1. **[コマンド引数]** ボックスに、任意の必要なプログラム引数を追加します。

1. **[OK]** を選択します。

## <a name="specify-a-calling-app-in-a-managed-dll-project"></a>マネージド DLL プロジェクトで呼び出し元のアプリを指定する

1. **[ソリューション エクスプローラー]** で、C# DLL プロジェクトまたは Visual Basic DLL プロジェクトを選択します。 **[プロパティ]** アイコンを選択して **Alt**+**Enter** キーを押すか、右クリックして **[プロパティ]** を選択します。

1. ウィンドウの上部にある **[構成]** フィールドが **[デバッグ]** に設定されていることを確認します。

1. **[開始動作]** で次の操作を行います。

   - .NET Framework DLL の場合は、 **[外部プログラムを起動する]** を選択して、呼び出し元のアプリの完全修飾パスと名前を追加します。

   - または、 **[ブラウザーを開始時に使用する URL]** を選択して、ローカルの ASP.NET アプリの URL を入力します。

   - .NET Core DLL の場合は、 **[デバッグ プロパティ]** ページが異なります。 **[起動]** ドロップダウンから **[実行可能ファイル]** を選択して、 **[実行可能ファイル]** フィールドで、呼び出し元のアプリの完全修飾パスと名前を追加します。

1. **[コマンド ライン引数]** フィールドまたは **[アプリケーション引数]** フィールドで、必要なコマンド ライン引数を追加します。

   ![[C# デバッグ プロパティ] ウィンドウ](../debugger/media/dbg-debugging-properties-dll-csharp.png "[C# デバッグ プロパティ] ウィンドウ")

1. **[ファイル]**  >  **[Save Selected Items]\(選択した項目を保存\)** を使用するか、または **Ctrl**+**S** キーを押して、変更を保存します。

## <a name="debug-from-the-dll-project"></a>DLL プロジェクトからデバッグする

1. DLL プロジェクトにブレークポイントを設定します。

1. DLL プロジェクトを右クリックして、 **[スタートアップ プロジェクトに設定]** を選択します。

1. ソリューションの **[構成]** フィールドが **[デバッグ]** に設定されていることを確認します。 **F5** キーを押して、緑色の **[開始]** 矢印をクリックするか、または **[デバッグ]**  >  **[デバッグの開始]** を選択します。

デバッグでブレークポイントがヒットされない場合、ご自分の DLL 出力 (既定では、 *\<project>\Debug* フォルダー) が、呼び出し元のアプリで呼び出されている場所であることを確認します。

## <a name="see-also"></a>関連項目
- [DLL プロジェクトのデバッグ](../debugger/debugging-dll-projects.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)