---
title: 'テスト領域 8: プラグインの切り替え |Microsoft Docs'
description: このソース管理テスト領域には、Visual Studio のソリューションソースコントロールに使用するプラグインを選択するためのテストケースが用意されています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], switching plug-ins
- source control plug-ins, switching
ms.assetid: 01370792-b5da-4e46-9ce2-7dd326587141
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 50cbf92b8214e605976aec58aaea984276ca8cc6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99848209"
---
# <a name="test-area-8-plug-in-switching"></a>テスト領域 8: プラグインの切り替え
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE: integrated development environment) には、現在のソース管理プラグインを変更するためのユーザーインターフェイス (UI) が用意されています。 このテスト領域には、ソリューションのソース管理に使用するプラグインを選択するプロセスのテストケースが表示されます。

## <a name="command-menu-access"></a>コマンドメニューへのアクセス
 テストケースでは、次の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境メニューパスが使用されます。

- 現在のソース管理プラグイン:**ツール**  ->  **オプション**  ->  の **ソース管理**  ->  **プラグインの選択**。

- ソース管理のバインドの変更:**ファイル**  ->  **ソース管理**  ->  の **ソース管理の変更**...

## <a name="common-expected-behavior"></a>想定される一般的な動作
 ソリューションのソース管理プラグインを変更するには、Visual Studio を終了するか、ソリューションを再読み込みする必要があります。 さらに、現在のソース管理プラグインは、ソリューションが読み込まれるときに、ソリューションによって使用されているものに自動的に変更されます。

## <a name="test-cases"></a>テスト ケース
 次に示すのは、プラグインの切り替えテスト領域の特定のテストケースです。

### <a name="case-8a-automatic-change"></a>ケース 8a: 自動変更

#### <a name="expected-behavior"></a>想定されている動作
 ユーザーがソース管理下にあるソリューションを読み込むと、ソリューションが自動的に読み込まれ、適切なソース管理プラグインが現在のものとして選択されます。

| 操作 | テストステップ | 確認が必要な結果 |
| - | - | - |
| ソース管理プラグインの自動変更 | 1. [現在のものとしてテスト] で [プラグイン] を選択します ([**ツール**  ->  **オプション]**[  ->  **ソース管理**] [  ->  **プラグインの選択**]。<br />2. 新しいプロジェクトを作成します。<br />3. ソリューションをソース管理に追加します。<br />4. 別のプラグインを選択します (例: [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] )。<br />5. ソリューションのアンロードプロンプトを受け入れます。<br />6. ディスクからソリューションを再度開きます。 | ソリューションが開かれています。<br /><br /> テスト中のプラグインは、現在のソース管理プラグインです。 |

### <a name="case-8b-solution-based-change"></a>ケース 8b: ソリューションベースの変更

#### <a name="expected-behavior"></a>想定されている動作
 ソリューションには、関連付けられたソース管理プラグインを変更することができます。

| 操作 | テストステップ | 確認が必要な結果 |
|----------------------------------| - | - |
| ソリューションのプラグインの変更 | 1. [現在のものとして **テスト] の**[プラグイン] を選択  ->  します。  ->    ->  <br />2. 新しいプロジェクトとソリューションを作成します。<br />3. ソリューションをソース管理に追加します。<br />4. ソース管理からソリューションのバインドを解除します ([ **ソース管理の変更** ] ダイアログボックスを使用します)。<br />5. 別のプラグインを選択します (例: [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] )。<br />6. アンロードされた場合は、ディスクからソリューションを再読み込みします。<br />7. ソリューションをソース管理に追加します。<br />8. ソース管理からソリューションのバインドを解除します ([ **ソース管理の変更** ] ダイアログボックスを使用します)。<br />9. テストの [プラグイン] をもう一度選択します。<br />10. アンロードされた場合は、ディスクからソリューションを再読み込みします。<br />11. [ **ソース管理の変更** ] ダイアログボックスを使用して、ソリューションを元の場所にバインドします。 | ソリューションは、選択したプラグインを使用してソース管理に追加されます。 |

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン向けのテスト ガイド](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
