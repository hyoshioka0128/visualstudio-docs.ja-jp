---
title: '方法: ClickOnce アプリケーションを使用して必須コンポーネントを含める |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c66bf0a5-8c93-4e68-a224-3b29ac36fe4d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 94ed90b9fcdd0c4ffe35789d00de4bbbd4aaa355
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557632"
---
# <a name="how-to-include-prerequisites-with-a-clickonce-application"></a>方法: ClickOnce アプリケーションと共に必須コンポーネントを含める
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションと共に必須コンポーネントを配布する前に、まず開発用コンピューターにそれらの必須コンポーネントのインストーラー パッケージをダウンロードする必要があります。 インストーラー パッケージが **[パッケージ]** フォルダーにない場合、アプリケーションを発行して **[アプリケーションと同じ場所から必須コンポーネントをダウンロードする]** を選択するとエラーが発生します。

> [!NOTE]
> .NET Framework のインストーラーパッケージを追加するには、「[開発者向けの .NET Framework 配置ガイド](/dotnet/framework/deployment/deployment-guide-for-developers)」を参照してください。

## <a name="Package"></a> Package.xml を使用してインストーラー パッケージを追加するには

1. ファイル エクスプローラーで、**Packages** フォルダーを開きます。

    既定では、パスは `%ProgramFiles(x86)%\Microsoft SDKs\ClickOnce Bootstrapper\Packages\`です。

2. 追加する必須コンポーネントのフォルダーを開いてから、インストールされているバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の言語フォルダー (たとえば、英語の場合は **en**) を開きます。

3. メモ帳で、*Package.xml* ファイルを開きます。

4. `http://go.microsoft.com/fwlink`が含まれている**Name**要素を見つけ、URL をコピーします。 **LinkID** 部分を含めます。

   > [!NOTE]
   > **Name**要素に `http://go.microsoft.com/fwlink`が含まれていない場合は、前提条件のルートフォルダーにある**fwlink** **ファイルを**開き、その文字列を見つけます。

   > [!IMPORTANT]
   > 一部の必須コンポーネントには、複数のインストーラー パッケージ (たとえば、32 ビット システム用または 64 ビット システム用) があります。 複数の **Name** 要素に **fwlink** が含まれている場合、各要素で残りの手順を繰り返す必要があります。

5. ブラウザーのアドレス バーに URL を貼り付け、実行または保存を確認するメッセージが表示されたら、**[上書き保存]** をクリックします。

    この手順では、コンピューターにインストーラー ファイルをダウンロードします。

6. 必須コンポーネントのルート フォルダーにファイルをコピーします。

    たとえば、Windows Installer 4.5 の前提条件の場合は、*\Packages\WindowsInstaller 4_5* フォルダーにファイルをコピーします。

    これで、アプリケーションと共にインストーラー パッケージを配布できます。

## <a name="see-also"></a>参照
- [方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールする](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
