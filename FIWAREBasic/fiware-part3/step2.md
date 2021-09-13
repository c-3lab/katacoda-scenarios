Orion Subscriptionにおける様々な設定に関して学習していきます。


# 2-1 idPatternによる検知対象の指定

変更を検知するEntityの指定方法にidPatternを使うことができます。  
idPatternは正規表現を使用しマッチしたEntityを対象とすることができます。

![idPattern](./assets/3-6.png)

今回の例では".\*"を指定することで全てのidを対象にしています。

元のTerminalで以下のコマンドを実行します。

```json
curl -v -X PATCH localhost:1026/v2/subscriptions/${SUBSCRIPTION_ID} -s -S -H 'Content-Type: application/json' -d @- <<EOF
{
  "description": "A subscription to get info about Room",
  "subject": {
    "entities": [
      {
        "idPattern"l ".*",
        "type": "Room"
      }
    ],
    "condition": {
      "attr": ["temperature"]
    }
  },
  "notification": {
    "http": {
      "url": "https://[[HOST_SUBDOMAIN]]-1028-[[KATACODA_HOST]].environments.katacoda.com/accumulate"
    },
    "attrs": [
      "temperature"
    ]
  }
}
EOF
```{{copy}}

temperatureの値を変更してみます。

`curl localhost:1026/v2/entities/Room1/attrs/temperature/value -s -S -H 'Content-Type: text/plain' -X PUT -d 29.5`{{copy}}

**Terminal2**を開きログを確認してみます。
先ほどと同じように通知された結果が確認できます。

他にも様々な条件や設定で通知を行うことができます。詳細は公式の[ngsiv2_implementation_note](uhttps://github.com/telefonicaid/fiware-orion/blob/master/doc/manuals/user/ngsiv2_implementation_notes.md#subscription-payload-validations)に記載されています。
