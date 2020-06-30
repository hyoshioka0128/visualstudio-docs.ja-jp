---
title: '&lt;InstallChecks &gt; 要素 (ブートストラップ) |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <InstallChecks> element [bootstrapper]
ms.assetid: ad329c87-b0ad-4304-84de-ae9496514c42
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c7ba4da072a586bdc09993b77200a769be3940ab
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536306"
---
# <a name="ltinstallchecksgt-element-bootstrapper"></a>&lt;InstallChecks &gt; 要素 (ブートストラップ)
要素は、 `InstallChecks` ローカルコンピューターに対してさまざまなテストを開始して、アプリケーションの適切なすべての前提条件がインストールされていることを確認することをサポートしています。

## <a name="syntax"></a>構文

```xml
<InstallChecks>
    <AssemblyCheck
        Property
        Name
        PublicKeyToken
        Version
        Language
        ProcessorArchitecture
    />
    <RegistryCheck
        Property
        Key
        Value
    />
    <ExternalCheck
        PackageFile
        Property
        Arguments
    />
    <FileCheck
        Property
        FileName
        SearchPath
        SpecialFolder
        SearchDepth
    />
    <MsiProductCheck
        Property
        Product
        Feature
    />
    <RegistryFileCheck
        Property
        Key
        Value
        FileName
        SearchDepth
    />
</InstallChecks>
```

## <a name="assemblycheck"></a>AssemblyCheck
 この要素は、の省略可能な子要素です `InstallChecks` 。 の各インスタンスについて `AssemblyCheck` 、ブートストラップは、要素によって識別されるアセンブリがグローバルアセンブリキャッシュ (GAC) に存在することを確認します。 要素は含まれず、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、要素の子である、要素の下にあるテストから参照でき `InstallConditions` `Command` ます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`Name`|必須。 確認するアセンブリの完全修飾名。|
|`PublicKeyToken`|必須。 この厳密な名前を持つアセンブリに関連付けられている公開キーの省略形。 GAC に格納されているすべてのアセンブリは、名前、バージョン、および公開キーを持っている必要があります。|
|`Version`|必須。 アセンブリのバージョン。<br /><br /> バージョン番号の形式は... \<*major version*> \<*minor version*> \<*build version*> \<*revision version*> です。|
|`Language`|省略可能。 ローカライズされたアセンブリの言語。 既定値は `neutral` です。|
|`ProcessorArchitecture`|省略可能。 このインストールの対象となるコンピュータープロセッサ。 既定値は `msil` です。|

## <a name="externalcheck"></a>ExternalCheck
 この要素は、の省略可能な子要素です `InstallChecks` 。 ブートストラップは、の各インスタンスについて、 `ExternalCheck` 指定された外部プログラムを別のプロセスで実行し、によって示されるプロパティにその終了コードを格納し `Property` ます。 `ExternalCheck`は、複雑な依存関係のチェックを実装する場合や、コンポーネントの存在を確認する唯一の方法が、インスタンスをインスタンス化する場合に便利です。

 `ExternalCheck`には要素が含まれておらず、には次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、要素の子である、要素の下にあるテストから参照でき `InstallConditions` `Command` ます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`PackageFile`|必須。 実行する外部プログラムです。 プログラムは、セットアップ配布パッケージの一部である必要があります。|
|`Arguments`|省略可能。 は、によって指定された実行可能ファイルにコマンドライン引数を渡し `PackageFile` ます。|

## <a name="filecheck"></a>FileCheck
 この要素は、の省略可能な子要素です `InstallChecks` 。 ブートストラップは、の各インスタンスについて、 `FileCheck` 指定されたファイルが存在するかどうかを判断し、そのファイルのバージョン番号を返します。 ファイルにバージョン番号がない場合、ブートストラップはによって指定されたプロパティを `Property` 0 に設定します。 ファイルが存在しない場合、 `Property` は何の値にも設定されません。

 `FileCheck`には要素が含まれておらず、には次の属性があります。

