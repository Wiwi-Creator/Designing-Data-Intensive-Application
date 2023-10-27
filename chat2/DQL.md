# 第二章 - Data Query Language

## Data Query Language
DQL，資料查詢的語言，而關連式資料庫引入了SQL，是一種**宣告式**查詢語言，而IMS 和 CODASYL 使用 **命令式** 程式碼來查詢資料庫。

常用的程式語言是命令式的。EX:給定一個動物物種的列表，返回列表中的鯊魚可以這樣寫

``` java
function getSharks() {
    var sharks = [];
    for (var i = 0; i < animals.length; i++) {
        if (animals[i].family === "Sharks") {
            sharks.push(animals[i]);
        }
    }
    return sharks;
}
```
而SQL : 
```SQL
SELECT * FROM animals WHERE family ='Sharks';
```
命令式語言告訴計算機以特定順序執行某些操作。逐行地遍歷程式碼，評估條件，更新變數，並決定是否再迴圈一遍。

## Web 上的宣告式查詢

宣告式查詢語言的優勢不僅限於資料庫。為了說明這一點，讓我們在一個完全不同的環境中比較宣告式和命令式方法：一個 Web 瀏覽器。

假設你有一個關於海洋動物的網站。使用者當前正在檢視鯊魚頁面，因此你將當前所選的導航專案 “鯊魚” 標記為當前選中專案。
``` html
<ul>
    <li class="selected">
        <p>Sharks</p>
        <ul>
            <li>Great White Shark</li>
            <li>Tiger Shark</li>
            <li>Hammerhead Shark</li>
        </ul>
    </li>
    <li><p>Whales</p>
        <ul>
            <li>Blue Whale</li>
            <li>Humpback Whale</li>
            <li>Fin Whale</li>
        </ul>
    </li>
</ul>
```
現在想讓當前所選頁面的標題具有一個藍色的背景，以便在視覺上突出顯示。使用 CSS 實現起來非常簡單：
``` CSS
li.selected > p {
  background-color: blue;
}
```
這裡的 CSS 選擇器 li.selected > p 聲明瞭我們想要應用藍色樣式的元素的模式：即其直接父元素是具有 CSS 類 selected 的 <li> 元素的所有 <p> 元素。示例中的元素 <p>Sharks</p> 匹配此模式，但 <p>Whales</p> 不匹配，因為其 <li> 父元素缺少 class="selected"。

如果使用 XSL 而不是 CSS，你可以做類似的事情：
``` XSL
<xsl:template match="li[@class='selected']/p">
    <fo:block background-color="blue">
        <xsl:apply-templates/>
    </fo:block>
</xsl:template>
```

在 Web 瀏覽器中，使用宣告式 CSS 樣式比使用 JavaScript 命令式地操作樣式要好得多。類似地，在資料庫中，使用像 SQL 這樣的宣告式查詢語言比使用命令式查詢 API 要好得多。

## MapReduce查詢
MapReduce是一種Google推行的計算模型和資料處理方法，特別適合於分散式系統和大數據環境。

一些 NoSQL 資料儲存（MongoDB 和 CouchDB）支援有限形式的 MapReduce，作為在多個文件中執行只讀查詢的機制。

它既不是一個宣告式的查詢語言，也不是一個完全命令式的查詢 API，而是處於兩者之間。

查詢的邏輯用程式碼片段來表示，這些程式碼片段會被處理框架重複性呼叫。

Map 步驟：對每行文本進行處理，並對每個單詞產生一個 key-value 對，例如 ("apple", 1)。

Reduce 步驟：對所有具有相同 key 的 value 進行合併和聚合，計算每個單詞的總次數。

其優點是擴展性。由於每個Map和Reduce任務都是獨立的，所以可以在不同機器上平行運作。

現代許多資料處理框架深受其啟發(EX:Hadoop , Spark)

後續會再做詳細介紹。