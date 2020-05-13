---
title: ソース管理プラグインの互換性警告をオフにする |マイクロソフトドキュメント
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
ms.openlocfilehash: 22dd3821426aa1dae6265c520ddac60dd93e1c5e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710723"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>方法: ソース管理プラグインの互換性警告をオフにする
でソース管理を使用すると、互換性に関する警告が[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]いくつか表示されることがあります。 表示される警告は、ソース管理プラグインの機能によって異なります。

### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>警告を無効にするには:"Visual Studio との最適なソース管理の統合を確保するには"

- 次のレジストリ エントリを設定します (必要に応じて値を追加します)。

   **HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\8.0\ソースコントロール\ドントディスプレイチェックドットネット互換性 = dword:00000001**

   この警告は、すべての非[!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)]プラグインに対して表示されます。

### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>警告を無効にするには:"インストールされているソース管理プロバイダは、すべての機能をサポートしていません"

- 次の 2 つのレジストリ値を設定します (必要に応じて値を追加します)。

     **HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\8.0\ソースコントロール\警告OldMSSCCIプロバイダー = dword:00000000**

    **HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\8.0\ソースコントロール\使用OldSCC = dword:00000001**

     この警告は、ソース管理プラグインが複数のプロジェクトの再入を明示的にサポートしていない場合 (つまり、一度に 1 つのファイルとプロジェクトのみをチェックインできる場合) に表示されます。

     再入性 (能力)`SCC_CAP_REENTRANT`をサポートするのが最善です。この操作を行うと、この警告は削除されます。 ただし、このサポートが不可能な場合は、これらのレジストリ エントリを設定できます。

## <a name="see-also"></a>関連項目
- [機能フラグ](../extensibility/capability-flags.md)
