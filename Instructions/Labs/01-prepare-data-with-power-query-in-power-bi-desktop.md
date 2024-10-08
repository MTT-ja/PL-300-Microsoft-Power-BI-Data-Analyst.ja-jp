---
lab:
  course: 'PL-300, DP-605'
  title: Power BI Desktop でデータを取得する
  module: Get Data in Power BI
---

# Power BI Desktop でデータを取得する

## **ラボのストーリー**

このラボでは、Power BI Desktop アプリケーションについて紹介し、データに接続する方法、データ プレビューの手法を使用してソース データの特性と品質を理解する方法について説明します。 学習目標は次のとおりです。

- Power BI Desktop を開く
- さまざまなデータ ソースに接続する
- Power Query を使用してソース データをプレビューする
- Power Query でデータ プロファイル機能を使用する

**この配信には約 30 分かかります。**

## **Power BI Desktop の概要**

 このタスクでは、スターター Power BI (.pbix) ファイルを開くことから始めます。 スターター ファイルにデータは含まれませんが、ラボの完了に役立つように特別に構成されています。 スターター ファイルでは、次のレポートレベルの設定が無効になっています。

- データの読み込み > 最初の読み込みでデータ ソースからリレーションシップをインポートする
- データの読み込み > データが読み込まれた後に新しいリレーションシップを自動検出する

*注: この 2 つのオプションを有効にすると、データ モデルを開発するときに役立ちますが、ラボ エクスペリエンスをサポートするために以前無効にしました。「**Power BI Desktop で変換されたデータを読み込む**」のラボでリレーションシップを作成するときに、それぞれを追加する理由について説明します。*

1. Power BI Desktop を開きます。

    ![Power BI Desktop アイコン](Linked_image_Files/02-load-data-with-power-query-in-power-bi-desktop_image1.png)

    ''ヒント: 既定では、Power BI Desktop の前に [はじめに] ダイアログ ボックスが開きます。サインインしてから、ポップアップを閉じることができます。''**

1. スターター Power BI Desktop ファイルを開くには、 **[ファイル] > [レポートを開く] > [レポートの参照]** の順に選択します。

1. **[開く]** ウィンドウで、**D:\Allfiles\Labs\01-prepare-data-with-power-query-in-power-bi-desktop\Starter** フォルダーに移動します。

1. **Sales Analysis** ファイルを選択します。

1. **[名前を付けて保存]** を使用して、ファイルのコピーを **D:\Allfiles\MySolution** フォルダーに保存します。

## **SQL Server からデータを取得する**

このタスクでは、SQL Server データベースに接続し、Power Query でクエリを作成するテーブルをインポートする方法について説明します。

1. **[ホーム]** リボン タブで、**[データ]** グループ内から **[SQL Server]** を選択します。

     ![SQL Server の [データの取得] アイコン](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image11.png)

1. **[SQL Server データベース]** ウィンドウの **[サーバー]** ボックスに「**localhost**」と入力して、**[データベース]** を空白のままにして **[OK]** を選択してください。

    "このラボでは、**localhost** を使用して SQL Server データベースに接続します。ゲートウェイ データ ソースでは **localhost** を解決できないためです。独自のソリューションを作成する場合、この方法は推奨されません。"**

1. **[SQL Server データベース]** ウィンドウで資格情報を求めるダイアログが表示されたら、 **[現在の資格情報を使用する]** 、 **[接続]** の順に選択します。

1. **[ナビゲーター]** ウィンドウで、**AdventureWorksDW2020** データベースを展開してください。

    "注: **AdventureWorksDW2020** データベースは、**AdventureWorksDW2017** サンプル データベースに基づいています。これは、コースのラボの学習目標をサポートするように変更されています。"**

1. **[DimEmployee]** テーブルを選択し、テーブル データのプレビューに注目してください。

     ![DimEmployee が示されている AdventureWorksDW2020 データベース](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image18.png)

    *注:プレビュー データで、列と行のサンプルを確認できます。*

