---
title: コンポーネント管理 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], components
- installation [Visual Studio SDK], file management
ms.assetid: 029bffa2-6841-4caa-a41a-442467e1aedc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b5dcac9fb14a83021b852be2c52436fcdca84bf5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709335"
---
# <a name="component-management"></a>コンポーネント管理
Windows インストーラのタスクの単位は、Windows インストーラ コンポーネント (WIC またはコンポーネントと呼ばれることもあります) と呼ばれます。 GUID は、Windows インストーラを使用するセットアップのインストールと参照カウントの基本単位である各 WIC を識別します。

 VSPackage インストーラーを作成するのには、いくつかの製品を使用できますが、この説明では、Windows インストーラー (*.msi*) ファイルを使用することを前提としています。 インストーラーを作成する場合は、ファイルの配置を正しく管理して、常に正しい参照カウントが行われるようにする必要があります。 したがって、インストールとアンインストールのシナリオが混在する場合、製品の異なるバージョンが互いに干渉したり、中断したりしません。

 Windows インストーラでは、参照カウントはコンポーネント レベルで発生します。 リソース (ファイル、レジストリ エントリなど) をコンポーネントに慎重に編成する必要があります。 モジュール、機能、製品など、さまざまなシナリオで役立つ組織の他のレベルがあります。 詳細については、「 [Windows インストーラの基本](../../extensibility/internals/windows-installer-basics.md)」を参照してください。

## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>サイド バイ サイド インストールのオーサリング セットアップのガイドライン

- バージョン間で共有されるファイルとレジストリ キーを独自のコンポーネントに作成します。

     そうすることで、次のバージョンで簡単にそれらを消費することができます。 たとえば、グローバルに登録されているタイプ ライブラリ、ファイル拡張子 **、HKEY_CLASSES_ROOT**に登録されているその他のアイテムなど。

- 共有コンポーネントを別々のマージ モジュールにグループ化します。

     この方法は、サイド バイ サイド インストールを進める場合に、正しく作成するのに役立ちます。

- 複数のバージョンで同じ Windows インストーラ コンポーネントを使用して、共有ファイルとレジストリ キーをインストールします。

     別のコンポーネントを使用する場合、バージョン管理された VSPackage がアンインストールされたが、別の VSPackage がインストールされている場合、ファイルとレジストリ エントリがアンインストールされます。

- バージョン管理されたアイテムと共有アイテムを同じコンポーネントに混在させないでください。

     これにより、共有アイテムをグローバルな場所にインストールし、バージョン管理されたアイテムを分離された場所にインストールすることができなくなります。

- バージョン管理されたファイルを指す共有レジストリ キーを持っていません。

     これを行うと、別のバージョン付き VSPackage がインストールされたときに共有キーが上書きされます。 2 番目のバージョンを削除すると、キーが指しているファイルが削除されます。

## <a name="see-also"></a>関連項目
- [共有 VS パッケージとバージョン対応 VS パッケージの間で選択](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [VSPackage セットアップ シナリオ](../../extensibility/internals/vspackage-setup-scenarios.md)
