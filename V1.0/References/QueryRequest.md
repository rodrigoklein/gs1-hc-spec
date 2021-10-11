# QueryRequest Reference

The QueryRequest is a Message responsbile to carry information to query a HC Server.


### Fields of the QueryRequest

|Field|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|id|The Message ID|Alphanumeric String|123456978696050595050AAAABBBDDDDD| The ID has to be unique for the Trading Partner|
|date|Message Generation Date|Datetime with Timezone|2021-10-03T22:06:45Z| The date reference is always defined for GMT-0|
|schemaVersion|The version of the GS1 HC Schema used|Double|1.0||
|sender|The Sender of the Transaction|Partner (see XSD)|```<sender><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></sender>```||
|receiver|The Receiver of the Transaction|Partner (see XSD)|```<receiver><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></receiver>```||
|queryRequestItem|list of QueryrequestItem|QueryRequestItem (see XSD)|```<queryRequestItem><parameterKey>parameter</parameterKey><parameterValue>value</parameterValue></queryRequestItem><queryRequestItem><parameterKey>parameter1</parameterKey><parameterValue>value1</parameterValue></queryRequestItem>```|List of QueryRequestItem to pass parameters for the query|

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

### List of allowed Parameters


|Parameter|Description|Data Type|Required|Sample|Note|
|---------|-----------|---------|--------|------|----|
|index|initial index for query results|Numeric|N|0|Start at result 0|
|offset|final index of the query result|Numeric|N|10|Finish at result 10|
|sender.Key|Key of the sender Partner object|String|Y|Ex: CNPJ||
|sender.Value|Value of the sender Partner object|String|Y|15042274000199||
|receiver.Key|Key of the receiver Partner object|String|Y|Ex: CNPJ||
|receiver.Value|Value of the sender Partner object|String|Y|15042274000499||
|dateFrom|Query Start Date|Datetime|N|2021-10-04T16:16:39Z||
|dateTo|Query End Date|Datetime|N|2021-10-04T16:16:39Z||
|additionalInfo.key|Key of the additionalInfo tag|String|N|InvoiceNumber||
|additionalInfo.value|Value of the additionalInfo tag|String|N|10||
