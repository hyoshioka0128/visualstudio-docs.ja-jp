---
title: エディット コンティニュ (Visual Basic) | Microsoft Docs
description: エディット コンティニュは、Visual Basic プロジェクトで使用できます。 どのような編集がサポートされているかについて、および編集の適用の可否とタイミングを制御する方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f5df9910d779a4c360a0c1f3b6482b5c51256d29
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99871924"
---
# <a name="edit-and-continue-visual-basic"></a>エディット コンティニュ (Visual Basic)
エディット コンティニュは、中断モードでの実行中にコードを変更できるようにするための、[!INCLUDE [vbprvb](../code-quality/includes/vbprvb_md.md)] 用デバッグ機能です。 コードの編集を適用した後で、新しい編集でコードの実行を再開して編集結果を確認できます。

 エディット コンティニュ機能は、中断モードで使用できます。 中断モードでは、命令ポインター (ソース ウィンドウ内の黄色の矢印) は、次に実行されるメソッドまたはプロパティ本体内の実行可能なステートメントを含む行を指します。

 エディット コンティニュは、デバッグ セッションで行う必要があるほとんどの変更をサポートしますが、いくつか例外があります。 詳細については、「[サポートされているコード変更 (C# および Visual Basic)](../debugger/supported-code-changes-csharp.md)」を参照してください。

 許可されない編集を行った場合は、その変更に紫色の波下線が表示され、タスク一覧にタスクが表示されます。 エディット コンティニュを引き続き使用するには、許可されない編集を元に戻さなければなりません。 エディット コンティニュの外部であれば、許可されない編集が認められる場合もあります。 そのような許可されない編集の結果を保持するには、デバッグを停止してアプリケーションを再起動する必要があります。

 エディット コンティニュは、Windows 10 用の UWP アプリで、および.NET Framework 4.6 デスクトップ以降のバージョンを対象とする x86 および x64 アプリでサポートされています (.NET Framework はデスクトップ バージョンのみです)。

 > [!NOTE]
 > サポートされていないアプリおよびプラットフォームとしては、ASP.NET 5、Silverlight 5、Windows 8.1 などがあります。

 **[プロセスにアタッチ]** を使用してデバッグを開始した場合は、エディット コンティニュはサポートされません。 エディット コンティニュは、最適化されたコードでも、マネージド コードとネイティブ コードの混合コードでもサポートされていません。 詳細については、「[サポートされているコード変更 (C# および Visual Basic)](../debugger/supported-code-changes-csharp.md)」を参照してください。

 このセクションの各トピックでは、この機能の使用方法と許可されない種類の変更について詳しく説明します。

## <a name="in-this-section"></a>このセクションの内容
 [方法: エディット コンティニュの中断モード時に編集を適用する](../debugger/how-to-apply-edits-in-break-mode-with-edit-and-continue.md) 中断モードにおいてコードの編集を適用する方法について説明します。

 [サポートされているコード変更 (C# および Visual Basic)](../debugger/supported-code-changes-csharp.md) [!INCLUDE [vb_current_short](../debugger/includes/vb_current_short_md.md)] エディット コンティニュで実行できない編集の種類について説明します。

## <a name="related-sections"></a>関連項目
 [エディット コンティニュ](../debugger/edit-and-continue.md) エディット コンティニュに関するトピックの一覧を提供します。
