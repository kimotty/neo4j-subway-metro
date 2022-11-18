# neo4j-subway-metro
- neo4jサンプル metro

- input
[東京メトロ路線図](https://www.tokyometro.jp/station/)

- data
```
# data
:ID,:LABLE,station_code,station_name,
ST001,G00:Z00,G01:Z01,渋谷
ST002,G00:Z00,G02:Z02,表参道
ST003,G00,G03,外苑前
ST004,G00:Z00,G04:Z03,青山一丁目
ST005,G00,G05,赤坂見附
ST006,G00,G06,溜池山王
ST007,G00,G07,虎ノ門
ST008,G00,G08,新橋
ST009,G00,G09,銀座
ST010,G00,G10,京橋
ST011,G00,G11,日本橋
ST012,G00:Z00,G12:Z09,三越前
ST024,Z00,Z04,永田町
ST025,Z00,Z05,半蔵門
ST026,Z00,Z06,九段下
ST027,Z00,Z07,神保町
ST028,Z00,Z08,大手町
ST030,Z00,Z10,水天宮前
ST031,Z00,Z11,清澄白河
```

- cypher
```
# cypher
CREATE (n:G00:Z00 {station_code: "G01:Z01", station_name : "渋谷"} )
CREATE (n:G00:Z00 {station_code: "G02:Z02", station_name : "表参道"} )
CREATE (n:G00 {station_code: "G03", station_name : "外苑前"} )
CREATE (n:G00:Z00 {station_code: "G04:Z03", station_name : "青山一丁目"} )

```

