---
title: エラー - サーバーに自動的にステップ インできません | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.causality_no_server_response
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, notification error
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 647f51314d5506e817fa6982aa693b62f62125cf
ms.sourcegitcommit: ed4372bb6f4ae64f1fd712b2b253bf91d9ff96bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89599917"
---
# <a name="error-unable-to-automatically-step-into-the-server"></a>エラー :サーバーに自動的にステップ インできません
このエラーは次のように表示されます。

 サーバーに自動的にステップ インできません。 デバッガーは、リモート プロシージャが実行される前に通知されませんでした。

 このエラーは、Web サービスにステップ インしようとすると発生することがあります (「 [XML Web サービスへのステップ イン](/previous-versions/zc57803s(v=vs.100))」を参照してください)。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] が正しくセットアップされていない場合に発生する可能性があります。

 考えられる原因:

- [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] アプリケーションの web.config ファイルでデバッグを "true" に設定していません (「 [方法: .NET アプリケーションのデバッグを有効にする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)」を参照してください)。

- いずれかのバージョンの [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] が Visual Studio のインストール後にインストールされました。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] は Visual Studio のインストール前にインストールする必要があります。 この問題を解決するには、Windows の **[コントロール パネル] で [プログラムと機能]** を使用して、Visual Studio のインストールを修復します。

## <a name="see-also"></a>関連項目
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Remote Debugging](../debugger/remote-debugging.md)