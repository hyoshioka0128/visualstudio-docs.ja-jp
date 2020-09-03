---
title: '方法: ClickOnce アプリケーションを使用して必須コンポーネントを含める |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
ms.assetid: c66bf0a5-8c93-4e68-a224-3b29ac36fe4d
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9639da1f735095f6d04a59d1f2302f822423e006
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77557681"
---
# <a name="how-to-include-prerequisites-with-a-clickonce-application"></a>方法 : ClickOnce アプリケーションと共に必須コンポーネントを含める
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションと共に必須コンポーネントを配布する前に、まず開発用コンピューターにそれらの必須コンポーネントのインストーラー パッケージをダウンロードする必要があります。 アプリケーションを発行し、[ **アプリケーションと同じ場所から必須コンポーネントをダウンロード**する] を選択すると、インストーラーパッケージが **packages** フォルダーにない場合にエラーが発生します。  
  
> [!NOTE]
> .NET Framework のインストーラーパッケージを追加するには、「 [開発者向けの .NET Framework 配置ガイド](/dotnet/framework/deployment/deployment-guide-for-developers)」を参照してください。  
  
## <a name="to-add-an-installer-package-by-using-packagexml"></a><a name="Package"></a> Package.xml を使用してインストーラー パッケージを追加するには  
  
1. ファイル エクスプローラーで、**Packages** フォルダーを開きます。  
  
     既定では、パスは 32 ビット システムでは C:\Program Files\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages、64 ビット システムでは C:\Program Files (x86)\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages です。  
  
2. 追加する必須コンポーネントのフォルダーを開いてから、インストールされているバージョンの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の言語フォルダー (たとえば、英語の場合は **en**) を開きます。  
  
3. メモ帳で、**Package.xml** ファイルを開きます。  
  
4. を含む **Name** 要素を見つけ `http://go.microsoft.com/fwlink` 、URL をコピーします。 **LinkID** 部分を含めます。  
  
    > [!NOTE]
    > **Name**要素が含まれていない場合は、 `http://go.microsoft.com/fwlink` 前提条件のルートフォルダーにある**Product.xml**ファイルを開き、 **fwlink**文字列を見つけます。  
  
    > [!IMPORTANT]
    > 一部の必須コンポーネントには、複数のインストーラー パッケージ (たとえば、32 ビット システム用または 64 ビット システム用) があります。 複数の **Name** 要素に **fwlink** が含まれている場合、各要素で残りの手順を繰り返す必要があります。  
  
5. ブラウザーのアドレス バーに URL を貼り付け、実行または保存を確認するメッセージが表示されたら、**[上書き保存]** をクリックします。  
  
     この手順では、コンピューターにインストーラー ファイルをダウンロードします。  
  
6. 必須コンポーネントのルート フォルダーにファイルをコピーします。  
  
     たとえば、Windows Installer 4.5 の前提条件の場合は、\Packages\WindowsInstaller 4_5 フォルダーにファイルをコピーします。  
  
     これで、アプリケーションと共にインストーラー パッケージを配布できます。  
  
## <a name="see-also"></a>参照  
 [方法: ClickOnce アプリケーションを使用して必須コンポーネントをインストールする](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
