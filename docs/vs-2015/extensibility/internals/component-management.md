---
title: コンポーネントの管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], components
- installation [Visual Studio SDK], file management
ms.assetid: 029bffa2-6841-4caa-a41a-442467e1aedc
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 56a110f382d0b182eed0ea1a95cd4dabf2877037
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191859"
---
# <a name="component-management"></a>コンポーネント管理
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Windows インストーラー内のタスクの単位は、Windows インストーラーコンポーネント (WICs またはコンポーネントとも呼ばれます) と呼ばれます。 GUID は、各 WIC を識別します。これは、インストールの基本単位であり、Windows インストーラーを使用するセットアップの参照カウントです。  
  
 いくつかの製品を使用して VSPackage インストーラーを作成することもできますが、この説明では Windows インストーラー (.msi) ファイルを使用することを前提としています。 インストーラーを作成するときに、正しい参照カウントが常に発生するように、ファイルの配置を正しく管理する必要があります。 このため、インストールとアンインストールのシナリオでは、製品のバージョンによって相互に干渉したり、相互に侵入したりすることはありません。  
  
 Windows インストーラーでは、参照カウントはコンポーネントレベルで発生します。 リソース (ファイル、レジストリエントリなど) をコンポーネントに慎重に整理する必要があります。 さまざまなシナリオで役立つ、モジュール、機能、製品など、他のレベルの組織があります。 詳細については、「 [Windows インストーラーの基礎](../../extensibility/internals/windows-installer-basics.md)」を参照してください。  
  
## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>サイドバイサイドインストールのセットアップの作成に関するガイドライン  
  
- バージョン間で共有されるファイルとレジストリキーを独自のコンポーネントに作成します。  
  
     これにより、次のバージョンで簡単に使用できるようになります。 たとえば、グローバル、ファイル拡張子、HKEY_CLASSES_ROOT に登録されているその他の項目などに登録されているタイプライブラリなどです。  
  
- 共有コンポーネントを別々のマージモジュールにグループ化します。  
  
     これにより、をサイドバイサイドで正しく作成することができます。  
  
- 同じ Windows インストーラーコンポーネントを複数のバージョンで使用して、共有ファイルとレジストリキーをインストールします。  
  
     別のコンポーネントを使用する場合、1つのバージョン付き VSPackage がアンインストールされても、別の VSPackage がまだインストールされていると、ファイルとレジストリエントリはアンインストールされます。  
  
- 同じコンポーネントにバージョン管理された項目と共有項目を混在させないでください。  
  
     これにより、グローバルな場所に共有アイテムをインストールしたり、アイテムを分離された場所にバージョン管理したりすることができなくなります。  
  
- バージョン管理されたファイルを指す共有レジストリキーがありません。  
  
     この場合、別のバージョンの VSPackage がインストールされていると、共有キーは上書きされます。 2番目のバージョンを削除すると、キーが指しているファイルが消えます。  
  
## <a name="see-also"></a>参照  
 [共有バージョンとバージョン付き Vspackage の選択](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)   
 [VSPackage のセットアップ シナリオ](../../extensibility/internals/vspackage-setup-scenarios.md)
