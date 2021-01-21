---
title: VSIX パッケージに署名しています |Microsoft Docs
description: 拡張機能アセンブリに署名する方法について説明します。 VSIX インストーラーには、VSIX に署名されたことを示すメッセージと、その署名自体に関する情報が表示されます。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: e9152e45b402294dfd0bbb41bfda2c685588f01e
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97716082"
---
# <a name="signing-vsix-packages"></a>VSIX パッケージの署名
拡張機能アセンブリは、Visual Studio で実行する前に署名する必要はありませんが、これを行うことをお勧めします。

 拡張機能をセキュリティで保護し、改ざんされていないことを確認するには、VSIX パッケージにデジタル署名を追加します。 VSIX が署名されると、VSIX インストーラーには、その VSIX が署名されていることを示すメッセージが表示され、さらに署名自体に関する情報も表示されます。 Vsix の内容が変更されていて、VSIX が再度署名されていない場合は、その署名が無効であることが VSIX インストーラーによって表示されます。 インストールは停止されませんが、ユーザーに警告が出てきます。

> [!IMPORTANT]
> Visual Studio 2015 以降では、SHA256 暗号化以外のものを使用して署名された VSIX パッケージは、無効な署名があるものとして識別されます。 VSIX のインストールはブロックされませんが、ユーザーに警告が表示されます。

## <a name="signing-a-vsix-with-vsixsigntool"></a>VSIXSignTool を使用した VSIX への署名
 Nuget.org の[VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility)では、SHA256 暗号化署名ツールを使用でき[ます。](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool)

#### <a name="to-use-the-vsixsigntool"></a>VSIXSignTool を使用するには

1. プロジェクトに VSIX を追加します。

2. ソリューションエクスプローラーでプロジェクトノードを右クリックし、[ **&#124; 追加] [NuGet パッケージの管理**] の順に選択します。  Nuget と NuGet パッケージの追加の詳細については、 [nuget のドキュメント](/NuGet) と [パッケージマネージャーの UI](/NuGet/Tools/Package-Manager-UI) に関するトピックを参照してください。

3. VisualStudioExtensibility から VSIXSignTool を検索し、NuGet パッケージをインストールします。

4. これで、プロジェクトのローカルパッケージの場所から VSIXSignTool を実行できるようになりました。 署名シナリオ (VSIXSignTool.exe/?) については、ツールのコマンドラインヘルプを参照してください。

   たとえば、パスワードで保護された証明書ファイルで署名するには、次のようにします。

   VSIXSignTool.exe サインイン/f \<certfile> /p \<password>\<VSIXfile>

## <a name="see-also"></a>関連項目
- [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)