| 属性 | 説明 |
|-----------------| - |
| `Property` | 必須。 結果を格納するプロパティの名前。 このプロパティは、要素の子である、要素の下にあるテストから参照でき `InstallConditions` `Command` ます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。 |
| `FileName` | 必須。 検索するファイルの名前。 |
| `SearchPath` | 必須。 ファイルを検索するディスクまたはフォルダー。 が割り当てられている場合、これは相対パスである必要があります。 `SpecialFolder` それ以外の場合は、絶対パスである必要があります。 |
| `SpecialFolder` | 省略可能。 Windows またはのいずれかに特別な意味を持つフォルダー [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 既定では、 `SearchPath` 絶対パスとして解釈されます。 有効な値は次のとおりです。<br /><br /> `AppDataFolder`. このアプリケーションのアプリケーションデータフォルダー [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。現在のユーザーに固有です。<br /><br /> `CommonAppDataFolder`. すべてのユーザーが使用するアプリケーションデータフォルダー。<br /><br /> `CommonFilesFolder`. 現在のユーザーの共通ファイルフォルダー。<br /><br /> `LocalDataAppFolder`. 非ローミングアプリケーションのデータフォルダー。<br /><br /> `ProgramFilesFolder`. 32ビットアプリケーションの標準の Program Files フォルダー。<br /><br /> `StartUpFolder`. システムの起動時に起動されるすべてのアプリケーションを含むフォルダー。<br /><br /> `SystemFolder`. 32ビットシステム Dll を格納しているフォルダー。<br /><br /> `WindowsFolder`. Windows システムのインストールが含まれているフォルダー。<br /><br /> `WindowsVolume`. Windows システムのインストールが含まれているドライブまたはパーティション。 |
| `SearchDepth` | 省略可能。 名前付きファイルのサブフォルダーを検索する深さ。 検索は深さ優先です。 既定値は0です。これにより、と SearchPath によって指定された最上位フォルダーに検索が制限され `SpecialFolder` ます。 **SearchPath** |

## <a name="msiproductcheck"></a>MsiProductCheck
 この要素は、の省略可能な子要素です `InstallChecks` 。 ブートストラップは、の各インスタンスについて、 `MsiProductCheck` 指定した Microsoft Windows インストーラーのインストールが完了するまで実行されているかどうかを確認します。 プロパティ値は、インストールされている製品の状態に応じて設定されます。 正の値は、製品がインストールされていることを示します。0または-1 は、インストールされていないことを示します。 (詳細については、Windows インストーラー SDK 関数 MsiQueryFeatureState を参照してください)。. コンピューターに Windows インストーラーがインストールされていない場合、 `Property` は設定されません。

 `MsiProductCheck`には要素が含まれておらず、には次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、要素の子である、要素の下にあるテストから参照でき `InstallConditions` `Command` ます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`Product`|必須。 インストールされている製品の GUID。|
|`Feature`|省略可能。 インストールされているアプリケーションの特定の機能の GUID。|

## <a name="registrycheck"></a>RegistryCheck
 この要素は、の省略可能な子要素です `InstallChecks` 。 ブートストラップは、の各インスタンスについ `RegistryCheck` て、指定されたレジストリキーが存在するかどうか、または指定された値があるかどうかを確認します。

 `RegistryCheck`には要素が含まれておらず、には次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、要素の子である、要素の下にあるテストから参照でき `InstallConditions` `Command` ます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`Key`|必須。 レジストリ キーの名前。|
|`Value`|省略可能。 取得するレジストリ値の名前です。 既定では、既定値のテキストが返されます。 `Value`文字列または DWORD のいずれかである必要があります。|

## <a name="registryfilecheck"></a>RegistryFileCheck
 この要素は、の省略可能な子要素です `InstallChecks` 。 ブートストラップは、の各インスタンスについて、指定された `RegistryFileCheck` ファイルのバージョンを取得します。最初に、指定したレジストリキーからファイルへのパスを取得しようとします。 これは、レジストリで値として指定されたディレクトリ内のファイルを検索する場合に特に便利です。

 `RegistryFileCheck`には要素が含まれておらず、には次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、要素の子である、要素の下にあるテストから参照でき `InstallConditions` `Command` ます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`Key`|必須。 レジストリ キーの名前。 属性が設定されていない場合、その値はファイルへのパスとして解釈され `File` ます。 このキーが存在しない場合、 `Property` は設定されません。|
|`Value`|省略可能。 取得するレジストリ値の名前です。 既定では、既定値のテキストが返されます。 `Value`は文字列である必要があります。|
|`FileName`|省略可能。 ファイルの名前。 指定した場合、レジストリキーから取得した値はディレクトリパスと見なされ、この名前が追加されます。 指定しない場合、レジストリから返される値は、ファイルへの完全パスであると見なされます。|
|`SearchDepth`|省略可能。 名前付きファイルのサブフォルダーを検索する深さ。 検索は深さ優先です。 既定値は0で、レジストリキーの値によって指定された最上位フォルダーまで検索を制限します。|

## <a name="remarks"></a>Remarks
 の下にある要素は、 `InstallChecks` 実行するテストを定義しますが、実行されません。 テストを実行するには、要素の下に要素を作成する必要があり `Command` `Commands` ます。

## <a name="example"></a>例
 次のコード例では、 `InstallChecks` .NET Framework の製品ファイルで使用されている要素を示します。

```xml
<InstallChecks>
    <ExternalCheck Property="DotNetInstalled" PackageFile="dotnetchk.exe" />
    <RegistryCheck Property="IEVersion" Key="HKLM\Software\Microsoft\Internet Explorer" Value="Version" />
</InstallChecks>
```

## <a name="installconditions"></a>InstallConditions
 を `InstallChecks` 評価すると、プロパティが生成されます。 次に、プロパティを使用して、 `InstallConditions` パッケージのインストール、バイパス、または失敗のいずれを行うかを決定します。 次の表に、の一覧を示し `InstallConditions` ます。

|条件|説明|
|-|-|
|`FailIf`|いずれかの `FailIf` 条件が true と評価された場合、パッケージは失敗します。 残りの条件は評価されません。|
|`BypassIf`|いずれかの条件が true と評価されると、 `BypassIf` パッケージはバイパスされます。 残りの条件は評価されません。|

## <a name="predefined-properties"></a>定義済みのプロパティ
 要素と要素の一覧を次の表に示し `BypassIf` `FailIf` ます。

|プロパティ|Notes|指定できる値|
|--------------|-----------|---------------------|
|`Version9X`|Windows 9X オペレーティングシステムのバージョン番号。|4.10 = Windows 98|
|`VersionNT`|Windows NT ベースのオペレーティングシステムのバージョン番号。|Major. Minor. ServicePack<br /><br /> 5.0 = Windows 2000<br /><br /> 5.1.0 = Windows XP<br /><br /> 5.1.2 = Windows XP Professional SP2<br /><br /> 5.2.0 = Windows Server 2003|
|`VersionNT64`|64ビット Windows NT ベースのオペレーティングシステムのバージョン番号。|前に説明したのと同じです。|
|`VersionMsi`|Windows インストーラーサービスのバージョン番号。|2.0 = Windows インストーラー2.0|
|`AdminUser`|ユーザーが Windows NT ベースのオペレーティングシステムに対する管理者特権を持っているかどうかを指定します。|0 = 管理者特権はありません。<br /><br /> 1 = 管理者特権|

 たとえば、Windows 95 を実行しているコンピューターでのインストールをブロックするには、次のようなコードを使用します。

```xml
<!-- Block install on Windows 95 -->
    <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatform"/>
```

## <a name="see-also"></a>関連項目
- [\<Commands>element](../deployment/commands-element-bootstrapper.md)
- [製品およびパッケージスキーマリファレンス](../deployment/product-and-package-schema-reference.md)