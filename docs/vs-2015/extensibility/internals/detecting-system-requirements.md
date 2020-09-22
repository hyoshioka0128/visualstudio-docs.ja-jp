---
title: システム要件の検出 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- setup, VSPackages
- launch conditions
ms.assetid: 0ba94acf-bf0b-4bb3-8cca-aaac1b5d6737
caps.latest.revision: 51
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 467554b8e50878bcdf1029e4792bbf168a09fa11
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841489"
---
# <a name="detecting-system-requirements"></a>システム要件の検出
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage は、Visual Studio がインストールされていない場合は機能しません。 Microsoft Windows インストーラーを使用して VSPackage のインストールを管理する場合、Visual Studio がインストールされているかどうかを検出するようにインストーラーを構成できます。 また、特定のバージョンの Windows や特定の RAM 容量など、システムに他の要件がないかどうかを確認するように構成することもできます。  
  
## <a name="detecting-visual-studio-editions"></a>Visual Studio のエディションの検出  
 Visual Studio のエディションがインストールされているかどうかを確認するには、次の表に示すように、インストールレジストリキーの値が適切なフォルダーの (REG_DWORD) 1 であることを確認します。 Visual Studio の各エディションの階層があることに注意してください。  
  
1. Enterprise  
  
2. 2 次元形式  
  
3. コミュニティ  
  
   "高" エディションがインストールされている場合、そのエディションのレジストリキーと "lower" エディションのレジストリキーが追加されます。 つまり、Enterprise edition がインストールされている場合は、Enterprise、Professional、Community の各エディションのインストールキーが1に設定されます。 そのため、必要な "最高" エディションだけを確認する必要があります。  
  
> [!NOTE]
> 64ビット版のレジストリエディターでは、32ビットのキーが HKEY_LOCAL_MACHINE] の下に表示され \\ ます。 Visual Studio のキーは HKEY_LOCAL_MACHINE \SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing に \\ あります。  
  
|製品|キー|  
|-------------|---------|  
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\enterprise|  
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\professional|  
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\community|  
|Visual Studio 2015 シェル (統合および分離)|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell|  
  
## <a name="detecting-when-visual-studio-is-running"></a>Visual Studio が実行中であることを検出する  
 VSPackage がインストールされているときに Visual Studio が実行されている場合は、VSPackage を正しく登録できません。 インストーラーは、Visual Studio が実行されていることを検出してから、プログラムのインストールを拒否する必要があります。 Windows インストーラーでは、このような検出を有効にするためにテーブルエントリを使用することはできません。 代わりに、次のように、カスタムアクションを作成する必要があります。関数を使用して `EnumProcesses` devenv.exe プロセスを検出し、起動条件で使用されるインストーラープロパティを設定するか、Visual Studio を閉じるようユーザーに求めるダイアログボックスを条件付きで表示します。  
  
## <a name="see-also"></a>参照  
 [Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
