---
title: ソース サーバーのセキュリティ警告 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.sourceserver.enablewarning
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 8451c281-6914-469c-b80c-6271cc3f3d17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 69511c2f83570abf37ef4bea8b71c8f59431a128
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729573"
---
# <a name="source-server-security-alert"></a>ソース サーバー のセキュリティ警告
ソース サーバーの使用時は、認識できて信頼できる場所からのシンボル ファイルのみを使用してください。

 ソース サーバーのサポートを有効にすると、この警告が表示されます。 ソース サーバーのコマンドは、デバッグ シンボル ファイル ( **\*.pdb** ファイル) に埋め込まれています。 PDB ファイルの作成元を確認してください。

> [!IMPORTANT]
> ソース サーバーを使用する場合、次の潜在的なセキュリティ上の脅威について考慮する必要があります。アプリケーションの PDB ファイルには任意のコマンドを埋め込むことができるため、srcsrv.ini ファイルには実行するコマンドのみ配置するようにします。 srcsvr.ini ファイルにないコマンドを実行しようとすると、確認のダイアログ ボックスが表示されます。 詳細については、「[セキュリティ警告: デバッガーは信頼されないコマンドを実行する必要があります](../debugger/security-warning-debugger-must-execute-untrusted-command.md)。 コマンド パラメーターでは何も検証されないため、コマンドを信頼するときは注意してください。 たとえば、cmd.exe を信頼した場合、悪意のあるユーザーが危険な動作を実行するようにコマンドにパラメーターを指定する可能性があります。

## <a name="see-also"></a>関連項目
- [シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [ソース サーバー](/windows/desktop/Debug/source-server-and-source-indexing)
