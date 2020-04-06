---
title: 相互運用機能アセンブリ コマンド ハンドラーの登録 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e2ab6389f1e0d369dd095290d12c97431c44155
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705858"
---
# <a name="registering-interop-assembly-command-handlers"></a>相互運用機能アセンブリ コマンド ハンドラーの登録
統合開発環境 (IDE)[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]がコマンドを適切にルーティングするように、VSPackage をに登録する必要があります。

 レジストリは、手動編集またはレジストラー (.rgs) ファイルを使用して更新できます。 詳細については、「 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)」を参照してください。

 マネージ パッケージ フレームワーク (MPF) は、<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute>クラスを通じてこの機能を提供します。

- [コマンド テーブル形式 リファレンス](https://msdn.microsoft.com/library/09e9c6ef-9863-48de-9483-d45b7b7c798f)リソースは、アンマネージ サテライト UI DLL にあります。

## <a name="command-handler-registration-of-a-vspackage"></a>VS パッケージのコマンド ハンドラー登録
 ユーザー インターフェイス (UI) ベースのコマンドのハンドラーとして機能する VSPackage には、VSPackage`GUID`に基づくレジストリ エントリが必要です。 このレジストリ エントリは、VSPackage の UI リソース ファイルとそのファイル内のメニュー リソースの場所を指定します。 レジストリ エントリ自体は、バージョン*\<>* が 9.0\\などのバージョンであるHKEY_LOCAL_MACHINE\ソフトウェア\Microsoft\VisualStudio[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]*\<バージョン>* \Menus の下にあります。

> [!NOTE]
> シェルが初期化されるときに、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*\<バージョン>* のルート パスを代替ルートでオーバーライドできます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ルート パスの詳細については、「 [Windows インストーラを使用した VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。

### <a name="the-ctmenu-resource-registry-entry"></a>CTMENU リソース レジストリ エントリ
 レジストリ エントリの構造は次のとおりです。

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\
  Menus\
    <GUID> = <Resource Information>
```

 \<*GUID*>は`GUID`、{XXXXXX-XXXX-XXXX-XXXX-Xxx-XXX-XXXXXXXXX}という形式のVSPackageのです。

 リソース情報>は、コンマで区切られた 3 つの要素で構成されます。 * \<* これらの要素は、次の順に示します。

 \<*リソース DLL>へのパス*、\<*メニュー リソース ID*>、\<*メニュー バージョン*>

 次の表は、\<*リソース情報*>のフィールドを示しています。

| 要素 | 説明 |
|---------------------------| - |
| \<*リソース DLL へのパス*> | これは、メニュー リソースを含むリソース DLL の完全パスであるか、または VSPackage のリソース DLL が使用されることを示す空白のままにします (VSPackage 自体が登録されているパッケージ サブキーで指定されている)。<br /><br /> このフィールドは空白のままにするのが一例です。 |
| \<*メニュー リソース ID*> | これは[、VSPackage](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)のすべての`CTMENU`UI 要素を含むリソースのリソース ID です。 |
| \<*メニューバージョン*> | これは、リソースのバージョンとして使用される数値です`CTMENU`。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、この値を使用して、リソースの内容をすべての`CTMENU``CTMENU`リソースのキャッシュに再結合する必要があるかどうかを判断します。 再マージは、devenv セットアップ コマンドを実行することによってトリガーされます。<br /><br /> この値は、最初は 1 に設定し、`CTMENU`リソース内の変更が行われるたびに、再マージが発生する前に増分されます。 |

### <a name="example"></a>例
 いくつかのリソースエントリの例を次に示します。

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\9.0Exp\
  Menus\
    {019971D6-4685-11D2-B48A-0000F87572EB} = ,1, 10
    {1b027a40-8f43-11d0-8d11-00a0c91bc942} = , 10211, 3
```

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)
