# InboundResponse Reference

The InboundResponse is a Message responsible to provide feedback if the message was accepted by the receiver.

> The receipt information is not the final information and means that the message was accepted but not processed.
> To ask if the message was processed please see the Query Section


### Fields of the Message

|Field|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|id|The id of the Message|Alphanumeric String|123456978696050595050AAAABBBDDDDD| The ID have to be unique inside the Trading Partner|
|date|The date of the Message Generation|Datetime with Timezone|2021-10-03T22:06:45Z| The date reference is always defined with GMT-0|
|schemaVersion|The version of the GS1 HC Schema used|Double|1.0||
|sender|The Sender of the Transaction|Partner (see XSD)|```<sender><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></sender>```||
|receiver|The Receiver of the Transaction|Partner (see XSD)|```<receiver><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></receiver>```||
|receipt|The content of the Message|Content (see XSD)|1910191019333440ABCAHYG|Receipt identification of the transaction|

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

### List of error codes

|Error Code|Error Description|Note|
|----------|-----------------|------|
|400|Unable to process|The server is unable to process the request due to problems in the message|
|401|Unauthorized|The sender is not authorized to send messages to this server|
|402|Invalid Parameters|The server is unable to process the request due to invalid parameters| 
|500|Server Error|The server is unable to process the request due to problems in the server| 
