---
title: '&lt;Commands &gt; 要素 (ブートストラップ) |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Commands> element [bootstrapper]
ms.assetid: e61d5787-fe1f-4ebf-b0cf-0d7909be7ffb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f52c862adcdaf7a95de6a90c2c330c39edcea13
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62900345"
---
# <a name="ltcommandsgt-element-bootstrapper"></a>&lt;Commands &gt; 要素 (ブートストラップ)
要素は、要素の下にある `Commands` 要素によって記述されたテストを実装 `InstallChecks` し、テストが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 失敗した場合にブートストラップがインストールする必要があるパッケージを宣言します。

## <a name="syntax"></a>Syntax

```xml
<Commands
    Reboot
>
    <Command
        PackageFile
        Arguments
        EstimatedInstallSeconds
        EstimatedDiskBytes
        EstimatedTempBytes
        Log
    >
        <InstallConditions>
            <BypassIf
                Property
                Compare
                Value
                Schedule
            />
            <FailIf
                Property
                Compare
                Value
                String
                Schedule
            />
        </InstallConditions>
        <ExitCodes>
            <ExitCode
                Value
                Result
                String
            />
        </ExitCodes>
    </Command>
</Commands>
```

## <a name="elements-and-attributes"></a>要素と属性
 `Commands` 要素は必須です。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Reboot`|省略可能。 いずれかのパッケージが再起動終了コードを返す場合に、システムを再起動するかどうかを指定します。 有効な値を次の一覧に示します。<br /><br /> `Defer`. 再起動は、将来の時刻まで延期されます。<br /><br /> `Immediate`. いずれかのパッケージが再起動終了コードを返した場合、直ちに再起動します。<br /><br /> `None`. 再起動要求を無視します。<br /><br /> 既定値は、`Immediate` です。|

## <a name="command"></a>コマンド
 `Command` 要素は、`Commands` 要素の子要素です。 要素には `Commands` 1 つ以上の要素を含めることができ `Command` ます。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`PackageFile`|必須です。 によって指定された1つ以上の条件が false を返す場合は、インストールするパッケージの名前を指定し `InstallConditions` ます。 パッケージは、要素を使用して同じファイル内に定義されている必要があり `PackageFile` ます。|
|`Arguments`|省略可能。 パッケージファイルに渡すコマンドライン引数のセット。|
|`EstimatedInstallSeconds`|省略可能。 パッケージのインストールにかかる推定時間 (秒単位)。 この値は、ブートストラップによってユーザーに表示される進行状況バーのサイズを決定します。 既定値は0です。この場合、推定時間は指定されません。|
|`EstimatedDiskBytes`|省略可能。 インストールの完了後にパッケージが占有するディスク領域の推定サイズ (バイト単位)。 この値は、ブートストラップによってユーザーに表示されるハードディスク領域の要件で使用されます。 既定値は0です。この場合、ブートストラップはハードディスク領域の要件を表示しません。|
|`EstimatedTempBytes`|省略可能。 パッケージが必要とする一時ディスク領域の推定サイズ (バイト単位)。|
|`Log`|省略可能。 パッケージのルートディレクトリを基準とした、パッケージによって生成されるログファイルへのパスです。|

## <a name="installconditions"></a>InstallConditions
 要素は `InstallConditions` 要素の子です `Command` 。 各 `Command` 要素は、最大で1つの要素を持つことができ `InstallConditions` ます。 要素が存在しない場合 `InstallConditions` 、によって指定されたパッケージ `Condition` は常に実行されます。

## <a name="bypassif"></a>BypassIf
 `BypassIf`要素は要素の子であり、コマンドを実行し `InstallConditions` ないという肯定条件を記述します。 各 `InstallConditions` 要素には、0個以上の要素を含めることができ `BypassIf` ます。

 `BypassIf` には次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須です。 テストするプロパティの名前。 プロパティは、要素の子によって既に定義されている必要があり `InstallChecks` ます。 詳細については、[\<InstallChecks> 要素](../deployment/installchecks-element-bootstrapper.md)に関するページを参照してください。|
|`Compare`|必須です。 実行する比較の種類。 有効な値を次の一覧に示します。<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|
|`Value`|必須です。 プロパティと比較する値。|
|`Schedule`|省略可能。 `Schedule`この規則を評価するタイミングを定義するタグの名前。|

## <a name="failif"></a>FailIf
 `FailIf`要素は要素の子であり、インストールを停止するための `InstallConditions` 肯定条件を記述します。 各 `InstallConditions` 要素には、0個以上の要素を含めることができ `FailIf` ます。

 `FailIf` には次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須です。 テストするプロパティの名前。 プロパティは、要素の子によって既に定義されている必要があり `InstallChecks` ます。 詳細については、[\<InstallChecks> 要素](../deployment/installchecks-element-bootstrapper.md)に関するページを参照してください。|
|`Compare`|必須です。 実行する比較の種類。 有効な値を次の一覧に示します。<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|
|`Value`|必須です。 プロパティと比較する値。|
|`String`|省略可能。 失敗したときにユーザーに表示するテキスト。|
|`Schedule`|省略可能。 `Schedule`この規則を評価するタイミングを定義するタグの名前。|

## <a name="exitcodes"></a>ExitCodes
 要素は `ExitCodes` 要素の子です `Command` 。 `ExitCodes`要素には1つ以上の要素が含まれて `ExitCode` おり、パッケージからの終了コードに応じてインストールで実行する処理を決定します。 要素の下には、省略可能な要素を1つ指定でき `ExitCode` `Command` ます。 `ExitCodes` に属性はありません。

## <a name="exitcode"></a>ExitCode
 要素は `ExitCode` 要素の子です `ExitCodes` 。 要素は、 `ExitCode` パッケージからの終了コードに応答してインストールが実行する処理を決定します。 `ExitCode` には子要素が含まれておらず、には次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Value`|必須です。 この要素が適用される終了コード値 `ExitCode` 。|
