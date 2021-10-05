# QueryRequest Reference

The QueryRequest is a Message responsbile to carry information to query a HC Server.


### Fields of the QueryRequest

|Field|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|id|The id of the Message|Alphanumeric String|123456978696050595050AAAABBBDDDDD| The ID have to be unique inside the Trading Partner|
|date|The date of the Message Generation|Datetime with Timezone|2021-10-03T22:06:45Z| The date reference is always defined with GMT-0|
|schemaVersion|The version of the GS1 HC Schema used|Double|1.0||
|sender|The Sender of the Transaction|Partner (see XSD)|```<sender><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></sender>```||
|receiver|The Receiver of the Transaction|Partner (see XSD)|```<receiver><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></receiver>```||
|queryRequestItem|list of QueryrequestItem|QueryRequestItem (see XSD)|``` <queryRequestItem>
        <parameterKey>parameter</parameterKey>
        <parameterValue>value</parameterValue>
    </queryRequestItem>
    <queryRequestItem>
        <parameterKey>parameter1</parameterKey>
        <parameterValue>value1</parameterValue>
    </queryRequestItem>```|List of QueryRequestItem to pass parameters for the query|

##### Sample

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<QueryRequest id="123456978696050595050AAAABBBDDDDD" date="2021-10-04T16:16:39Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </receiver>
    <queryRequestItem>
        <parameterKey>parameter</parameterKey>
        <parameterValue>value</parameterValue>
    </queryRequestItem>
    <queryRequestItem>
        <parameterKey>parameter1</parameterKey>
        <parameterValue>value1</parameterValue>
    </queryRequestItem>
</QueryRequest>

```

### List of Parameters

|Parameter|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|index|||||
|offset|||||
|sender.Key|||||
|sender.Value|||||
|receiver.Key|||||
|receiver.Value|||||
|dateFrom|||||
|dateTo|||||
|additionalInfo.key|||||
|additionalInfo.value|||||
