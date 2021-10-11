# PreferenceData Reference

The PreferenceData is the message returned by the getPreferences webservice method.


### Fields of the PreferenceData

|Field|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|id|The Message ID|Alphanumeric String|123456978696050595050AAAABBBDDDDD| The ID has to be unique for the Trading Partner|
|date|Message Generation Date|Datetime with Timezone|2021-10-03T22:06:45Z| The date reference is always defined as GMT-0|
|schemaVersion|The version of the GS1 HC Schema used|Double|1.0||
|partner|The source partner of the response|Partner (see XSD)|```<partner><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></partner>```||
|preferences|list of preferences|info (see XSD)|```<preferences><info key="key0">value0</info><info key="key1">value1</info><info key="key2">value2</info><info key="key3">value3</info><info key="key4">value4</info></preferences>```|List of info |

##### Sample
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<PreferenceData id="123456978696050595050AAAABBBDDDDD" date="2021-10-04T16:16:40Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <partner>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </partner>
    <preferences>
        <info key="key0">value0</info>
        <info key="key1">value1</info>
        <info key="key2">value2</info>
        <info key="key3">value3</info>
        <info key="key4">value4</info>
    </preferences>
</PreferenceData>
```

### Allowed PreferenceData

|Preference|Description|Data Type|Note|
|----------|-----------|---------|----|
|epcis.allowed|If the server accepts the EPCIS BR Standard|true/false||
|base64message.allowed|If the server accept base64 messages in the body|true/false||

