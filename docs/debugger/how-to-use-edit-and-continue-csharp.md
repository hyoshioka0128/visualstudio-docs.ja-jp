---
title: エディット コンティニュを使用する (C#) | Microsoft Docs
description: エディット コンティニュを使用して、Visual Studio でデバッグ セッションを停止して再開することなく、デバッグ中に中断モードでコードに変更を加えます。
ms.custom: SEO-VS-2020
ms.date: 10/04/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], about Edit and Continue
ms.assetid: 40e136d8-a08c-43bd-b313-fb821c55eb3c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: ed538c49aeb1257b165d7cfecab0352dd0deb488
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889175"
---
# <a name="how-to-use-edit-and-continue-c"></a>方法: エディット コンティニュを使用する (C#)
C# のエディット コンティニュを使用すると、デバッグ セッションを停止して再開することなく、デバッグ中に中断モードでコードに変更を加えることができます。

C# のエディット コンティニュは、中断モードでコードの変更を行うと自動的に発生します。その後、 **[続行]** 、 **[ステップ]** 、または **[次のステートメントの設定]** を使用してデバッグを続行するか、デバッガー ウィンドウで関数を評価します。

詳細については、「[エディット コンティニュ (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)」を参照してください。

>[!NOTE]
>最適化されたコード、混合コード、または SQL Server の共通言語ランタイム (CLR) との統合コードについては、エディット コンティニュはサポートされません。 サポートされていないその他のシナリオについては、「[サポートされているコード変更 (C# および Visual Basic)](../debugger/supported-code-changes-csharp.md)」を参照してください。 これらのシナリオのいずれかでエディット コンティニュを適用しようとすると、エディット コンティニュがサポートされないことを伝えるメッセージ ボックスが表示されます。

**エディット コンティニュを有効または無効にするには:**

1. デバッグ セッション中は、デバッグを停止します ( **[デバッグ]**  >  **[停止]** 、または **Shift**+**F5** キー)。

1. **[ツール]**  >  **[オプション]** (または **[デバッグ]**  >  **[オプション]** ) > **[デバッグ]**  >  **[全般]** で **[エディット コンティニュを有効にする]** チェックボックスをオンまたはオフにします。

デバッグ セッションを開始または再開すると、この設定が有効になります。

**エディット コンティニュを使用するには:**

1. デバッグ中は、中断モードでソース コードを変更します。

1. **[デバッグ]** メニューの **[続行]** 、 **[ステップ]** 、または **[次のステートメントの設定]** をクリックするか、デバッガー ウィンドウに表示された関数を評価します。

   その新しい、コンパイルされたコードでデバッグが続行されます。

エディット コンティニュでサポートされないコードの種類の変更もあります。 詳細については、「[サポートされているコード変更 (C# および Visual Basic)](../debugger/supported-code-changes-csharp.md)」を参照してください。