|`Result`|必須です。 インストールがこの終了コードにどのように反応するか。 有効な値を次の一覧に示します。<br /><br /> `Success`. パッケージに正常にインストールされたことを示すフラグを付けます。<br /><br /> `SuccessReboot`. パッケージに正常にインストールされたというフラグを付け、再起動するようにシステムに指示します。<br /><br /> `Fail`. パッケージに失敗としてフラグを付けます。<br /><br /> `FailReboot`. パッケージに失敗のフラグを付け、再起動するようにシステムに指示します。|
|`String`|省略可能。 この終了コードへの応答としてユーザーに表示される値。|
|`FormatMessageFromSystem`|省略可能。 終了コードに対応するシステム指定のエラーメッセージを使用するか、に指定された値を使用するかを決定し `String` ます。 有効な値は `true` 、システムによって提供されるエラーとを使用することを意味し `false` ます。これは、によって提供される文字列を使用することを意味し `String` ます。 既定値は、`false` です。 このプロパティが `false` で、が設定されていない場合は、システムによって指定されたエラーが使用され `String` ます。|

## <a name="example"></a>例
 次のコード例では、.NET Framework 2.0 をインストールするコマンドを定義します。

```xml
<Commands Reboot="Immediate">
    <Command PackageFile="instmsia.exe"
             Arguments= ' /q /c:"msiinst /delayrebootq"'
             EstimatedInstallSeconds="20" >
        <InstallConditions>
           <BypassIf Property="VersionNT" Compare="ValueExists"/>
             BypassIf Property="VersionMsi" Compare="VersionGreaterThanOrEqualTo" Value="2.0"/>
        </InstallConditions>
        <ExitCodes>
            <ExitCode Value="0" Result="SuccessReboot"/>
            <ExitCode Value="1641" Result="SuccessReboot"/>
            <ExitCode Value="3010" Result="SuccessReboot"/>
            <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
        </ExitCodes>
    </Command>
    <Command PackageFile="WindowsInstaller-KB884016-v2-x86.exe"
             Arguments= '/quiet /norestart'
             EstimatedInstallSeconds="20" >
      <InstallConditions>
          <BypassIf Property="Version9x" Compare="ValueExists"/>
          <BypassIf Property="VersionNT" Compare="VersionLessThan" Value="5.0.3"/>
          <BypassIf Property="VersionMsi" Compare="VersionGreaterThanOrEqualTo" Value="3.0"/>
          <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired"/>
      </InstallConditions>
      <ExitCodes>
          <ExitCode Value="0" Result="Success"/>
          <ExitCode Value="1641" Result="SuccessReboot"/>
          <ExitCode Value="3010" Result="SuccessReboot"/>
          <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
      </ExitCodes>
    </Command>
    <Command PackageFile="dotnetfx.exe"
         Arguments=' /q:a /c:"install /q /l"'
         EstimatedInstalledBytes="21000000"
         EstimatedInstallSeconds="300">

        <!-- These checks determine whether the package is to be installed -->
        <InstallConditions>
            <!-- Either of these properties indicates the .NET Framework is already installed -->
            <BypassIf Property="DotNetInstalled" Compare="ValueNotEqualTo" Value="0"/>

            <!-- Block install if user does not have adminpermissions -->
            <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired"/>

            <!-- Block install on Windows 95 -->
            <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatformWin9x"/>

            <!-- Block install on Windows 2000 SP 2 or less -->
            <FailIf Property="VersionNT" Compare="VersionLessThan" Value="5.0.3" String="InvalidPlatformWinNT"/>

            <!-- Block install if Internet Explorer 5.01 or later is not present -->
            <FailIf Property="IEVersion" Compare="ValueNotExists" String="InvalidPlatformIE" />
            <FailIf Property="IEVersion" Compare="VersionLessThan" Value="5.01" String="InvalidPlatformIE" />

            <!-- Block install if the operating system does not support x86 -->
            <FailIf Property="ProcessorArchitecture" Compare="ValueNotEqualTo" Value="Intel" String="InvalidPlatformArchitecture" />
       </InstallConditions>

        <ExitCodes>
            <ExitCode Value="0" Result="Success"/>
            <ExitCode Value="3010" Result="SuccessReboot"/>
            <ExitCode Value="4097" Result="Fail" String="AdminRequired"/>
            <ExitCode Value="4098" Result="Fail" String="WindowsInstallerComponentFailure"/>
            <ExitCode Value="4099" Result="Fail" String="WindowsInstallerImproperInstall"/>
            <ExitCode Value="4101" Result="Fail" String="AnotherInstanceRunning"/>
            <ExitCode Value="4102" Result="Fail" String="OpenDatabaseFailure"/>
            <ExitCode Value="4113" Result="Fail" String="BetaNDPFailure"/>
            <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
        </ExitCodes>

    </Command>
</Commands>
```

## <a name="see-also"></a>こちらもご覧ください
- [製品およびパッケージスキーマリファレンス](../deployment/product-and-package-schema-reference.md)
- [\<InstallChecks> element](../deployment/installchecks-element-bootstrapper.md)