1. テーブル データをインポートするには、次の 6 つのテーブルの横にある**チェック ボックスを選択してください**。

    - DimEmployee
    - DimEmployeeSalesTerritory
    - DimProduct
    - DimReseller
    - DimSalesTerritory
    - FactResellerSales

1. **[データの変換]** を選択してこのタスクを完了すると、Power Query エディターが開きます。

これで、Power BI にデータがインポートされ、次のタスク用に Power Query エディターが開きます。

## **Power Query エディターでデータをプレビューする**

このタスクでは、Power Query エディターが導入されるため、データを確認してプロファイリングできます。 これは、後でデータをクリーンして変換する方法を決定するのに役立ちます。 また、"Dim" というプレフィックスが付いたディメンション テーブルと、"Fact" というプレフィックスが付いたファクト テーブルの両方についても確認します。

1. **Power Query エディター** ウィンドウで、左側の **[クエリ]** ペインに注意してください。 **クエリ** ウィンドウには、チェックを付けた各テーブルに対して 1 つのクエリが含まれています。

     ![読み込まれたクエリの一覧](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image20.png)

1. 最初のクエリ **「DimEmployee」** を選択します。

    "SQL Server データベースの **DimEmployee** テーブルには、従業員ごとに 1 行が格納されます。このテーブルの行のサブセットは営業担当者を表します。これが、開発するモデルに関連します。"**

1. 左下隅にあるステータス バーに、テーブル統計情報が提供されます。テーブルには 33 列と 296 行があります。

     ![33 列、296 行のカウント](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image22.png)

1. データ プレビュー ペインで、水平方向にスクロールして、すべての列を確認します。 最後の 5 列に、**「テーブル」** または **「値」** のリンクが含まれていることに注意してください。

    *これら 5 つの列は、データベース内の他のテーブルとのリレーションシップを表します。これらは、テーブルを結合するために使用できます。テーブルの結合は「**Power BI Desktop で変換されたデータを読み込む**」のラボで行います。*

1. 列の品質を評価するには、**「表示」** リボン タブの **「データ プレビュー」** グループ内から、**「列の品質」** をオンにします。 列の品質機能を使用すると、列にある有効、エラー、または空の値の割合を簡単に判断できます。

     ![リボンの [列の品質] の選択](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image23.png)

1. **[位置]** 列に 94% の空 (null) 行があることに注目してください。

     ![94% の空の行を示す [列の品質]](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image24.png)

1. 列の分布を評価するには、**[表示]** リボン タブの **[データ プレビュー]** グループ内から、**[列の分布]** をオンにします。

1. **[位置]** 列を再度確認し、4 つの個別の値と 1 つの一意の値があることに注意してください。

1. **EmployeeKey** 列の列の分布を確認します。296 個の個別の値と 296 個の一意の値があります。

    *個別と一意でカウントが同じ場合は、列に一意の値が含まれていることを意味します。モデル化するときは、いくつかのモデル テーブルに一意の列が含まれることが重要です。このような一意の列を使用して、一対多のリレーションシップを作成できます。これは、「**Power BI Desktop でデータをモデル化する**」ラボで行います。*

     ![296 個の個別の値と 296 個の一意の値を示す列分布](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image26.png)

1. **[クエリ]** ペインで、**[DimProduct]** クエリを選択します。

    **[DimProduct]** テーブルには、その会社が販売した商品ごとに 1 行が含まれています。**

1. **[クエリ]** ペインで、**[DimReseller]** クエリを選択します。

    "**DimReseller** テーブルにはリセラーごとに 1 行が含まれます。リセラーは販売、流通を行い、Adventure Works の製品の価値を高めます。"**

1. 列値を表示するには、**「表示」** リボン タブの **「データ プレビュー」** グループ内から、**「列のプロファイル」** をオンにします。

1. **BusinessType** 列ヘッダーを選択し、データ プレビュー ペインの下にある新しいペインに注目します。

1. データ プレビュー ウィンドウで、列の統計および値の分布を確認します。

    "データ品質の問題を見てください。倉庫にラベルが 2 つあります (**Warehouse** とスペルが間違っている **Ware House**)。"**

     ![BusinessType 列の値の分布](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image31.png)

