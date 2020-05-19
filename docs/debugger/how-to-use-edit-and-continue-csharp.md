---
title: '方法: エディット コンティニュを使用する (C#) | Microsoft Docs'
ms.date: 10/04/2018
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 515068f29045ef92ee7d2323f752ba2185f28cac
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62906272"
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
