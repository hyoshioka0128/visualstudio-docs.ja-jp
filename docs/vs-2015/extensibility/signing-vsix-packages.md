---
title: VSIX パッケージに署名しています |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- signature
- signing
- authenticode
- vsix
- packages
ms.assetid: e34cfc2c-361c-44f8-9cfe-9f2be229d248
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a4efaaa78ce593d8b97d1df454a9c30c2e62d9f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75918740"
---
# <a name="signing-vsix-packages"></a>VSIX パッケージの署名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

拡張機能アセンブリは、Visual Studio で実行する前に署名する必要はありませんが、これを行うことをお勧めします。  
  
 拡張機能をセキュリティで保護し、改ざんされていないことを確認するには、VSIX パッケージにデジタル署名を追加します。 VSIX が署名されると、VSIX インストーラーには、その VSIX が署名されていることを示すメッセージが表示され、さらに署名自体に関する情報も表示されます。 Vsix の内容が変更されていて、VSIX が再度署名されていない場合は、その署名が無効であることが VSIX インストーラーによって表示されます。 インストールは停止されませんが、ユーザーに警告が出てきます。  
  
> [!IMPORTANT]
> 2015以降では、SHA256 暗号化以外のものを使用して署名された VSIX パッケージは、無効な署名があるものとして識別されます。 VSIX のインストールはブロックされませんが、ユーザーに警告が表示されます。  
  
## <a name="signing-a-vsix-with-vsixsigntool"></a>VSIXSignTool を使用した VSIX への署名  
 Nuget.org の[VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility)では、SHA256 暗号化署名ツールを使用でき[ます。](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool)  
  
#### <a name="to-use-the-vsixsigntool"></a>VSIXSignTool を使用するには  
  
1. プロジェクトに VSIX を追加します。  
  
2. ソリューションエクスプローラーでプロジェクトノードを右クリックし、[ **&#124; 追加] [NuGet パッケージの管理**] の順に選択します。  Nuget と NuGet パッケージの追加の詳細については、「 [nuget の概要](/nuget/) 」および「 [ダイアログを使用した Nuget パッケージの管理](/nuget/consume-packages/install-use-packages-visual-studio)」を参照してください。  
  
3. VisualStudioExtensibility から VSIXSignTool を検索し、NuGet パッケージをインストールします。  
  
4. これで、プロジェクトのローカルパッケージの場所から VSIXSignTool を実行できるようになりました。 署名シナリオ (VSIXSignTool.exe/?) については、ツールのコマンドラインヘルプを参照してください。  
  
   たとえば、パスワードで保護された証明書ファイルで署名するには、次のようにします。  
  
   VSIXSignTool.exe サインイン/f \<certfile> /p \<password>\<VSIXfile>  
  
## <a name="see-also"></a>参照  
 [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)
