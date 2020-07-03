---
title: エラー - ASP.NET がインストールされていません |Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.http_not_supported
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Web applications, errors
- debugger, Web application errors
- error messages, ASP.NET
- ASP.NET, installation error messages
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: 3a768a1a3a0295190701cacc9bbf017baee507b7
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460906"
---
# <a name="error-aspnet-not-installed"></a>エラー :ASP.NET がインストールされていません
このエラーは、デバッグを実行しようとしているコンピューターに [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] が正しくインストールされていない場合に発生します。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] がインストールされていないか、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] がインストールされてから IIS がインストールされた可能性があります。

### <a name="to-reinstall-aspnet"></a>ASP.NET を再インストールするには

1. コマンド プロンプト ウィンドウで、次のコマンドを実行します。

   ```cmd
   \WINDOWS\Microsoft.NET\Framework\version\aspnet_regiis -i
   ```

    *version* は、コンピューターにインストールされている .NET Framework のバージョン番号です (v1.0.370 など)。 `\WINDOWS\Microsoft.NET\Framework` ディレクトリを見ることで、.Net Framework のバージョンを確認できます。

   > [!NOTE]
   > Windows Server 2003 の場合は、コントロール パネルの **[プログラムの追加と削除]** を使って [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] をインストールできます。

## <a name="see-also"></a>関連項目
- [Web アプリケーションのデバッグ: エラーとトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
