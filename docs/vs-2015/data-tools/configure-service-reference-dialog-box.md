---
title: '[サービス参照の構成] ダイアログボックス |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: reference
f1_keywords:
- msvse_wcf.dlg.ConfigureServiceReference
helpviewer_keywords:
- WCF services, Configure Service Reference dialog box
- service references [Visual Studio], configuring behavior
- Configure Service Reference dialog box
ms.assetid: 25e4c36b-2db6-4e71-9010-b7068255d09d
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ac8f4cf619bbdd007bb7aa570f549ae3c0b50e86
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651113"
---
# <a name="configure-service-reference-dialog-box"></a>[サービス参照の構成] ダイアログ ボックス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[ **サービス参照の構成** ] ダイアログボックスを使用して、サービスの動作を構成でき [!INCLUDE[vsindigo](../includes/vsindigo-md.md)] ます。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、[ツール] メニューの [設定のインポートとエクスポート] をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

 **[サービス参照の構成]** ダイアログ ボックスにアクセスするには、**ソリューション エクスプローラー**でサービス参照を右クリックし、**[サービス参照の構成]** を選択します。 **[サービス参照の追加] ダイアログ ボックス**で **[詳細]** ボタンをクリックしてダイアログ ボックスにアクセスすることもできます。

## <a name="task-list"></a>タスク一覧

- WCF サービスがホストされるアドレスを変更するには、**[アドレス]** フィールドに新しいアドレスを入力します。

- WCF クライアント内のクラスのアクセス レベルを変更するには、**[生成されたクラスのアクセス レベル]** リストでアクセス レベル キーワードを選択します。

- WCF サービスのメソッドを非同期に呼び出すには、**[非同期操作を生成する]** チェック ボックスをオンにします。

- WCF クライアントでメッセージ コントラクト型を生成するには、**[メッセージ コントラクトを常に生成]** チェック ボックスをオンにします。

- WCF クライアントのリストまたはディクショナリ コレクションの型を指定するには、**[コレクション型]** リストおよび **[ディクショナリ コレクション型]** リストから型を選択します。

- 型の共有を無効にするには、**[参照されたアセンブリで型を再利用]** チェック ボックスをオフにします。 参照されたアセンブリのサブセットで型の共有を有効にするには、**[参照されたアセンブリで型を再利用]** チェック ボックスをオンにし、**[参照されたアセンブリを指定して型を再利用]** チェック ボックスをオンにして、**[Referenced assemblies list]\(参照されたアセンブリの一覧\)** で必要な参照を選択します。

## <a name="uielement-list"></a>UIElement の一覧
 **アドレス** サービス参照がサービスを検索する Web アドレスを更新するために使用します。 たとえば、開発中のサービスは開発サーバーでホストされ、その後、運用サーバーに移されることがあり、アドレスの変更が必要になります。

> [!NOTE]
> Address 要素は、**[サービス参照の構成]** ダイアログ ボックスが **[サービス参照の追加] ダイアログ ボックス**から表示された場合は使用できません。

 **生成されたクラスのアクセスレベル** WCF クライアントクラスのコードアクセスレベルを決定します。

> [!NOTE]
> Web サイト プロジェクトの場合、このオプションは常に `Public` に設定され、変更できません。 詳細については、「 [サービス参照のトラブルシューティング](../data-tools/troubleshooting-service-references.md)」を参照してください。

 **非同期操作の生成** WCF サービスメソッドを同期的に呼び出すか (既定値)、非同期的に呼び出すかを指定します。

 **タスクベースの操作を生成** する非同期コードを記述する場合、このオプションを使用すると、.Net 4 で導入されたタスク並列ライブラリ (TPL) を利用できます。 「 [タスク並列ライブラリ (TPL)](https://msdn.microsoft.com/library/dd460717.aspx)」を参照してください。

 **メッセージコントラクトを常に生成** するWCF クライアントに対してメッセージコントラクト型を生成するかどうかを決定します。 メッセージコントラクトの詳細については、「 [Using Message contracts](https://msdn.microsoft.com/library/1e19c64a-ae84-4c2f-9155-91c54a77c249)」を参照してください。

 **コレクション型** WCF クライアントのリストコレクション型を指定します。 既定の型は <xref:System.Array> です。

 **Dictionary コレクション型** WCF クライアントのディクショナリコレクション型を指定します。 既定の型は <xref:System.Collections.Generic.Dictionary%602> です。

 参照された**アセンブリで型を再利用**するサービスが追加または更新されたときに新しい型を生成するのではなく、参照されているアセンブリに既に存在する再利用を WCF クライアントが試行するかどうかを決定します。 既定では、このチェック ボックスはオンになっています。

 参照されて**いるすべてのアセンブリで型を再利用**する選択すると、[参照された**アセンブリ] の一覧**のすべての型が、可能な場合は再利用されます。 既定では、このオプションが選択されています。

 **指定された参照アセンブリでの型の再利用** 選択した場合、[参照された **アセンブリ] の一覧** で選択した型のみが再利用されます。

 **参照** されたアセンブリの一覧プロジェクトまたは Web サイトの参照アセンブリの一覧が含まれています。 **[指定された参照アセンブリで型を再利用**する] を選択すると、個々のアセンブリを選択またはクリアできます。

 **Web 参照の追加** [ [NIB: Web 参照の追加] ダイアログボックス](https://msdn.microsoft.com/bdf05776-c591-40af-bfd7-e1e2aa1e87b5)を表示します。

> [!NOTE]
> このオプションは、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] のバージョン 2.0 を対象にするプロジェクトでのみ使用する必要があります。

> [!NOTE]
> [ **Web 参照の追加**] ボタンは、[**サービス参照の追加] ダイアログボックス**の [**サービス参照の構成**] ダイアログボックスが表示された場合にのみ使用できます。

## <a name="see-also"></a>参照
 [方法: サービス参照を追加、更新、または削除](https://msdn.microsoft.com/library/cacc14bd-4455-4a44-be78-d2ac16113dd9)する [方法: Web サービスへの参照を追加](https://msdn.microsoft.com/library/952e49a1-567e-4a74-8cd7-f2e7b62c3168)する [Windows Communication Foundation サービスと WCF Data Services](../data-tools/configure-service-reference-dialog-box.md)
