---
title: '&lt;Strings &gt; 要素 (ブートストラップ) |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- MSBuild.GenerateBootstrapper.NoStringsForCulture
- MSBuild.GenerateBootstrapper.ProductCultureNotFound
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Strings> element [bootstrapper]
ms.assetid: d5ea3613-5fc9-4a11-bef3-46a01178bf60
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a8bc56bf980bba6326b3615b6892ec555b795ec8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "66747407"
---
# <a name="ltstringsgt-element-bootstrapper"></a>&lt;Strings &gt; 要素 (ブートストラップ)
製品名、パッケージ名、およびインストールエラーメッセージのローカライズされた文字列を定義します。

## <a name="syntax"></a>構文

```xml
<Strings>
    <String
        Name
    >
    </String>
</Strings>
```

## <a name="elements-and-attributes"></a>要素と属性
 要素は `Strings` 要素の子です `Package` 。 属性はありません。

## <a name="string"></a>String
 要素は `String` 要素の子です `Strings` 。 `Strings`要素には、1つまたは複数の要素を含めることができ `String` ます。

 `String` には次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Name`|必須。 文字列の名前。|

## <a name="example"></a>例
 次のコード例では、.NET Framework インストーラーのすべての英語文字列を指定しています。

```xml
<Strings>
    <String Name="DisplayName">.NET Framework 2.0</String>
    <String Name="Culture">en</String>
    <String Name="AdminRequired">Administrator permissions are required to install the .NET Framework 2.0. Contact your administrator.</String>
    <String Name="InvalidPlatformWin9x">Installation of the .NET Framework 2.0 is not supported on Windows 95. Contact your application vendor.</String>
    <String Name="InvalidPlatformWinNT">Installation of the .NET Framework 2.0 is not supported on Windows NT 4.0. Contact your application vendor.</String>
    <String Name="InvalidPlatformIE">Installation of the .NET Framework 2.0 requires Internet Explorer 5.01 or greater. Contact your application vendor.</String>
    <String Name="InvalidPlatformArchitecture">This version of the .NET Framework 2.0 is not supported on a 64-bit operating system. Contact your application vendor.</String>
    <String Name="WindowsInstallerImproperInstall">Due to an error with Windows Installer, the installation of the .NET Framework 2.0 cannot proceed.</String>
    <String Name="AnotherInstanceRunning">Another instance of setup is already running. The running instance must complete before this setup can proceed.</String>
    <String Name="BetaNDPFailure">A beta version of the .NET Framework was detected on the computer. Uninstall any previous beta versions of .NET Framework before continuing.</String>
    <String Name="GeneralFailure">A failure occurred attempting to install the .NET Framework 2.0.</String>
    <String Name="DotNetFXExe">http://go.microsoft.com/fwlink/?LinkId=37283</String>
    <String Name="InstMsiAExe">http://go.microsoft.com/fwlink/?LinkId=37285</String>
    <String Name="Msi30Exe">http://go.microsoft.com/fwlink/?LinkId=37287</String>
</Strings>
```

## <a name="see-also"></a>関連項目
- [\<Package> element](../deployment/package-element-bootstrapper.md)