1. **[Ware House]** バーの上にカーソルを置くと、この値を持つ 5 つの行があることに気付きます。

    *変換を適用して、「**Power BI Desktop で変換されたデータを読み込む**」のラボで、これらの 5 つの行のラベルを再設定します。*

1. **[クエリ]** ペインで、**[DimSalesTerritory]** クエリを選択します。  

    "**DimSalesTerritory** テーブルには、**Corporate HQ** (本社) を含めて販売地域ごとに 1 行が含まれています。地域は国に割り当てられ、国はグループに割り当てられます。「**Power BI Desktop でデータをモデル化する**」ラボで、地域、国、またはグループ レベルでの分析をサポートする階層を作成します。"**

1. **[クエリ]** ペインで、**[FactResellerSales]** クエリを選択します。

    "**FactResellerSales** テーブルには、販売注文明細ごとに 1 行が含まれています。販売注文には 1 行以上の品目が含まれています。"**

1. **TotalProductCost** 列の列の品質を確認して、行の 8% が空であることに注意してください。

    ***TotalProductCost** 列に値がないのは、データ品質の問題です。この問題に対処するために、「**Power BI Desktop で変換されたデータを読み込む**」のラボでは、関連する **DimProduct** テーブルに格納されている製品の標準原価を使用して、欠落した値を埋めるための変換を適用します。*

## **CSV ファイルからデータを取得する**

このタスクでは、CSV ファイルに基づいて新しいクエリを作成します。

1. 新しいクエリを追加するには、**[Power Query エディター]** ウィンドウの **[ホーム]** リボン タブで、**[新しいクエリ]** グループ内から、**[新しいソース]** 下矢印を選択し、**[テキスト/CSV]** を選択します。

1. **[開く]** ウィンドウで、**D:\Allfiles\Resources** フォルダーに移動し、**ResellerSalesTargets.csv** ファイルを選択します。 **[Open (開く)]** を選択します。

1. **ResellerSalesTargets.csv** ウィンドウで、プレビュー データを確認します。 **[OK]** を選択します。

1. **[クエリ]** ペインで、**ResellerSalesTargets** クエリが追加されていることに注意してください。

    "**ResellerSalesTargets** CSV ファイルには、営業担当者ごとに 1 年につき 1 行が含まれています。各行には、12 個の月次売上目標が記録されます (千単位)。Adventure Works 社の事業年度は、7 月 1 日に開始されます。"**

1. 空の値を含む列がない点に注目してください。  月間売上目標がない場合は、代わりにハイフン文字が格納されています。

1. 列名の左側にある各列ヘッダーのアイコンを確認します。 アイコンは、列のデータ型を表します。 **123** は整数で、**ABC** はテキストです。

     ![画像 74](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image38.png)

1. 手順を繰り返し、**D:\Allfiles\Resources\ColorFormats.csv** ファイルに基づいてクエリを作成します。

    "**ColorFormats** CSV ファイルには、製品の色ごとに 1 行が含まれています。各行には、背景色とフォントの色を書式設定する HEX コードが記録されます。"**

"これで、**ResellerSalesTargets** と **ColorFormats** という 2 つの新しいクエリが作成されるはずです。"**

 ![クエリの一覧](Linked_image_Files/01-all-queries-loaded.png)

### **仕上げ**

このタスクでは、ラボを完了します。

1. **「表示」** リボン タブの **「データ プレビュー」** グループ内から、次の 3 つのデータ プレビュー オプションをオフにします。

    - 列の品質
    - 列の分布
    - 列のプロファイル

     ![画像 76](Linked_image_Files/01-prepare-data-with-power-query-in-power-bi-desktop_image40.png)

1. Power BI Desktop ファイルを**保存**します。 保留中の変更の適用を求めるダイアログが表示されたら、 **[後で適用]** を選択します。

    "ヒント: クエリを適用すると、データ モデルにデータが読み込まれます。先に適用する必要がある変換が多数あるため、これを行う準備はできていません。"**
