---
title: VSパッケージ登録 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: ecd20da8-b04b-4141-a8f4-a2ef91dd597a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a05dec8fbef40143f31f2c0ac484824717ea2e32
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703928"
---
# <a name="vspackage-registration"></a>VSPackage の登録
VSPackages は[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、インストールされていること、および読み込む必要があることを通知する必要があります。 この処理は、レジストリに情報を書き込む方法で行います。 これは、インストーラの一般的な作業です。

> [!NOTE]
> これは、自己登録を使用する VSPackage の開発中に受け入れられたプラクティスです。 ただし、[!INCLUDE[vsipprvsip](../../extensibility/includes/vsipprvsip_md.md)]パートナーは、セットアップの一部として自己登録を使用して製品を出荷することはできません。

 Windows インストーラ パッケージのレジストリ エントリは、通常、レジストリ テーブルに作成されます。 ファイル拡張子は、レジストリテーブルに登録することもできます。 ただし、Windows インストーラーは、プログラム識別子 (ProgId)、クラス、拡張機能、および動詞のテーブルを介して組み込みのサポートを提供します。 詳細については、「[データベース テーブル](/windows/desktop/Msi/database-tables)」を参照してください。

 選択したサイド バイ サイド戦略に適したコンポーネントにレジストリ エントリが関連付けられていることを確認します。 たとえば、共有ファイルのレジストリ エントリは、そのファイルの Windows インストーラ コンポーネントに関連付ける必要があります。 同様に、バージョン固有のファイルのレジストリ エントリも、そのファイルのコンポーネントに関連付ける必要があります。 それ以外の場合は、VSPackage をインストールまたはアンインストール[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]して、1 つのバージョンの VSPackage を他のバージョンで壊す可能性があります。 詳細については、「 [Visual Studio の複数バージョンのサポート](../../extensibility/supporting-multiple-versions-of-visual-studio.md)」を参照してください。

> [!NOTE]
> 登録を管理する最も簡単な方法は、開発者登録とインストール時の登録の両方に同じファイル内の同じデータを使用することです。 たとえば、インストーラ開発ツールの中には、ビルド時に .reg-format でファイルを使用するものもあります。 開発者が日々の開発とデバッグのために .reg ファイルを管理している場合、同じファイルをインストーラーに自動的に含めることができます。 登録データを自動的に共有できない場合は、登録データのインストーラのコピーが最新であることを確認する必要があります。

## <a name="registering-unmanaged-vspackages"></a>アンマネージ VS パッケージの登録
 アンマネージ VS パッケージ (Visual Studio パッケージ テンプレートによって生成されたものも含む) は、ATL 形式の .rgs ファイルを使用して登録情報を格納します。 .rgs ファイル形式は ATL 固有であり、通常はインストール オーサリング ツールでは使用できません。 VSPackage インストーラーの登録情報は、個別に保守する必要があります。 たとえば、開発者は .reg 形式のファイルを .rgs ファイルの変更と同期させることができます。 reg ファイルは、開発作業のために RegEdit とマージするか、インストーラーによって使用することができます。

## <a name="registering-managed-vspackages"></a>管理 VS パッケージの登録
 RegPkg ツールは、マネージ VSPackage から登録属性を読み取り、レジストリに直接情報を書き込むか、インストーラーで使用できる .reg 形式のファイルを書き込むことができます。

> [!NOTE]
> RegPkg ツールは再頒布可能ではなく、ユーザーのシステムに VSPackage を登録するために使用できません。

## <a name="why-vspackages-should-not-self-register-at-install-time"></a>VS パッケージがインストール時に自己登録しない理由
 VSPackage インストーラーは、自己登録に依存しないでください。 一見すると、VSPackage 自体の中に VSPackage のレジストリ値を保持することは良い考えのように思えます。 開発者が日常的な作業とテストに使用できるレジストリ値を必要としている場合、インストーラーでレジストリ データのコピーを個別に保持することは避けるのが理にかなっています。 インストーラーは、VSPackage 自体に依存してレジストリ値を書き込むことができます。

 理論的には良いですが、自己登録にはVSPackageのインストールに適さないいくつかの欠陥があります。

- インストール、アンインストール、インストールのロールバック、およびアンインストールのロールバックを正しくサポートするには、RegPkg を呼び出すことによって自己登録するマネージ VSPackage ごとに 4 つのカスタム アクションを作成する必要があります。

- サイド バイ サイド サポートへのアプローチでは、サポートされているすべてのバージョンの RegSvr32 または RegPkg を呼び出す[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]4 つのカスタム アクションを作成する必要があります。

- 自己登録されたキーが別の機能またはアプリケーションによって使用されているかどうかを知る方法がないため、自己登録モジュールを使用したインストールは安全にロールバックできません。

- 自己登録 DLL は、存在しない補助 DLL やバージョンが間違っている場合があります。 これに対し、Windows インストーラは、システムの現在の状態に依存しないレジストリ テーブルを使用して DLL を登録できます。

- コンポーネントが両方ともソースから実行するように指定され、SelfReg テーブルに一覧表示されている場合、タイプ ライブラリなどのネットワーク リソースへの自己登録コードへのアクセスを拒否できます。 これにより、管理者インストール中にコンポーネントのインストールが失敗する可能性があります。

## <a name="see-also"></a>関連項目
- [インストーラ](/windows/desktop/Msi/windows-installer-portal)
- [管理パッケージの登録](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)
