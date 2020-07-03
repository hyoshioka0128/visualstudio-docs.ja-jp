---
title: エラー - SQL が SSDEBUGPS を見つけることができません | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.sqlde_cant_find_ssdebugps
dev_langs:
- CSharp
- VB
- FSharp
- C++
- SQL
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: edebb932e11554b24296314817eea514743525b1
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460508"
---
# <a name="error-sql-can39t-find-ssdebugps"></a>エラー :SQL が SSDEBUGPS を見つけることができません

SSDEBUGPS.dll は、SQL Server のデバッグ ホスト コンポーネントです。

このエラーはデバッグの開始時に発生し、指定されたファイルが [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] コンピューターに存在しないことを示します。 リモート デバッグのセットアップが実行されていない、または何らかの理由でこのファイルが削除されていることが原因として考えられます。

このエラーの解決方法は 2 つあります。1 つは、リモート デバッグのセットアップを再実行する方法です。もう 1 つは、このファイルを [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] コンピューターにコピーする方法です。

リモート デバッグのセットアップを再実行する場合は、「[リモート デバッグ](../debugger/remote-debugging.md)」の手順に従います。

ssdebugps.dll のファイルを見つけることができる場合は、これを [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] コンピューターにコピーします。 このファイルが存在する場合は、\Program Files\ Common Files\Microsoft Shared\SQL Debugging にあります。 これは、別の [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] コンピューターや、Visual Studio 2005 がインストールされているコンピューターにある場合もあります。

SSDEBUGPS.dll を SQL Server 2005 コンピューターにコピーするには:

1. [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] コンピューターの上記の名前とパスを持つディレクトリにファイルをコピーします。

2. **コマンド プロンプト**を開き、次のコマンドを実行してファイルを登録します。

    ```cmd
    regsvr32 ssdebugps.dll
    ```
