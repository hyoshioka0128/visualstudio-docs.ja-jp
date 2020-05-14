---
title: ドキュメントロックホルダー管理 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document locking
ms.assetid: fa1ce513-eb7d-42bc-b6e8-cb2433d051d5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f9dd520f8ad5cab1f0cfee890c4bcc388c204bb1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712122"
---
# <a name="document-lock-holder-management"></a>ドキュメントロックホルダー管理

実行中のドキュメント テーブル (RDT) は、開いているドキュメントの数と、そのドキュメントに含まれる編集ロックを保持します。 RDT のドキュメントをプログラムで編集するときに、ドキュメント ウィンドウで開いているドキュメントを表示せずに、編集ロックをバックグラウンドで編集できます。 この機能は、グラフィカル ユーザー インターフェイスを通じて複数のファイルを変更するデザイナーによってよく使用されます。

## <a name="document-lock-holder-scenarios"></a>ドキュメント ロック ホルダのシナリオ

### <a name="file-a-has-a-dependence-on-file-b"></a>ファイル "a" はファイル "b" に依存しています

ファイルの種類 "a" に対して標準エディタ "A" を実装し、"a" 型の各ファイルがタイプ b のファイルへの参照 (または依存) を持つ状況を考えてみましょう。 タイプ "b" のファイルには、標準のエディタ "B" が存在します。 エディタ "A" がファイル "a" を開くと、対応するファイル "b" への参照が取得されます。 ファイル "b" は表示されませんが、エディタ "A" は変更できます。 エディタ "A" は、メソッドからファイル "b" のドキュメント<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>データへの参照を取得し、ファイル "b" の編集ロックも維持します。 エディタ "A" の変更が完了したら、ファイル "b" の編集ロックカウントをメソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A>呼び出して減らすことができます。 パラメーター`dwRDTLockType`を _VSRDTFLAGS に設定してメソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>呼び出した場合は、この手順を省略できます[。RDT_NoLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_NoLock>).

### <a name="file-b-is-opened-by-a-different-editor"></a>ファイル "b" は別のエディターで開かれます

エディタ "B" がエディタ "B" で開かれている場合、エディタ "A" が開こうとすると、次の 2 つの別々のシナリオを処理できます。

- 互換性のあるエディタでファイル "b" を開いている場合は、このメソッドを使用して、エディタ "A" がファイル<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A>"b" のドキュメント編集ロックを登録する必要があります。 エディタ "A" の変更が完了したら、"b" を使用してドキュメント編集ロックを<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnregisterDocumentLockHolder%2A>解除します。

- ファイル "b" が互換性のない方法で開かれている場合は、エディタ "A" によるファイル "b" の開きが失敗するか、エディタ "A" に関連付けられたビューを部分的に開いて適切なエラー メッセージを表示することができます。 このエラー メッセージは、互換性のないエディタでファイル "b" を閉じ、エディタ "A" を使用してファイル "a" を開き直す必要があります。 互換性のないエディターで[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]開いている<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable2.QueryCloseRunningDocument%2A>ファイル "b" を閉じるようユーザーに求めるメソッドを実装することもできます。 ユーザーがファイル "b" を閉じると、エディタ "A" でファイル "a" を開くのは正常に続行されます。

## <a name="additional-document-edit-lock-considerations"></a>ドキュメント編集ロックに関するその他の考慮事項

エディタ "A" がファイル "b" のドキュメント編集ロックを持つ唯一のエディタである場合、エディタ "B" がファイル "b" のドキュメント編集ロックを保持している場合とは異なる動作を得ます。 クラス[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]**デザイナー**は、関連付けられたコード ファイルに対する編集ロックを保持しないビジュアル デザイナーの例です。 つまり、ユーザーがデザイン ビューでクラス ダイアグラムを開き、関連付けられたコード ファイルを同時に開いた場合、ユーザーがコード ファイルを変更しても変更を保存しない場合、変更はクラス ダイアグラム (.cd) ファイルにも失われます。 クラス**デザイナー**にコード ファイルに対するドキュメント編集ロックが唯一の場合、ユーザーはコード ファイルを閉じるときに変更を保存するように求めらないです。 IDE は、ユーザーが**クラス デザイナー**を閉じた後にのみ、変更を保存するようにユーザーに求めます。 保存された変更は両方のファイルに反映されます。 **クラス デザイナー**とコード ファイル エディターの両方が、コード ファイルに対するドキュメント編集ロックを保持している場合、コード ファイルまたはフォームを閉じるときに保存するように求められます。 その時点で、保存された変更はフォームとコード ファイルの両方に反映されます。 クラス ダイアグラムの詳細については、「クラス[ダイアグラムの操作 (クラス デザイナー)」](../ide/class-designer/designing-and-viewing-classes-and-types.md)を参照してください。

エディタ以外のドキュメントに編集ロックを設定する必要がある場合は、インタフェースを実装する<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>必要があります。

コード ファイルをプログラムによって変更する UI デザイナーは、複数のファイルに変更を加えることがよくあります。 このような場合、メソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell2.SaveItemsViaDlg%2A>は **、次の項目への変更を保存しますか?**

## <a name="see-also"></a>関連項目

- [ドキュメント テーブルの実行](../extensibility/internals/running-document-table.md)
- [永続性と実行中のドキュメントテーブル](../extensibility/internals/persistence-and-the-running-document-table.md)
