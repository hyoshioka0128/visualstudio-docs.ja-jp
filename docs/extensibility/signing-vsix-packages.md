---
title: VSIX パッケージに署名する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- signature
- signing
- authenticode
- vsix
- packages
ms.assetid: e34cfc2c-361c-44f8-9cfe-9f2be229d248
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17179c35496fc19322c5bb951f4d04bc28e5d7bc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700088"
---
# <a name="signing-vsix-packages"></a>VSIX パッケージの署名
拡張機能アセンブリは、Visual Studio で実行する前に署名する必要はありませんが、これを行うことをお勧めします。

 拡張機能をセキュリティで保護し、改ざんされていないことを確認する場合は、VSIX パッケージにデジタル署名を追加できます。 VSIX が署名されると、VSIX インストーラーは、署名されていることを示すメッセージに加えて、署名自体に関する詳細情報を表示します。 VSIX の内容が変更され、VSIX が再び署名されていない場合、VSIX インストーラーは、署名が無効であることを示します。 インストールは停止されませんが、ユーザーに警告が表示されます。

> [!IMPORTANT]
> Visual Studio 2015 以降では、SHA256 暗号化以外の機能を使用して署名された VSIX パッケージは、無効な署名を持つものとして識別されます。 VSIX のインストールはブロックされませんが、ユーザーに警告が表示されます。

## <a name="signing-a-vsix-with-vsixsigntool"></a>を使用して VSIX に署名する
 [VsixSignTool](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool)の nuget.org で[VisualStudio の拡張性](https://www.nuget.org/profiles/VisualStudioExtensibility)から利用できる SHA256 暗号化署名ツールがあります。

#### <a name="to-use-the-vsixsigntool"></a>を使用するには

1. VSIX をプロジェクトに追加します。

2. ソリューション エクスプローラーでプロジェクト ノードを右クリックし **、[NuGet パッケージの追加&#124;を選択**します。  NuGet と NuGet パッケージの追加の詳細については[、NuGet のドキュメント](/NuGet)と[パッケージ マネージャーの UI](/NuGet/Tools/Package-Manager-UI)のトピックを参照してください。

3. 拡張機能から VSIXSignTool を検索し、NuGet パッケージをインストールします。

4. これで、プロジェクトのローカル パッケージの場所から VSIXSignTool を実行できます。 署名シナリオについては、ツールのコマンド ライン ヘルプを参照してください (VSIXSignTool.exe /?

   たとえば、パスワードで保護された証明書ファイルで署名する場合:

   VSIX ファイル> /p パスワード> /f\<\<証明書ファイルに署名します> \<

## <a name="see-also"></a>関連項目
- [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)
