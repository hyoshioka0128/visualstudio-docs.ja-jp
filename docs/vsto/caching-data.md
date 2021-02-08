---
title: キャッシュ データ
description: ドキュメントレベルのカスタマイズでデータオブジェクトをキャッシュして、Microsoft Office Word または Excel を開かずにデータにアクセスできるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], about caching data
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f31556e64ee93a73fb09c27edd095bcd2653dfdc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99836164"
---
# <a name="cache-data"></a>キャッシュ データ
  ドキュメントレベルのカスタマイズでデータオブジェクトをキャッシュして、データにアクセスできるようにすることも、Word や Excel Microsoft Office Microsoft Office を開かずにデータにアクセスすることもできます。 オブジェクトをキャッシュするには、オブジェクトのデータ型が特定の要件を満たしている必要があります。 .NET Framework の多くの一般的なデータ型は、、、などの要件を満たし <xref:System.String> <xref:System.Data.DataSet> て <xref:System.Data.DataTable> います。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 データキャッシュにオブジェクトを追加するには、次の2つの方法があります。

- ソリューションのビルド時にオブジェクトをデータキャッシュに追加するには、 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性をオブジェクト宣言に適用します。 詳細については、「 [方法: オフラインまたはサーバー上で使用するデータをキャッシュ](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)する」を参照してください。

- 実行時にプログラムによってオブジェクトをデータキャッシュに追加するに `StartCaching` は、クラスやクラスなどのホスト項目のメソッドを使用し `ThisDocument` `ThisWorkbook` ます。 詳細については、「 [方法: Office ドキュメント内のデータソースをプログラムによってキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)」を参照してください。

  オブジェクトをデータキャッシュに追加した後は、Word または Excel を起動しなくても、キャッシュされたデータにアクセスして変更することができます。 詳細については、「 [サーバー上のドキュメントのデータにアクセス](../vsto/accessing-data-in-documents-on-the-server.md)する」を参照してください。

## <a name="requirements-for-data-objects-to-be-cached"></a>キャッシュするデータオブジェクトの要件
 ソリューションにデータオブジェクトをキャッシュするには、オブジェクトが次の要件を満たしている必要があります。

- またはクラスなど、ホスト項目の読み取り/書き込みパブリックフィールドまたはプロパティを指定し `ThisDocument` `ThisWorkbook` ます。

- インデクサーまたはその他のパラメーター化されたプロパティではありません。

  また、データオブジェクトはクラスによってシリアル化可能である必要があります <xref:System.Xml.Serialization.XmlSerializer> 。つまり、オブジェクトの型には次の特性が必要です。

- パブリック型であること。

- パラメーターのないパブリックコンストラクターを使用します。

- 追加のセキュリティ特権を必要とするコードを実行しません。

- 読み取り/書き込みのパブリックプロパティのみを公開します (その他のプロパティは無視されます)。

- 多次元配列を公開しません (入れ子になった配列が受け入れられます)。

- プロパティおよびフィールドからインターフェイスを返しません。

- <xref:System.Collections.IDictionary>コレクションの場合はを実装しません。

  データオブジェクトをキャッシュすると、は、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ドキュメント内の *カスタム xml 部分* に格納されている xml 文字列にオブジェクトをシリアル化します。 詳細については、「 [カスタム XML 部分の概要](../vsto/custom-xml-parts-overview.md)」を参照してください。

## <a name="cached-data-size-limits"></a>キャッシュされたデータサイズの制限
 ドキュメント内のデータキャッシュに追加できるデータの総量と、データキャッシュ内の個々のオブジェクトのサイズには、いくつかの制限があります。 これらの制限を超えると、データがデータキャッシュに保存されるときにアプリケーションが予期せず終了する可能性があります。

 これらの制限を回避するには、次のガイドラインに従ってください。

- 10 MB を超えるオブジェクトをデータキャッシュに追加しないでください。

- 1つのドキュメントで、データキャッシュに 100 MB を超える合計データを追加しないでください。

  これらはおおよその値です。 正確な制限は、使用可能な RAM や実行中のプロセスの数など、いくつかの要因によって異なります。

## <a name="control-the-behavior-of-cached-objects"></a>キャッシュされたオブジェクトの動作を制御する
 キャッシュされたオブジェクトの動作をより詳細に制御するには、キャッシュされた <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> オブジェクトの型にインターフェイスを実装します。 たとえば、オブジェクトが変更されたときにユーザーに通知する方法を制御する場合は、このインターフェイスを実装できます。 の実装方法を示すコード例につい <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> ては、「 `ControlCollection` Office 開発のサンプル [とチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の「Excel 動的コントロールのサンプルと Word の動的コントロールのサンプル」のクラスを参照してください。

## <a name="persist-changes-to-cached-data-in-password-protected-documents"></a>パスワードで保護されたドキュメント内のキャッシュされたデータに対する変更を保持する
 パスワードで保護されているドキュメント内のデータオブジェクトをキャッシュする場合、キャッシュされたデータへの変更は保存されません。 キャッシュされたデータへの変更を保存するには、2つのメソッドをオーバーライドします。 これらのメソッドをオーバーライドして、ドキュメントの保存時に保護を一時的に解除し、保存操作の完了後に保護を再適用します。

 詳細については、「 [方法: パスワードで保護されたドキュメントでデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)」を参照してください。

## <a name="prevent-data-loss-when-adding-null-values-to-the-data-cache"></a>データキャッシュに null 値を追加するときにデータが失われないようにする
 オブジェクトをデータキャッシュに追加する場合、ドキュメントを保存して閉じる前に、キャッシュされたすべてのオブジェクトを **null** 以外の値に初期化する必要があります。 ドキュメントを保存して閉じたときに、キャッシュされたオブジェクトに **null** 値がある場合、は、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] キャッシュされたすべてのオブジェクトをデータキャッシュから自動的に削除します。

 デザイン時に属性を使用して、 **null** 値を持つオブジェクトをデータキャッシュに追加する場合は、クラスを使用して、 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> ドキュメントを <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 開く前にキャッシュされたデータオブジェクトを初期化できます。 これは、Word または Excel がインストールされていないサーバーでキャッシュされたデータを初期化してから、ドキュメントがエンドユーザーによって開かれるようにする場合に便利です。 詳細については、「 [サーバー上のドキュメントのデータにアクセス](../vsto/accessing-data-in-documents-on-the-server.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: オフラインまたはサーバーで使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [方法: Office ドキュメント内のデータソースをプログラムによってキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [方法: パスワードで保護されたドキュメントでデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [チュートリアル: キャッシュされたデータセットを使用したマスター詳細関係の作成](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)
