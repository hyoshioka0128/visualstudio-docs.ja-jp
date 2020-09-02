---
title: VSPackage Registration |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: ecd20da8-b04b-4141-a8f4-a2ef91dd597a
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a11f05edb4e7d476fdbcab82d365f9327dd4869a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685282"
---
# <a name="vspackage-registration"></a>VSPackage の登録
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Vspackage [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、インストールされていることを通知し、読み込む必要があります。 このプロセスは、レジストリに情報を書き込むことによって行われます。 これは、一般的なインストーラーのジョブです。  
  
> [!NOTE]
> VSPackage の開発中に自己登録を使用するために受け入れられるプラクティスです。 ただし、 [!INCLUDE[vsipprvsip](../../includes/vsipprvsip-md.md)] パートナーは、セットアップの一環として自己登録を使用して製品を出荷することはできません。  
  
 Windows インストーラーパッケージ内のレジストリエントリは、通常、レジストリテーブルで作成されます。 レジストリテーブルにファイル拡張子を登録することもできます。 ただし、Windows インストーラーでは、プログラム識別子 (ProgId)、クラス、拡張機能、動詞テーブルを使用した組み込みのサポートが提供されます。 詳細については、「 [データベーステーブル](https://msdn.microsoft.com/library/aa368259\(VS.85\).aspx)」を参照してください。  
  
 レジストリエントリが、選択したサイドバイサイド戦略に適したコンポーネントに関連付けられていることを確認してください。 たとえば、共有ファイルのレジストリエントリは、そのファイルの Windows インストーラーコンポーネントに関連付けられている必要があります。 同様に、バージョン固有のファイルのレジストリエントリは、そのファイルのコンポーネントに関連付けられている必要があります。 そうしないと、1つのバージョンの VSPackage をインストールまたはアンインストールすると、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 他のバージョンの VSPackage が壊れる可能性があります。 詳細については、「 [Visual Studio の複数のバージョンのサポート](../../extensibility/supporting-multiple-versions-of-visual-studio.md)」を参照してください。  
  
> [!NOTE]
> 登録を管理する最も簡単な方法は、開発者の登録とインストール時の登録の両方に同じファイル内の同じデータを使用することです。 たとえば、一部のインストーラー開発ツールでは、ビルド時に .reg 形式のファイルを使用できます。 開発者が独自の日常的な開発とデバッグを行うために .reg ファイルを保持している場合は、それらの同じファイルをインストーラーに自動的に含めることができます。 登録データを自動的に共有できない場合は、インストーラーの登録データのコピーが最新であることを確認する必要があります。  
  
## <a name="registering-unmanaged-vspackages"></a>アンマネージド Vspackage の登録  
 アンマネージ Vspackage (Visual Studio パッケージテンプレートによって生成されたものを含む) は、ATL スタイルの .rgs ファイルを使用して登録情報を格納します。 .Rgs ファイル形式は ATL に固有であり、通常、インストール作成ツールでそのように使用することはできません。 VSPackage インストーラーの登録情報は、個別に管理する必要があります。 たとえば、開発者は、ファイルの拡張子が .rgs であるファイルを .reg 形式で保存することができます。 .Reg ファイルは、開発作業またはインストーラーによる使用のために、RegEdit にマージできます。  
  
## <a name="registering-managed-vspackages"></a>Managed Vspackage の登録  
 RegPkg ツールは、マネージ VSPackage から登録属性を読み取り、レジストリに情報を直接書き込むか、インストーラーで使用できる .reg 形式のファイルを作成します。  
  
> [!NOTE]
> RegPkg ツールは再頒布可能ではなく、ユーザーのシステムに VSPackage を登録するために使用することはできません。  
  
## <a name="why-vspackages-should-not-self-register-at-install-time"></a>インストール時に Vspackage が自己登録できない理由  
 VSPackage インストーラーは自己登録に依存しないようにする必要があります。 一見すると、VSPackage のレジストリ値を VSPackage 自体に残しておくのは良いアイデアだと思います。 開発者が日常的な作業とテストに使用できるレジストリ値を必要とする場合は、インストーラーでレジストリデータのコピーを個別に保持しないようにすることをお勧めします。 インストーラーは、VSPackage 自体を使用してレジストリ値を書き込むことができます。  
  
 理論的には、自己登録には VSPackage のインストールに適していない欠陥がいくつかあります。  
  
- インストール、アンインストール、インストールのロールバック、およびアンインストールのロールバックを正しくサポートするには、RegPkg を呼び出して自己登録するすべてのマネージ VSPackage に対して4つのカスタムアクションを作成する必要があります。  
  
- サイドバイサイドのサポートを行うには、サポートされているすべてのバージョンのに対して RegSvr32 または RegPkg を呼び出す4つのカスタムアクションを作成する必要があり [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
- 自己登録されたモジュールを使用したインストールは、他の機能やアプリケーションで自己登録キーが使用されているかどうかを示す方法がないため、安全にロールバックすることはできません。  
  
- 自己登録 Dll は、存在しない、またはバージョンが間違っている補助 Dll にリンクすることがあります。 これに対し、Windows インストーラーは、システムの現在の状態に依存せずにレジストリテーブルを使用して Dll を登録できます。  
  
- コンポーネントがソースとして指定されており、SelfReg テーブルに一覧表示されている場合、自己登録コードはタイプライブラリなどのネットワークリソースへのアクセスを拒否できます。 このため、管理インストール中にコンポーネントのインストールが失敗する可能性があります。  
  
## <a name="see-also"></a>参照  
 [Windows インストーラー](https://msdn.microsoft.com/library/cc185688\(VS.85\).aspx)   
 [マネージドパッケージの登録](https://msdn.microsoft.com/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)
