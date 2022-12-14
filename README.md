# Textractor Extensions

## HttpSender

Asynchronously sends each sentence as an HTTP request. Can be used to integrate Textractor with other applications.

### Configuration

#### HttpSenderConfig.json

##### Example
```json
{
  "sentence": {
    "enabled": false,
    "url": "http://localhost:9650/sentence",
    "requestType": "PLAIN_TEXT",
    "selectedThreadOnly": true
  }
}
```

| Field                | Type                                                               |
|----------------------|--------------------------------------------------------------------|
| `enabled`*           | boolean                                                            |
| `url`                | string                                                             |
| `requestType`**      | `"PLAIN_TEXT"` &vert; `"JSON_TEXT"` &vert; `"JSON_TEXT_WITH_META"` |
| `selectedThreadOnly` | boolean                                                            |

**⚠️⚠️⚠️&ast;Set `enabled` field to `true` to make it work**

##### **`requestType` field

###### PLAIN_TEXT

```http request
POST http://localhost:9650/sentence
Content-Type: text/plain; charset=UTF-8

Lorem ipsum dolor sit amet
```

###### JSON_TEXT

```http request
POST http://localhost:9650/sentence
Content-Type: application/json; charset=UTF-8

{
  "text": "Lorem ipsum dolor sit amet"
}
```

###### JSON_TEXT_WITH_META

```http request
POST http://localhost:9650/sentence
Content-Type: application/json; charset=UTF-8

{
  "text": "Lorem ipsum dolor sit amet",
  "meta": {
    "isCurrentSelect": true,    // sentenceInfo["current select"]
    "processId": 2898235,       // sentenceInfo["process id"]
    "threadNumber": 12,         // sentenceInfo["text number"]
    "threadName": "Some name",  // sentenceInfo["text name"]
    "timestamp": 1669721578
  }
}
```

## TextractorTranslatorBridge

Zero config version of `HttpSender` special for [Textractor Translator](https://github.com/MRGRD56/textractor-translator)

Matches the following config of `HttpSender`:

```json
{
  "sentence": {
    "enabled": true,
    "method": "POST",
    "url": "http://localhost:18952/sentence",
    "requestType": "JSON_TEXT_WITH_META",
    "selectedThreadOnly": true
  }
}
```
