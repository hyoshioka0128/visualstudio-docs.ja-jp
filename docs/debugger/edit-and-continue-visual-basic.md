---
title: エディット コンティニュ (Visual Basic) |Microsoft Docs
ms.date: 10/11/2017
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue, 64-bit
- Edit and Continue [Visual Basic]
- debugging [Visual Basic], Edit and Continue
- Visual Basic, Edit and Continue
- 64-bit Edit and Continue
ms.assetid: 7e90f34f-e699-45ab-a4c9-a4b527c498c8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f73b67ac4268c04dfa9ff7ab020891623f528f9b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62851260"
---
# <a name="edit-and-continue-visual-basic"></a>エディット コンティニュ (Visual Basic)
エディット コンティニュは、中断モードでの実行中にコードを変更できるようにするための、[!INCLUDE [vbprvb](../code-quality/includes/vbprvb_md.md)] 用デバッグ機能です。 コードの編集を適用した後で、新しい編集でコードの実行を再開して編集結果を確認できます。

 エディット コンティニュ機能は、中断モードで使用できます。 中断モード、命令ポインター、ソース ウィンドウで黄色の矢印では、ポイントとなるメソッドまたはプロパティ本体の実行可能なステートメントを含む行には、[次へ] を実行します。

 エディット コンティニュは、デバッグ セッションで行う必要があるほとんどの変更をサポートしますが、いくつか例外があります。 詳細については、次を参照してください。 [(c# および Visual Basic) のサポートされているコード変更](../debugger/supported-code-changes-csharp.md)します。

 許可されない編集を行った場合は、その変更に紫色の波下線が表示され、タスク一覧にタスクが表示されます。 エディット コンティニュを引き続き使用するには、許可されない編集を元に戻さなければなりません。 エディット コンティニュの外部であれば、許可されない編集が認められる場合もあります。 そのような許可されない編集の結果を保持するには、デバッグを停止してアプリケーションを再起動する必要があります。

 Windows 10 用 UWP アプリと .NET Framework 4.6 を対象とする x86 および x64 のアプリでエディット コンティニュはサポートされてデスクトップまたはそれ以降のバージョン (.NET Framework は、デスクトップ バージョンのみ)。

 > [!NOTE]
 > サポートされていないアプリとプラットフォームには、ASP.NET 5、Silverlight 5、および Windows 8.1 が含まれます。

 **[プロセスにアタッチ]** を使用してデバッグを開始した場合は、エディット コンティニュはサポートされません。 最適化されたコードまたは混合にエディット コンティニュがサポートされていないマネージ コードとネイティブ コード。 詳細については、次を参照してください。 [(C# および Visual Basic) のサポートされているコード変更](../debugger/supported-code-changes-csharp.md)します。

 このセクションの各トピックでは、この機能の使用方法と許可されない種類の変更について詳しく説明します。

## <a name="in-this-section"></a>このセクションの内容
 [方法: エディット コンティニュの中断モードで編集を適用](../debugger/how-to-apply-edits-in-break-mode-with-edit-and-continue.md)中断モードでコードの編集を適用する方法について説明します。

 [サポートされるコードの変更 (C#および Visual Basic)](../debugger/supported-code-changes-csharp.md)できない編集の種類について説明しますで実行される[!INCLUDE [vb_current_short](../debugger/includes/vb_current_short_md.md)]エディット コンティニュ。

## <a name="related-sections"></a>関連項目
 [エディット コンティニュ](../debugger/edit-and-continue.md)エディット コンティニュに関するトピックの一覧を提供します。
