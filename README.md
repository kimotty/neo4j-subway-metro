# neo4j-subway-metro
- neo4jサンプル metro

- input
[東京メトロ路線図](https://www.tokyometro.jp/station/)

- # data --node G00=GINZA-LINE, Z00=HANZOUMON-LINE

```
:ID,:LABEL,station_code,station_name
ST001,G00;Z00,G01:Z01,渋谷
ST002,G00;Z00,G02:Z02,表参道
ST003,G00,G03,外苑前
ST004,G00;Z00,G04:Z03,青山一丁目
ST005,G00,G05,赤坂見附
ST006,G00,G06,溜池山王
ST007,G00,G07,虎ノ門
ST008,G00,G08,新橋
ST009,G00,G09,銀座
ST010,G00,G10,京橋
ST011,G00,G11,日本橋
ST012,G00;Z00,G12:Z09,三越前
ST024,Z00,Z04,永田町
ST025,Z00,Z05,半蔵門
ST026,Z00,Z06,九段下
ST027,Z00,Z07,神保町
ST028,Z00,Z08,大手町
ST030,Z00,Z10,水天宮前
ST031,Z00,Z11,清澄白河

```

- # data --relationship

```
:START_ID,:END_ID,:TYPE,cost:int
ST001,ST002,GINZA,1
ST002,ST003,GINZA,1
ST003,ST004,GINZA,1
ST004,ST005,GINZA,3
ST005,ST006,GINZA,3
ST006,ST007,GINZA,3
ST007,ST008,GINZA,3
ST008,ST009,GINZA,3
ST009,ST010,GINZA,3
ST010,ST011,GINZA,4
ST011,ST012,GINZA,4
ST002,ST001,GINZA,1
ST003,ST002,GINZA,1
ST004,ST003,GINZA,1
ST005,ST004,GINZA,3
ST006,ST005,GINZA,3
ST007,ST006,GINZA,3
ST008,ST007,GINZA,3
ST009,ST008,GINZA,3
ST010,ST009,GINZA,3
ST011,ST010,GINZA,4
ST012,ST011,GINZA,4
ST001,ST002,HANZOUMON,1
ST002,ST004,HANZOUMON,1
ST004,ST024,HANZOUMON,2
ST024,ST025,HANZOUMON,3
ST025,ST026,HANZOUMON,3
ST026,ST027,HANZOUMON,3
ST027,ST028,HANZOUMON,2
ST028,ST012,HANZOUMON,3
ST012,ST030,HANZOUMON,4
ST030,ST031,HANZOUMON,4
ST002,ST001,HANZOUMON,1
ST004,ST002,HANZOUMON,1
ST024,ST004,HANZOUMON,2
ST025,ST024,HANZOUMON,3
ST026,ST025,HANZOUMON,3
ST027,ST026,HANZOUMON,3
ST028,ST027,HANZOUMON,2
ST012,ST028,HANZOUMON,3
ST030,ST012,HANZOUMON,4
ST031,ST030,HANZOUMON,4

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

- match
```
match p=(n)-[r:GINZA*1..]->(m) where n.station_name='渋谷' and m.station_name='三越前' return p
match p=(n)-[r:HANZOUMON*1..]->(m) where n.station_name='渋谷' and m.station_name='三越前' return p

```

- delete 
```
match(n:G00)-[r]->(m) delete  n,r,m
match(n:Z00)-[r]->(m) delete  n,r,m
```
