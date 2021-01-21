---
title: '&lt;PackageFiles &gt; 要素 (ブートストラップ) |Microsoft Docs'
description: PackageFiles 要素について説明します。この要素には、コマンド要素の結果として実行されるインストールパッケージを定義する PackageFile 要素が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <PackageFiles> element [bootstrapper]
ms.assetid: 3ea252d7-18a3-47d8-af83-47feebcfe82b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 60d6491101bef33f1d8c91d4f7640be9d7277da0
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94349543"
---
# <a name="ltpackagefilesgt-element-bootstrapper"></a>&lt;PackageFiles &gt; 要素 (ブートストラップ)
要素には、要素 `PackageFiles` `PackageFile` の結果として実行されるインストールパッケージを定義する要素が含まれ `Command` ます。

## <a name="syntax"></a>構文

```xml
<PackageFiles
    CopyAllPackageFiles
>
    <PackageFile
        Name
        HomeSite
        CopyOnBuild
        PublicKey
        Hash
    />
</PackageFiles>
```

## <a name="elements-and-attributes"></a>要素と属性
 `PackageFiles` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`CopyAllPackageFiles`|任意。 に設定すると、 `false` インストーラーは要素から参照されるファイルのみをダウンロードし `Command` ます。 に設定すると `true` 、すべてのファイルがダウンロードされます。<br /><br /> に設定すると、インストーラーは、 `IfNotHomesite` がに設定されている場合と同じように動作し `False` `ComponentsLocation` `HomeSite` ます。それ以外の場合は、と同じように動作し `True` ます。 この設定は、ブートストラップ自体のパッケージが HomeSite シナリオで独自の動作を実行することを許可するのに役立ちます。<br /><br /> 既定値は、`true` です。|

## <a name="packagefile"></a>PackageFile
 要素は `PackageFile` 要素の子です `PackageFiles` 。 要素には、 `PackageFiles` 少なくとも1つの要素が必要 `PackageFile` です。

 `PackageFile` には次の属性があります。

| 属性 | 説明 |
|---------------| - |
| `Name` | 必須。 パッケージ ファイルの名前。 これは、 `Command` パッケージがインストールされる条件を定義するときに要素が参照する名前です。 この値は、テーブルのキーとしても使用され `Strings` ます。この名前は、などのツールが [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] パッケージの記述に使用するローカライズされた名前を取得するために使用されます。 |
| `HomeSite` | 任意。 リモートサーバー上のパッケージの場所 (インストーラーに含まれていない場合)。 |
| `CopyOnBuild` | 任意。 ブートストラップがビルド時にパッケージファイルをディスクにコピーするかどうかを指定します。 既定値は true です。 |
| `PublicKey` | パッケージの証明書署名者の暗号化された公開キー。 を使用する場合は必須。 `HomeSite` それ以外の場合は省略可能。 |
| `Hash` | 任意。 パッケージファイルの SHA1 ハッシュ。 これは、インストール時にファイルの整合性を確認するために使用されます。 パッケージファイルから同じハッシュを計算できない場合、パッケージはインストールされません。 |

## <a name="example"></a>例
 次のコード例では、.NET Framework 再頒布可能パッケージとその依存関係 (Windows インストーラーなど) のパッケージを定義します。

```xml
<PackageFiles>
    <PackageFile Name="instmsia.exe" HomeSite="InstMsiAExe" PublicKey="3082010A0282010100AA99BD39A81827F42B3D0B4C3F7C772EA7CBB5D18C0DC23A74D793B5E0A04B3F595ECE454F9A7929F149CC1A47EE55C2083E1220F855F2EE5FD3E0CA96BC30DEFE58C82732D08554E8F09110BBF32BBE19E5039B0B861DF3B0398CB8FD0B1D3C7326AC572BCA29A215908215E277A34052038B9DC270BA1FE934F6F335924E5583F8DA30B620DE5706B55A4206DE59CBF2DFA6BD154771192523D2CB6F9B1979DF6A5BF176057929FCC356CA8F440885558ACBC80F464B55CB8C96774A87E8A94106C7FF0DE968576372C36957B443CF323A30DC1BE9D543262A79FE95DB226724C92FD034E3E6FB514986B83CD0255FD6EC9E036187A96840C7F8E203E6CF050203010001"/>
    <PackageFile Name="WindowsInstaller-KB884016-v2-x86.exe" HomeSite="Msi30Exe" PublicKey="3082010A0282010100B22D8709B55CDF5599EB5262E7D3F4E34571A932BF94F20EE90DADFE9DC7046A584E9CA4D1D84441FB647E0F65EEC817DA4DDBD9D650B40C565B6C16884BBF03EE504883EC4F88939A51E394197FFAB397A5CE606D9FDD4C9338BDCD345971E686CEE98399A096B8EAE0445B1342B93A484E5472F70896E400C482017643AF61C2DBFAE5C5F00213DDF835B40F0D5236467443B1A2CA9CDD7E99F1351177FB1526018ECFE0B804782A15FD72C66076910CE74FB218181B6989B4F12F211B66EACA91C7460DB91758715856866523D10232AE64A06FDA5295FDFBDD8D34F5C10C35A347D7E91B6AFA0F45B4E8321D7019BDD1F9E5641FEB8737EA6FD40D838FFD0203010001"/>
    <PackageFile Name="dotnetfx.exe" HomeSite="DotNetFXExe" PublicKey="3082010A0282010100B22D8709B55CDF5599EB5262E7D3F4E34571A932BF94F20EE90DADFE9DC7046A584E9CA4D1D84441FB647E0F65EEC817DA4DDBD9D650B40C565B6C16884BBF03EE504883EC4F88939A51E394197FFAB397A5CE606D9FDD4C9338BDCD345971E686CEE98399A096B8EAE0445B1342B93A484E5472F70896E400C482017643AF61C2DBFAE5C5F00213DDF835B40F0D5236467443B1A2CA9CDD7E99F1351177FB1526018ECFE0B804782A15FD72C66076910CE74FB218181B6989B4F12F211B66EACA91C7460DB91758715856866523D10232AE64A06FDA5295FDFBDD8D34F5C10C35A347D7E91B6AFA0F45B4E8321D7019BDD1F9E5641FEB8737EA6FD40D838FFD0203010001"/>
    <PackageFile Name="dotnetchk.exe"/>
</PackageFiles>
```

## <a name="see-also"></a>関連項目
- [\<Product> element](../deployment/product-element-bootstrapper.md)
- [\<Package> element](../deployment/package-element-bootstrapper.md)
- [製品およびパッケージスキーマリファレンス](../deployment/product-and-package-schema-reference.md)