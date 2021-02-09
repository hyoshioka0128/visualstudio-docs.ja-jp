---
title: コンポーネントの管理 |Microsoft Docs
description: Visual Studio で VSPackage インストーラーを作成するときに Windows インストーラーコンポーネントを管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], components
- installation [Visual Studio SDK], file management
ms.assetid: 029bffa2-6841-4caa-a41a-442467e1aedc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 44ee1a3afe313cdc11bb28e0a24a89e3e3ad7f0c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852727"
---
# <a name="component-management"></a>コンポーネント管理
Windows インストーラー内のタスクの単位は、Windows インストーラーコンポーネント (WICs またはコンポーネントとも呼ばれます) と呼ばれます。 GUID は、各 WIC を識別します。これは、インストールの基本単位であり、Windows インストーラーを使用するセットアップの参照カウントです。

 いくつかの製品を使用して VSPackage インストーラーを作成することもできますが、この説明では Windows インストーラー (*.msi*) ファイルを使用することを前提としています。 インストーラーを作成するときに、正しい参照カウントが常に発生するように、ファイルの配置を正しく管理する必要があります。 このため、インストールとアンインストールのシナリオでは、製品のバージョンによって相互に干渉したり、相互に侵入したりすることはありません。

 Windows インストーラーでは、参照カウントはコンポーネントレベルで発生します。 リソース (ファイル、レジストリエントリなど) をコンポーネントに慎重に整理する必要があります。 さまざまなシナリオで役立つ、モジュール、機能、製品など、他のレベルの組織があります。 詳細については、「 [Windows インストーラーの基礎](../../extensibility/internals/windows-installer-basics.md)」を参照してください。

## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>サイドバイサイドインストールのセットアップの作成に関するガイドライン

- バージョン間で共有されるファイルとレジストリキーを独自のコンポーネントに作成します。

     これにより、次のバージョンで簡単に使用できるようになります。 たとえば、グローバル、ファイル拡張子、 **HKEY_CLASSES_ROOT** に登録されているその他の項目などに登録されているタイプライブラリなどです。

- 共有コンポーネントを別々のマージモジュールにグループ化します。

     この戦略は、並列インストールを進めるために正しく作成するのに役立ちます。

- 同じ Windows インストーラーコンポーネントを複数のバージョンで使用して、共有ファイルとレジストリキーをインストールします。

     別のコンポーネントを使用する場合、1つのバージョン付き VSPackage がアンインストールされても、別の VSPackage がまだインストールされていると、ファイルとレジストリエントリはアンインストールされます。

- 同じコンポーネントにバージョン管理された項目と共有項目を混在させないでください。

     これにより、グローバルな場所に共有アイテムをインストールしたり、アイテムを分離された場所にバージョン管理したりすることができなくなります。

- バージョン管理されたファイルを指す共有レジストリキーがありません。

     この場合、別のバージョンの VSPackage がインストールされていると、共有キーは上書きされます。 2番目のバージョンを削除すると、キーが指しているファイルが消えます。

## <a name="see-also"></a>関連項目
- [共有バージョンとバージョン付き Vspackage を選択する](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [VSPackage セットアップシナリオ](../../extensibility/internals/vspackage-setup-scenarios.md)
