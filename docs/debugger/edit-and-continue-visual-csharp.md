---
title: エディット コンティニュ (Visual C#) | Microsoft Docs
description: エディット コンティニュは、Visual C# プロジェクトで使用できます。 どのような編集がサポートされているかについて、および編集の適用の可否とタイミングを制御する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/11/2017
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Edit and Continue
- Edit and Continue [C#]
- debugging [C#], Edit and Continue
ms.assetid: 591bd1b7-ef10-4d10-817b-3f92ca4be006
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 375e1db598f925a193def159203ccb7e5c5fdf05
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99871859"
---
# <a name="edit-and-continue-visual-c"></a>エディット コンティニュ (Visual C#)
 C# のエディット コンティニュを使用すると、デバッグ中に中断モードでコードに変更を加えることができます。 デバッグ セッションを停止したり再開したりしなくても、変更を適用できます。 実行モードでは、ソース エディターは読み取り専用です。

 エディット コンティニュは、デバッグ セッションで行う必要があるほとんどの変更をサポートしますが、いくつか例外があります。 詳細については、「[サポートされているコード変更 (C# および Visual Basic)](../debugger/supported-code-changes-csharp.md)」を参照してください。

 エディット コンティニュは、Windows 10 の UWP と、.NET Framework 4.6 デスクトップ以降のバージョンを対象とする x86 および x64 アプリでサポートされています (.NET Framework はデスクトップ バージョンのみです)。

 > [!NOTE]
 > サポートされていないアプリおよびプラットフォームとしては、Silverlight 5、Windows 8.1 などがあります。

 エディット コンティニュが有効なときは、 **[続行]** 、 **[ステップ]** 、 **[次のステートメントの設定]** などのデバッガー実行コマンドを使用したり、デバッガー ウィンドウで関数の評価を実行したりすると、サポートされている変更が自動的に適用されます。

 詳細については、[エディット コンティニュを使用する (C#)](../debugger/how-to-use-edit-and-continue-csharp.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: エディット コンティニュを使用する (C#)](../debugger/how-to-use-edit-and-continue-csharp.md)
- [サポートされているコード変更 (C# および Visual Basic)](../debugger/supported-code-changes-csharp.md)
- [Visual Studio での XAML ホットリロードを使用した実行中の XAML コードの作成とデバッグ](../xaml-tools/xaml-hot-reload.md)
