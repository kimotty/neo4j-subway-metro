# neo4j-subway-metro
- neo4jサンプル metro

- input
[東京メトロ路線図](https://www.tokyometro.jp/station/)

- data
```
# data --node G00=GINZA-LINE, Z00=HANZOUMON-LINE
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

```
# data --relationship
:TYPE,station_src,station_dst,cost
GINZA, 渋谷,表参道,1
GINZA, 表参道,外苑前,1
GINZA, 外苑前,青山一丁目,1
GINZA, 青山一丁目,赤坂見附,3
GINZA, 赤坂見附,溜池山王,3
GINZA, 溜池山王,虎ノ門,3
GINZA, 虎ノ門,新橋,3
GINZA, 新橋,銀座,3
GINZA, 銀座,京橋,3
GINZA, 京橋,日本橋,4
GINZA, 日本橋,三越前,4
GINZA, 表参道,渋谷,1
GINZA, 外苑前,表参道,1
GINZA, 青山一丁目,外苑前,1
GINZA, 赤坂見附,青山一丁目,3
GINZA, 溜池山王,赤坂見附,3
GINZA, 虎ノ門,溜池山王,3
GINZA, 新橋,虎ノ門,3
GINZA, 銀座,新橋,3
GINZA, 京橋,銀座,3
GINZA, 日本橋,京橋,4
GINZA, 三越前,日本橋,4
HANZOUMON, 渋谷,表参道,1
HANZOUMON, 表参道,青山一丁目,1
HANZOUMON, 青山一丁目,永田町,2
HANZOUMON, 永田町,半蔵門,3
HANZOUMON, 半蔵門,九段下,3
HANZOUMON, 九段下,神保町,3
HANZOUMON, 神保町,大手町,2
HANZOUMON, 大手町,水天宮前,4
HANZOUMON, 水天宮前,清澄白河,4
HANZOUMON, 表参道,渋谷,1
HANZOUMON, 青山一丁目,表参道,1
HANZOUMON, 永田町,青山一丁目,2
HANZOUMON, 半蔵門,永田町,3
HANZOUMON, 九段下,半蔵門,3
HANZOUMON, 神保町,九段下,3
HANZOUMON, 大手町,神保町,2
HANZOUMON, 水天宮前,大手町,4
HANZOUMON, 清澄白河,水天宮前,4

```

- cypher node
```
# cypher node
CREATE (n:G00:Z00 {station_code: "G01:Z01", station_name : "渋谷"} )
CREATE (n:G00:Z00 {station_code: "G02:Z02", station_name : "表参道"} )
CREATE (n:G00 {station_code: "G03", station_name : "外苑前"} )
CREATE (n:G00:Z00 {station_code: "G04:Z03", station_name : "青山一丁目"} )
...
```

- cypher relationship
```
# cypher relationship
MATCH (s),(n) WHERE s.station_name="渋谷" AND n.station_name="表参道" CREATE (s)-[:GINZA{cost:1}]->(n);
MATCH (s),(n) WHERE s.station_name="表参道" AND n.station_name="外苑前" CREATE (s)-[:GINZA{cost:2}]->(n);
MATCH (s),(n) WHERE s.station_name="外苑前" AND n.station_name="青山一丁目" CREATE (s)-[:GINZA{cost:2}]->(n);
...

MATCH (s),(n) WHERE s.station_name="渋谷" AND n.station_name="表参道" CREATE (s)-[:HANZOUMON{cost:2}]->(n);
MATCH (s),(n) WHERE s.station_name="表参道" AND n.station_name="青山一丁目" CREATE (s)-[:HANZOUMON{cost:2}]->(n);
...

```
