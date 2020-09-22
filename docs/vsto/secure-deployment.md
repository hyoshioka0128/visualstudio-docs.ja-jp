---
title: セキュリティで保護されたデプロイ
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying applications [Office development in Visual Studio], security
- Office development in Visual Studio, security
- Office applications [Office development in Visual Studio], security
- ClickOnce deployment [Office development in Visual Studio], security
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c838eddea5b3118c28fb33411a8c58a19d7b4a2d
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810955"
---
# <a name="secure-deployment"></a>セキュリティで保護されたデプロイ
  Office ソリューションを作成すると、開発用コンピューターが自動的に更新され、プロジェクト内のコードが実行できるようになります。 ただし、ソリューションを配置するときは、証明書を使用してソリューションに署名するか、信頼プロンプトキーを使用することによって、信頼の決定の基礎となる証拠を提供する必要があり [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] ます。 詳細については、「 [Office ソリューションへの信頼の付与](../vsto/granting-trust-to-office-solutions.md)」を参照してください。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 ドキュメントレベルのカスタマイズでは、ドキュメントをネットワーク上の場所に配置する場合は、Office アプリケーションのセキュリティセンターにある信頼できる場所の一覧にドキュメントの場所を追加する必要もあります。 エンドユーザーのコンピューターに対するドキュメントのアクセス許可を設定する方法の詳細については、「 [ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)」を参照してください。

## <a name="prevent-office-solutions-from-running-code"></a>Office ソリューションでコードを実行できないようにする
 管理者は、レジストリを使用して、すべての Office ソリューションがコンピューター上で実行されるのを防ぐことができます。 マネージコード拡張機能を持つ Office ソリューションが開かれると、Visual Studio Tools for Office ランタイムは、 `Disabled` コンピューター上の次のいずれかのレジストリキーの下に名前のエントリが存在するかどうかを確認します。

- **HKEY_CURRENT_USER \Software\Microsoft\VSTO**

- **HKEY_LOCAL_MACHINE \Software\Microsoft\VSTO**

  Office ソリューションでコードを実行できないようにするには、 `Disabled` これらのレジストリキーのいずれかまたは両方にエントリを作成し、に次のデータ型と値のいずれかを指定し `Disabled` ます。

- "0" (ゼロ) 以外の任意の文字列に設定されている REG_SZ または REG_EXPAND_SZ。

- 0 (ゼロ) 以外の値に設定されている REG_DWORD。

  Office ソリューションでコードを実行できるようにするには、両方の `Disabled` エントリを 0 (ゼロ) に設定するか、レジストリエントリを削除します。

## <a name="see-also"></a>こちらもご覧ください
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
- [Office ソリューションを実行またはホストするためのコンピューターの準備](/previous-versions/bb772092(v=vs.110))
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)