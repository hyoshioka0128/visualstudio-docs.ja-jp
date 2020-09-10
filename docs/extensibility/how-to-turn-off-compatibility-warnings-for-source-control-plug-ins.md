---
title: ソース管理プラグインの警告をオフにする
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, turning off compatibility warnings
- compatibility warnings, turning off
ms.assetid: ba318e12-921b-4b7a-a8c2-12c712be1dbf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 33cf57aa86608cca96924faa2caeb9eec7fbdc0e
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89742771"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>方法: ソース管理プラグインの互換性に関する警告をオフにする

でソース管理を採用している場合、ユーザーにはいくつかの互換性の警告が表示されることがあり [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 表示される警告は、ソース管理プラグインの機能によって異なります。詳細については、こちらを参照してください。

### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>"Visual Studio との最適なソース管理の統合を保証するには" という警告を無効にするには

- 次のレジストリエントリを設定します (必要に応じて値を追加します)。

   **HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl\DontDisplayCheckDotNETCompatible = dword: 00000001**

   この警告は、すべての非プラグインに対して表示され [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] ます。

### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>"インストールされているソース管理プロバイダーは、すべての機能をサポートしていません" という警告を無効にするには

- 次の2つのレジストリ値を設定します (必要に応じて値を追加します)。

     **HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl\WarnedOldMSSCCIProvider = dword: 00000000**

    **HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl\UseOldSCC = dword: 00000001**

     この警告は、ソース管理プラグインが複数のプロジェクトの再入を明示的にサポートしていない場合 (つまり、一度に1つのファイルとプロジェクトだけをチェックインできる場合) に表示されます。

     再入 (機能) をサポートすることをお勧めします。そう `SCC_CAP_REENTRANT` しないと、この警告は削除されます。 ただし、このサポートが不可能な場合は、これらのレジストリエントリを設定できます。

## <a name="see-also"></a>関連項目

- [機能フラグ](../extensibility/capability-flags.md)
