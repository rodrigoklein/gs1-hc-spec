# InboundResponse Reference

The InboundResponse is a Message aimed to provide feedback to the sender that the message was accepted by the receiver.

> The receipt information is not the final response, meaning the message was accepted but not processed.
> To ask if the message was processed please see the Query Section

### Fields of the Message with Receipt

|Field|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|id|The Message ID|Alphanumeric String|123456978696050595050AAAABBBDDDDD| The ID has to be unique for the Trading Partner|
|date|Message Generation Date|Datetime with Timezone|2021-10-03T22:06:45Z| The date reference is always defined as GMT-0|
|schemaVersion|The version of the GS1 HC Schema used|Double|1.0||
|sender|The Sender of the Transaction|Partner (see XSD)|```<sender><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></sender>```||
|receiver|The Receiver of the Transaction|Partner (see XSD)|```<receiver><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></receiver>```||
|receipt|The content of the Message|Content (see XSD)|1910191019333440ABCAHYG|Receipt identification of the transaction|

##### Sample

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<InboundResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-04T15:24:05Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </receiver>
    <receipt>1910191019333440ABCAHYG</receipt>
</InboundResponse>
```

### Fields of the Message with Error

|Field|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|id|The Message ID|Alphanumeric String|123456978696050595050AAAABBBDDDDD| The ID has to be unique for the Trading Partner|
|date|Message Generation Date|Datetime with Timezone|2021-10-03T22:06:45Z| The date reference is always defined as GMT-0|
|schemaVersion|The version of the GS1 HC Schema used|Double|1.0||
|sender|The Sender of the Transaction|Partner (see XSD)|```<sender><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></sender>```||
|receiver|The Receiver of the Transaction|Partner (see XSD)|```<receiver><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></receiver>```||
|response|list of Errors|ErrorList (see XSD)|```<response><error><errorCode>1001</errorCode><errorDescription>Nodata</errorDescription></error><error><errorCode>2001</errorCode><errorDescription>Invalid parameters</errorDescription></error></response>```|List of Errors|

##### Sample

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<InboundResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-04T16:16:39Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </receiver>
    <response>
        <error>
            <errorCode>402</errorCode>
            <errorDescription>Invalid parameters</errorDescription>
        </error>
    </response>
</InboundResponse>
```



