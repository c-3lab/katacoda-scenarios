様々なEntityの取得方法を紹介していきます。

# 3-1 idを指定したEntityの取得

**/v2/entities/{id}**を使用して特定のEntityを取得することもできます。

`curl localhost:1026/v2/entities/Room1 | jq`{{copy}}

# 3-2 typeを指定したEntityの取得

**/v2/entities**を使用して特定のEntityを取得することもできます。

`curl localhost:1026/v2/entities?type=Room | jq`{{copy}}

# 3-3 Key Value形式での取得

keyValuesオプションを使うことでattributeを属性値だけ取得するようにできます

`curl localhost:1026/v2/entities/Room1?options=keyValues | jq`{{copy}}

# 3-4 Values形式での取得

さらにコンパクトにValuesオプションを使ってattirbuteの値のみの配列を取得することもできます。

`curl localhost:1026/v2/entities/Room1?options=values | jq`{{copy}}

attrsを指定することで取得するattributeの指定と順序を指定することができます。

`curl localhost:1026/v2/entities/Room1?options=values&attrs=temperature,pressure | jq`{{copy}}

# 3-5 attributeの取得

**/v2/entities/{id}/attrs/**を使用してattributeのみを取得することができます。

`curl localhost:1026/v2/entities/Room1/attrs/ | jq`{{copy}}

**/v2/entities/{id}/attrs/{attrsName}**を使用することによって単一のattributeを取得することもできます。

`curl localhost:1026/v2/entities/Room1/attrs/temperature | jq`{{copy}}

# 3-6 attribute valueの取得

**/v2/entities/{id}/attrs/{attrsName}/value**で指定したattributeのvalueのみを取得することもできます。

`curl localhost:1026/v2/entities/Room1/attrs/temperature/value`{{copy}}

# 3-7 その他高度なEntityの取得

## 3-7-1 idPatternによるEntityの取得

idPatterオプションを使うことで正規表現によってEntityをフィルタリングすることができます。  
以下のコマンドではidがRoomから始まり、次に数字が1~2の範囲に続くEntityを取得することができます。

`curl localhost:1026/v2/entities?idPattern=^Room[1-2] -g | jq`{{copy}}


## 3-7-2 クエリ言語によるEntityの取得

qオプションにより、クエリ言語によるフィルタリングを行うことができます。  
以下のコマンドではtemperatureのvalueが22よりも大きいEntityを取得することができます。

`curl 'localhost:1026/v2/entities?q=temperature>22' | jq`{{copy}}

[FIWARE NGSI v2 Specification](http://telefonicaid.github.io/fiware-orion/api/v2/stable/)の**SimpleQueryLanguage**の項目に様々な指定方法が書かれています。
