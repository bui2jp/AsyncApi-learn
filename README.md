# AsyncApi-learn (nodejs-template)

https://www.asyncapi.com/

## @asyncapi/nodejs-template の利用

https://github.com/asyncapi/nodejs-template

### nodejs-template でサポートされているプロトコル
AMQP, MQTT, Kafka, WebSocket

### snippet
```
$ sudo npm install -g @asyncapi/generator
```

定義ファイルをローカルへ落としておく
```
$ curl https://raw.githubusercontent.com/asyncapi/asyncapi/2.0.0/examples/2.0.0/streetlights.yml > streetlights.yml
```

nodejsのcodeをGenerate
```
$ sudo ag streetlights.yml @asyncapi/nodejs-template -o output -p server=production
```

```
$ sudo ag streetlights.yml ./ -o output -p server=production
```

実行
```
$ cd output
$ npm i
$ npm start
```

nodejsのmqttを使って動作確認
```
$ npm install mqtt -g
$ mqtt pub -t 'smartylighting/streetlights/1/0/event/123/lighting/measured' -h 'test.mosquitto.org' -m '{"id": 1, "lumens": 3, "sentAt": "2017-06-07T12:34:32.000Z"}'
```

デフォルトではテスト用のブローカー(test.mosquitto.org)を利用している
変更するには output/config/common.yml の url を編集
```
default:
  app:
    name: Streetlights API
    version: 1.0.0

  broker:
    mqtt:
      url: mqtt://test.mosquitto.org:1883
      topics: ["smartylighting/streetlights/1/0/event/+/lighting/measured"]
      qos:
      protocol: mqtt
      retain:
      subscribe: true
```

# documentの出力は @asyncapi/html-template
```
$ sudo ag streetlights.yml @asyncapi/html-template -o output_doc
```