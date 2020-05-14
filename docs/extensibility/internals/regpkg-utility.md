---
title: RegPkg ユーティリティ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- regpkg, registration utility
- registration, regpkg utility
ms.assetid: 1683ee18-59d1-4bab-a674-dd00dd960de3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cebfd7a9782a2760eb33f7e56bfe16b126fc6251
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705638"
---
# <a name="regpkg-utility"></a>RegPkg ユーティリティ
> [!NOTE]
> Visual Studio でパッケージを登録する場合は、.pkgdef ファイルを使用する方法が推奨されます。 これにより、VSIX の展開に必要なシステム レジストリにアクセスしなくても、拡張機能の展開が可能になります。 Pkgdef ファイルは[、CreatePkgDef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を使用して作成されます。 Visual Studio パッケージの展開の詳細については、「 [Visual Studio 拡張機能の配布](../../extensibility/shipping-visual-studio-extensions.md)」を参照してください。

 RegPkg.exe ユーティリティは VSPackage を[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]登録し、展開の準備をします。 このユーティリティは、VSPackage 開発の際にバックグラウンドで使用されます。 これは、テスト用ハイブで VSPackage をビルドして実行できるように、ビルド プロセスの一部として実行されます。

 RegPkg は、システム レジストリ スクリプトを複数の形式で生成できます。 これらのスクリプトは、.msi プロジェクトや Windows インストーラ XML ツールセット ファイルなどの配置プロジェクトに組み込むことができます。

 通常\<*、Visual Studio SDK*のインストール パス>\VisualStudioIntegration\ツール\ビン\RegPkg.exe にあります。 RegPkg は次の構文に従います。

```
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath
```

 /root:root 指定された下で登録を実行します

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ルート。

 /regfile:ファイル名 レジストリを更新するのではなく、.reg ファイルを作成します。  /vrgfile または /rgsfile または /wixfile では使用できません。

 /rgsfile:ファイル名 レジストリを更新するのではなく、.rgs ファイルを作成します。  /vrgfile または /regfile または /wixfile では使用できません。

 /vrgfile:ファイル名 レジストリを更新するのではなく、.vrgファイルを作成します。  /regfile または /rgsfile または /wixfile では使用できません。

 /rgm rgs ファイルに加えて .rgm ファイルを作成します。  /rgsfile と組み合わせる必要があります。

 /wixfile:ファイル名 レジストリを更新するのではなく、Windows インストーラ XML ツールセット互換ファイルを作成します。  /regfile または /rgsfile または /vrgfile では使用できません。

 /コードベース アセンブリではなく、コードベースで登録を強制します。

 /assembly は、コードベースではなく、アセンブリで登録を強制します。

 /登録解除 このパッケージの登録を解除します。  使用できません

 を /regfile または /vrgfile または /rgsfile または /wixfile と共に使用します。

## <a name="see-also"></a>関連項目
- [VSPackages](../../extensibility/internals/vspackages.md)
- [RegPkg パッケージ登録のトラブルシューティング](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)
