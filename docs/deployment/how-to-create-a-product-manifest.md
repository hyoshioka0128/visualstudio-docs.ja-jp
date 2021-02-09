---
title: 製品マニフェストを作成する |Microsoft Docs
description: 1つの製品マニフェストと各ロケールのパッケージマニフェストを含むパッケージを使用して、ClickOnce アプリケーションの前提条件を配置する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- product files [ClickOnce]
- product files [Windows Installer]
- prerequisites, custom bootstrapper package
- dependencies, custom bootstrapper package
ms.assetid: 2d316aaa-8bc0-4ce5-90ab-23b3eac0b5dd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 40a620023dad754e3de4fedb9bc4fdbe7b7835a5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861232"
---
# <a name="how-to-create-a-product-manifest"></a>方法: 製品マニフェストを作成する
アプリケーションの前提条件を展開するには、ブートストラップパッケージを作成します。 ブートストラップパッケージには、1つの製品マニフェストファイルが含まれていますが、各ロケールのパッケージマニフェストが含まれています。 パッケージマニフェストには、パッケージのローカライズ固有の側面が含まれています。 これには、文字列、エンドユーザーライセンス契約、および言語パックが含まれます。

 パッケージマニフェストの詳細については、「 [方法: パッケージマニフェストを作成](../deployment/how-to-create-a-package-manifest.md)する」を参照してください。

## <a name="create-the-product-manifest"></a>製品マニフェストを作成する

#### <a name="to-create-the-product-manifest"></a>製品マニフェストを作成するには

1. ブートストラップパッケージ用のディレクトリを作成します。 この例では、C:\ packageを使用します。

2. Visual Studio で、 *product.xml* という名前の新しい XML ファイルを作成し、 *c:\ package* フォルダーに保存します。

3. 次の XML を追加して、パッケージの XML 名前空間と製品コードを記述します。 製品コードをパッケージの一意の識別子に置き換えます。

    ```xml
    <Product
    xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
    ProductCode="Custom.Bootstrapper.Package">
    ```

4. XML を追加して、パッケージに依存関係があることを指定します。 この例では、Microsoft Windows インストーラー3.1 の依存関係を使用します。

    ```xml
    <RelatedProducts>
        <DependsOnProduct Code="Microsoft.Windows.Installer.3.1" />
      </RelatedProducts>
    ```

5. ブートストラップパッケージ内のすべてのファイルを一覧表示するには、XML を追加します。 この例では、 *CorePackage.msi* パッケージのファイル名を使用します。

    ```xml
    <PackageFiles>
        <PackageFile Name="CorePackage.msi"/>
    </PackageFiles>
    ```

6. *CorePackage.msi* ファイルを *c:\ パッケージ* フォルダーにコピーまたは移動します。

7. ブートストラップコマンドを使用してパッケージをインストールするには、XML を追加します。 ブートストラップは自動的に **/qn** フラグを *.msi* ファイルに追加します。これはサイレントインストールされます。 ファイルが *.exe* の場合、ブートストラップはシェルを使用して *.exe* ファイルを実行します。 次の XML は *CorePackage.msi* する引数を示していませんが、コマンドライン引数を属性に含めることができ `Arguments` ます。

    ```xml
    <Commands>
        <Command PackageFile="CorePackage.msi" Arguments="">
    ```

8. 次の XML を追加して、このブートストラップパッケージがインストールされているかどうかを確認します。 製品コードを再頒布可能コンポーネントの GUID に置き換えます。

    ```xml
    <InstallChecks>
        <MsiProductCheck
            Property="IsMsiInstalled"
            Product="{XXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"/>
    </InstallChecks>
    ```

9. ブートストラップコンポーネントが既にインストールされているかどうかによって、ブートストラップの動作を変更するには、XML を追加します。 コンポーネントがインストールされている場合、ブートストラップパッケージは実行されません。 次の XML は、現在のユーザーが管理者であるかどうかを確認します。このコンポーネントには管理者特権が必要です。

    ```xml
    <InstallConditions>
        <BypassIf
           Property="IsMsiInstalled"
           Compare="ValueGreaterThan" Value="0"/>
        <FailIf Property="AdminUser"
            Compare="ValueNotEqualTo" Value="True"
            String="NotAnAdmin"/>
    </InstallConditions>
    ```

10. インストールが正常に完了し、再起動が必要な場合は、終了コードを設定するために XML を追加します。 次の XML は、ブートストラップがパッケージのインストールを続行しないことを示す、Fail および FailReboot の終了コードを示しています。

    ```xml
    <ExitCodes>
        <ExitCode Value="0" Result="Success"/>
        <ExitCode Value="1641" Result="SuccessReboot"/>
        <ExitCode Value="3010" Result="SuccessReboot"/>
        <DefaultExitCode Result="Fail" String="GeneralFailure"/>
    </ExitCodes>
    ```

11. 次の XML を追加して、ブートストラップコマンドのセクションを終了します。

    ```xml
        </Command>
    </Commands>
    ```

12. *C:\ パッケージ* フォルダーを Visual Studio ブートストラップディレクトリに移動します。 Visual Studio 2010 の場合、これは *SDKs\Windows\v7.0A\Bootstrapper\Packages* ディレクトリです。

## <a name="example"></a>例
 製品マニフェストには、カスタムの必須コンポーネントのインストール手順が含まれています。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Product
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
  ProductCode="Custom.Bootstrapper.Package">

  <RelatedProducts>
    <DependsOnProduct Code="Microsoft.Windows.Installer.3.1" />
  </RelatedProducts>

  <PackageFiles>
    <PackageFile Name="CorePackage.msi"/>
  </PackageFiles>

  <InstallChecks>
    <MsiProductCheck Product="IsMsiInstalled"
      Property="{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"/>
  </InstallChecks>

  <Commands>
    <Command PackageFile="CorePackage.msi" Arguments="">

      <InstallConditions>
        <BypassIf Property="IsMsiInstalled"
          Compare="ValueGreaterThan" Value="0"/>
        <FailIf Property="AdminUser"
          Compare="ValueNotEqualTo" Value="True"
         String="NotAnAdmin"/>
      </InstallConditions>

      <ExitCodes>
        <ExitCode Value="0" Result="Success"/>
        <ExitCode Value="1641" Result="SuccessReboot"/>
        <ExitCode Value="3010" Result="SuccessReboot"/>
        <DefaultExitCode Result="Fail" String="GeneralFailure"/>
      </ExitCodes>
    </Command>
  </Commands>
</Product>
```

## <a name="see-also"></a>関連項目
- [製品およびパッケージスキーマリファレンス](../deployment/product-and-package-schema-reference.md)