---
title: 混合モードでデバッグする | Microsoft Docs
description: 呼び出し元アプリのプロジェクトのプロパティ ページで、混合モードのデバッグを (マネージドとネイティブ コードを一緒に) 有効にする方法を確認します。
ms.custom: SEO-VS-2020
ms.date: 11/05/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging DLLs
- debugging [Visual Studio], mixed-mode
- mixed-mode debugging
ms.assetid: 2859067d-7fcc-46b0-a4df-8c2101500977
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1144fa2f775427a3a46feda46d8bba015e960f2a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913240"
---
# <a name="how-to-debug-in-mixed-mode-c-c-visual-basic"></a>方法: 混合モードでデバッグする (C#、C++、Visual Basic)

以下の手順では、マネージド コードとネイティブ コードを一緒にデバッグできるようにする方法について説明します。これは、混合モード デバッグとも呼ばれます。 混合モードのデバッグ シナリオには、次の 2 つがあります。

- DLL を呼び出すアプリはネイティブ コードで記述されており、DLL はマネージド コードです。

- DLL を呼び出すアプリはマネージド コードで記述されており、DLL はネイティブ コードになります。 このシナリオを詳細に説明するチュートリアルについては、[マネージ コードとネイティブ コードのデバッグ](../debugger/how-to-debug-managed-and-native-code.md)に関するページを参照してください。

マネージド デバッガーとネイティブ デバッガーは両方とも、呼び出し元のアプリ プロジェクトの **[プロパティ]** ページで有効にすることができます。 ネイティブ アプリとマネージド アプリの設定は異なります。

呼び出し元のアプリのプロジェクトにアクセスできない場合は、DLL プロジェクトから DLL をデバッグすることができます。 DLL プロジェクトだけをデバッグするには、混合モードは必要ありません。 詳細については、「[方法:DLL プロジェクトからデバッグする](../debugger/how-to-debug-from-a-dll-project.md)」を参照してください。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとコマンドは、ご利用の Visual Studio の設定またはエディションによっては、この記事のものと異なる場合があります。 設定を変更するには、 **[ツール]**  >  **[設定のインポートとエクスポート]** を選択します。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

## <a name="enable-mixed-mode-debugging-for-a-native-calling-app"></a>ネイティブの呼び出し元アプリに対する混合モード デバッグを有効にする

1. **ソリューション エクスプローラー** で C++ プロジェクトを選択し、 **[プロパティ]** アイコンを選択して、**Alt** + **Enter** キーを押すか、右クリックして **[プロパティ]** を選択します。

1. **[\<Project> プロパティ ページ]** ダイアログ ボックスで、 **[構成プロパティ]** を展開して、 **[デバッグ]** を選択します。

1. **[デバッガーの種類]** を **[混合]** または **[自動]** に設定します。

1. **[OK]** を選択します。

   ![混合モード デバッグを有効にする](../debugger/media/dbg-mixed-mode-from-native.png "混合モード デバッグを有効にする")

## <a name="enable-mixed-mode-debugging-for-a-managed-calling-app"></a>マネージド呼び出し元アプリに対する混合モード デバッグを有効にする

1. **ソリューション エクスプローラー** で C# または Visual Basic プロジェクトを選択し、 **[プロパティ]** アイコンを選択して、**Alt** + **Enter** キーを押すか、右クリックして **[プロパティ]** を選択します。

1. **[デバッグ]** タブを選択してから、 **[ネイティブ コードのデバッグを有効にする]** を選択します。

1. プロパティ ページを閉じて、変更を保存します。

   ![ネイティブ コードのデバッグを有効にする](../debugger/media/dbg-mixed-mode-from-csharp.png "ネイティブ コードのデバッグを有効にする")

> [!NOTE]
> Visual Studio 2017 以降、Visual Studio のほとんどのバージョンでは、プロジェクト プロパティの代わりに *launchSettings.json* ファイルを使用して、.NET Core アプリでネイティブ コードの混合モード デバッグを有効にする必要があります。 詳細については、[マネージド コードとネイティブ コードのデバッグ](../debugger/how-to-debug-managed-and-native-code.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [方法: DLL プロジェクトからデバッグする](../debugger/how-to-debug-from-a-dll-project.md)