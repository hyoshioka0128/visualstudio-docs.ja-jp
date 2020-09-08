---
title: Windows フォームアプリのデバッグを準備する | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging Windows applications
- Windows applications, debugging
- debugging [Visual Studio], Windows applications
- debugging [C#], Windows applications
- debugging [Visual Basic], Windows applications
ms.assetid: 7092ee7f-8378-4def-aef8-1695bd97cf14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e9e98411a009ea4345b567cbc38e6cf94c037323
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75916388"
---
# <a name="debugging-preparation-windows-forms-applications"></a>デバッグの準備: Windows フォーム アプリケーション
Windows フォーム プロジェクト テンプレートは、Windows フォーム アプリケーションを作成します。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、この種類のアプリケーションを簡単にデバッグできます。 詳細については、[Windows アプリケーション プロジェクトの作成](/previous-versions/visualstudio/visual-studio-2010/42wc9kk5(v=vs.100))に関するページを参照してください。

 プロジェクト テンプレートを使用して Windows フォーム プロジェクトを作成する場合、デバッグ構成とリリース構成に必要な設定は [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって自動的に作成されます。 この設定は必要に応じて変更できます。 設定の変更は、 **[\<project name> プロパティ ページ]** ダイアログ ボックス (Visual Basic の場合は **[マイ プロジェクト]** ) で行います。

 詳細については、「[プロパティの推奨設定](../debugger/managed-debugging-recommended-property-settings.md)」を参照してください。

 推奨される追加のプロパティ設定を次の表に示します。

### <a name="configuration-properties-in-debug-tab"></a>[デバッグ] タブの構成プロパティ

|**プロパティ名**|**設定**|
|-----------------------|-----------------|
|**開始動作**|ほとんどの場合、 **[スタート プロジェクト]** に設定します。 デバッグの開始時に他の実行可能ファイルを起動する場合 (通常は DLL をデバッグする場合) には、 **[外部プログラムの開始]** に設定します。|

 Windows フォーム アプリケーションは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 内から、または既に実行中のアプリケーションにアタッチすることによってデバッグできます。 アタッチの詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。

### <a name="to-debug-a-c-f-or-visual-basic-windows-forms-application"></a>C#、F#、または Visual Basic の Windows フォーム アプリケーションをデバッグするには

1. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でプロジェクトを開きます。

2. 必要に応じて、ブレークポイントを作成します。

    Windows フォーム アプリケーションはイベント ドリブンであるため、ブレークポイントはイベント ハンドラー コード内またはイベント ハンドラー コードによって呼び出されるメソッド内に設定します。 ブレークポイントが配置される一般的なイベントは次のとおりです。

   1. Click、Enter などのコントロールに関連付けられたイベント。

   2. Load、Activated など、アプリケーションの起動またはシャットダウンに関連付けられたイベント。

   3. フォーカス イベントと検証イベント。

      詳細については、「[Windows フォーム内でのイベント ハンドラーの作成](/dotnet/framework/winforms/creating-event-handlers-in-windows-forms)」を参照してください。

3. **[デバッグ]** メニューの **[開始]** をクリックします。

4. 「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」で説明されている手法を使用してデバッグ ます。

## <a name="see-also"></a>関連項目
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [C#、F#、および Visual Basic のプロジェクト](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [方法: デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [Windows フォーム](/dotnet/framework/winforms/index)