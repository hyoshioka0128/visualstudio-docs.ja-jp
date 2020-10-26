---
title: '[サービス参照の構成] ダイアログ ボックス'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- msvse_wcf.dlg.ConfigureServiceReference
helpviewer_keywords:
- WCF services, Configure Service Reference dialog box
- service references [Visual Studio], configuring behavior
- Configure Service Reference dialog box
ms.assetid: 25e4c36b-2db6-4e71-9010-b7068255d09d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: f5bae3acb6f687c8c787e2d4121999d1133b0f1f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75586927"
---
# <a name="configure-service-reference-dialog-box"></a>[サービス参照の構成] ダイアログ ボックス

[ **サービス参照の構成** ] ダイアログボックスでは、WINDOWS COMMUNICATION FOUNDATION (WCF) サービスの動作を構成できます。

**[サービス参照の構成]** ダイアログ ボックスにアクセスするには、**ソリューション エクスプローラー**でサービス参照を右クリックし、**[サービス参照の構成]** を選択します。 **[サービス参照の追加] ダイアログ ボックス**で **[詳細]** ボタンをクリックしてダイアログ ボックスにアクセスすることもできます。

## <a name="task-list"></a>タスク一覧

- WCF サービスがホストされるアドレスを変更するには、**[アドレス]** フィールドに新しいアドレスを入力します。

- WCF クライアント内のクラスのアクセス レベルを変更するには、**[生成されたクラスのアクセス レベル]** リストでアクセス レベル キーワードを選択します。

- WCF サービスのメソッドを非同期に呼び出すには、**[非同期操作を生成する]** チェック ボックスをオンにします。

- WCF クライアントでメッセージ コントラクト型を生成するには、**[メッセージ コントラクトを常に生成]** チェック ボックスをオンにします。

- WCF クライアントのリストまたはディクショナリ コレクションの型を指定するには、**[コレクション型]** リストおよび **[ディクショナリ コレクション型]** リストから型を選択します。

- 型の共有を無効にするには、**[参照されたアセンブリで型を再利用]** チェック ボックスをオフにします。 参照されたアセンブリのサブセットで型の共有を有効にするには、**[参照されたアセンブリで型を再利用]** チェック ボックスをオンにし、**[参照されたアセンブリを指定して型を再利用]** チェック ボックスをオンにして、**[Referenced assemblies list]\(参照されたアセンブリの一覧\)** で必要な参照を選択します。

## <a name="uielement-list"></a>UIElement の一覧

**アドレス**

サービス参照がサービスを検索する web アドレスを更新します。 たとえば、開発時には、サービスが開発サーバーでホストされ、後で運用サーバーに移動され、アドレスの変更が必要になることがあります。

> [!NOTE]
> Address 要素は、**[サービス参照の構成]** ダイアログ ボックスが **[サービス参照の追加] ダイアログ ボックス**から表示された場合は使用できません。

**[生成されたクラスのアクセス レベル]**

WCF クライアント クラスのコード アクセス レベルを特定します。

> [!NOTE]
> Web サイト プロジェクトの場合、このオプションは常に `Public` に設定され、変更できません。 詳細については、「[サービス参照のトラブルシューティング](../data-tools/troubleshooting-service-references.md)」を参照してください。

**[非同期操作を生成する]**

WCF サービスメソッドを同期的に呼び出すか (既定値)、非同期的に呼び出すかを指定します。

**[タスク ベースの操作を生成する]**

このオプションを使用すると、非同期コードを記述するときに、.NET 4 で導入されたタスク並列ライブラリ (TPL) を利用できます。 「 [タスク並列ライブラリ (TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl)」を参照してください。

**[メッセージ コントラクトを常に生成]**

WCF クライアントに対してメッセージコントラクト型を生成するかどうかを決定します。 メッセージ コントラクトの詳細については、「[メッセージ コントラクトの使用](/dotnet/framework/wcf/feature-details/using-message-contracts)」を参照してください。

**[コレクション型]**

WCF クライアントのリスト コレクション型を指定します。 既定の型は <xref:System.Array> です。

**[ディクショナリ コレクション型]**

WCF クライアントのディクショナリ コレクション型を指定します。 既定の型は <xref:System.Collections.Generic.Dictionary%602> です。

**[参照されたアセンブリで型を再利用]**

サービスが追加または更新されたときに新しい型を生成するのではなく、参照されたアセンブリに既に存在するものを WCF クライアントで再利用するかどうかを指定します。 既定では、このチェック ボックスはオンになっています。

**[参照されたアセンブリすべてで型を再利用]**

選択すると、[参照された **アセンブリ] の一覧** にあるすべての型が、可能な場合は再利用されます。 既定では、このオプションが選択されています。

**[参照されたアセンブリを指定して型を再利用]**

選択した場合、[参照された **アセンブリ] の一覧** で選択した型のみが再利用されます。

**[Referenced assemblies list]\(参照されたアセンブリの一覧\)**

プロジェクトまたは web サイトの参照アセンブリの一覧が含まれています。 [ **指定された参照アセンブリで型を再利用**する] を選択すると、個々のアセンブリを選択またはクリアできます。

**[Web 参照の追加]**

**[Web 参照の追加]** ダイアログ ボックスを表示します。

> [!NOTE]
> このオプションは、.NET Framework のバージョン2.0 を対象とするプロジェクトに対してのみ使用してください。
>
> [!NOTE]
> [ **Web 参照の追加**] ボタンは、[**サービス参照の追加] ダイアログボックス**の [**サービス参照の構成**] ダイアログボックスが表示されている場合にのみ使用できます。

## <a name="see-also"></a>こちらもご覧ください

- [方法 : Web サービスへの参照を追加する](how-to-add-update-or-remove-a-wcf-data-service-reference.md)
- [Windows Communication Foundation サービスと WCF Data Services](../data-tools/configure-service-reference-dialog-box.md)
