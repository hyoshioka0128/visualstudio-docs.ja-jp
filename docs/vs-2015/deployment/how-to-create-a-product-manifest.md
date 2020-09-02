---
title: '方法: 製品マニフェストを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 73e2c3f2c9736fd762a9e763827ed641ea5069f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153820"
---
# <a name="how-to-create-a-product-manifest"></a>方法: 製品マニフェストを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションの前提条件を展開するには、ブートストラップパッケージを作成します。 ブートストラップパッケージには、1つの製品マニフェストファイルが含まれていますが、各ロケールのパッケージマニフェストが含まれています。 パッケージマニフェストには、パッケージのローカライズ固有の側面が含まれています。 これには、文字列、エンドユーザーライセンス契約、および言語パックが含まれます。  
  
 製品マニフェストの詳細については、「 [方法: パッケージマニフェストを作成](../deployment/how-to-create-a-package-manifest.md)する」を参照してください。  
  
## <a name="creating-the-product-manifest"></a>製品マニフェストを作成する  
  
#### <a name="to-create-the-product-manifest"></a>製品マニフェストを作成するには  
  
1. ブートストラップパッケージ用のディレクトリを作成します。 この例では、C:\ packageを使用します。  
  
2. Visual Studio で、という名前の新しい XML ファイルを作成 `product.xml` し、C:\ package フォルダーに保存します。  
  
3. 次の XML を追加して、パッケージの XML 名前空間と製品コードを記述します。 製品コードをパッケージの一意の識別子に置き換えます。  
  
    ```  
    <Product  
    xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"   
    ProductCode="Custom.Bootstrapper.Package">  
    ```  
  
4. XML を追加して、パッケージに依存関係があることを指定します。 この例では、Microsoft Windows インストーラー3.1 の依存関係を使用します。  
  
    ```  
    <RelatedProducts>  
        <DependsOnProduct Code="Microsoft.Windows.Installer.3.1" />  
      </RelatedProducts>  
    ```  
  
5. ブートストラップパッケージ内のすべてのファイルを一覧表示するには、XML を追加します。 この例では、CorePackage.msi パッケージのファイル名を使用します。  
  
    ```  
    <PackageFiles>  
        <PackageFile Name="CorePackage.msi"/>  
    </PackageFiles>  
    ```  
  
6. CorePackage.msi ファイルを C:\ パッケージフォルダーにコピーまたは移動します。  
  
7. ブートストラップコマンドを使用してパッケージをインストールするには、XML を追加します。 ブートストラップは自動的に **/qn** フラグを .msi ファイルに追加します。これはサイレントインストールされます。 ファイルが .exe の場合、ブートストラップはシェルを使用して .exe ファイルを実行します。 次の XML は CorePackage.msi する引数を示していませんが、Arguments 属性にはコマンドライン引数を指定できます。  
  
    ```  
    <Commands>  
        <Command PackageFile="CorePackage.msi" Arguments="">  
    ```  
  
8. 次の XML を追加して、このブートストラップパッケージがインストールされているかどうかを確認します。 製品コードを再頒布可能コンポーネントの GUID に置き換えます。  
  
    ```  
    <InstallChecks>  
        <MsiProductCheck   
            Property="IsMsiInstalled"   
            Product="{XXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"/>  
    </InstallChecks>  
    ```  
  
9. ブートストラップコンポーネントが既にインストールされているかどうかによって、ブートストラップの動作を変更するには、XML を追加します。 コンポーネントがインストールされている場合、ブートストラップパッケージは実行されません。 次の XML は、現在のユーザーが管理者であるかどうかを確認します。このコンポーネントには管理者特権が必要です。  
  
    ```  
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
  
    ```  
    <ExitCodes>  
        <ExitCode Value="0" Result="Success"/>  
        <ExitCode Value="1641" Result="SuccessReboot"/>  
        <ExitCode Value="3010" Result="SuccessReboot"/>  
        <DefaultExitCode Result="Fail" String="GeneralFailure"/>  
    </ExitCodes>  
    ```  
  
11. 次の XML を追加して、ブートストラップコマンドのセクションを終了します。  
  
    ```  
        </Command>  
    </Commands>  
    ```  
  
12. C:\ パッケージフォルダーを Visual Studio ブートストラップディレクトリに移動します。 Visual Studio 2010 の場合、これは SDKs\Windows\v7.0A\Bootstrapper\Packages ディレクトリです。  
  
## <a name="example"></a>例  
 製品マニフェストには、カスタムの必須コンポーネントのインストール手順が含まれています。  
  
```  
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
  
## <a name="see-also"></a>参照  
 [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)
