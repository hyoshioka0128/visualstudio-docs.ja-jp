---
title: 相互運用機能アセンブリの登録コマンドハンドラー |Microsoft Docs
description: 相互運用機能アセンブリを使用してコマンドを実装するすべての Vspackage で使用される基本的なコマンドコントラクトについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 641a21658e490f94a27cbd9120d044539a7ec284
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062760"
---
# <a name="registering-interop-assembly-command-handlers"></a>相互運用機能アセンブリ コマンド ハンドラーの登録
VSPackage は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) によってコマンドが適切にルーティングされるように、に登録する必要があります。

 レジストリを更新するには、手動で編集するか、レジストラー (.rgs) ファイルを使用します。 詳細については、「 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)」を参照してください。

 マネージパッケージフレームワーク (MPF) は、クラスを通じてこの機能を提供し <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> ます。

- [コマンドテーブル形式の参照](/previous-versions/bb164647(v=vs.100)) リソースは、アンマネージサテライト UI dll にあります。

## <a name="command-handler-registration-of-a-vspackage"></a>VSPackage のコマンドハンドラーの登録
 ユーザーインターフェイス (UI) ベースのコマンドのハンドラーとして機能する VSPackage には、VSPackage の後にという名前のレジストリエントリが必要です `GUID` 。 このレジストリエントリは、VSPackage の UI リソースファイルとそのファイル内の menu リソースの場所を指定します。 レジストリエントリ自体は HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudioメニューの下にあり \\ *\<Version>* ます。ここで、 *\<Version>* は、9.0 などののバージョンです [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

> [!NOTE]
> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudioのルートパスは、 \\ *\<Version>* シェルの初期化時に代替ルートでオーバーライドでき [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 ルートパスの詳細については、「 [Windows インストーラーを使用した Vspackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。

### <a name="the-ctmenu-resource-registry-entry"></a>CTMENU リソースレジストリエントリ
 レジストリエントリの構造は次のとおりです。

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\
  Menus\
    <GUID> = <Resource Information>
```

 \<*GUID*> は、 `GUID` {VSPackage} という形式の、XXXXXXXXX の形式です。

 *\<Resource Information>* コンマで区切られた3つの要素で構成されます。 これらの要素の順序は次のとおりです。

 \<*Path to Resource DLL*>, \<*Menu Resource ID*>, \<*Menu Version*>

 次の表では、のフィールドについて説明し \<*Resource Information*> ます。

| 要素 | 説明 |
|---------------------------| - |
| \<*Path to Resource DLL*> | これは、メニューリソースを含むリソース DLL への完全なパスです。これは、VSPackage のリソース DLL が使用されることを示します。これは、VSPackage 自体が登録されている Packages サブキーで指定されています。<br /><br /> 慣例として、このフィールドは空白にしておきます。 |
| \<*Menu Resource ID*> | これは、 `CTMENU` VSPackage ファイルからコンパイルされた、すべての UI 要素を含むリソースのリソース ID[です。](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) |
| \<*Menu Version*> | これは、リソースのバージョンとして使用される番号です `CTMENU` 。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、この値を使用して、リソースの内容を `CTMENU` すべてのリソースのキャッシュと再マージする必要があるかどうかを判断し `CTMENU` ます。 Devenv のセットアップコマンドを実行すると、再マージがトリガーされます。<br /><br /> この値は、最初に1に設定し、リソースのすべての変更の後、再 `CTMENU` マージが発生する前にインクリメントする必要があります。 |

### <a name="example"></a>例
 いくつかのリソースエントリの例を次に示します。

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\9.0Exp\
  Menus\
    {019971D6-4685-11D2-B48A-0000F87572EB} = ,1, 10
    {1b027a40-8f43-11d0-8d11-00a0c91bc942} = , 10211, 3
```

## <a name="see-also"></a>こちらもご覧ください
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)