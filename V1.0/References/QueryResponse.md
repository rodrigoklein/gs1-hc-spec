# QueryResponse Reference

The QueryResponse is a Message returned by a Server when it receives a QueryRequest.


### Fields of the QueryResponse

|Field|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|id|The Message ID|Alphanumeric String|123456978696050595050AAAABBBDDDDD| The ID has to be unique for the Trading Partner|
|date|Message Generation Date|Datetime with Timezone|2021-10-03T22:06:45Z| The date reference is always defined as GMT-0|
|schemaVersion|The version of the GS1 HC Schema used|Double|1.0||
|sender|The Sender of the Transaction|Partner (see XSD)|```<sender><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></sender>```||
|receiver|The Receiver of the Transaction|Partner (see XSD)|```<receiver><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></receiver>```||
|response|list of QueryResponseItem|QueryResponseItem(see XSD)|```<response><queryResponseItem><date>2021-10-04T16:16:40Z</date><content format="SNCM" schemaVersion="1.0" encoding="XML">  <fileURL>https://sampleurl.sampledomain.com/fileXXXXXXXX-0.xml</fileURL></content></queryResponseItem></response>```|List of QueryResponseItem |
|error|list of Error|Error (see XSD)||List of Error |
##### Sample

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<QueryResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-04T16:16:40Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </receiver>
    <response>
        <queryResponseItem>
            <date>2021-10-04T16:16:40Z</date>
            <content format="SNCM" schemaVersion="1.0" encoding="XML">
                <fileURL>https://sampleurl.sampledomain.com/fileXXXXXXXX-0.xml</fileURL>
            </content>
        </queryResponseItem>
        <queryResponseItem>
            <date>2021-10-04T16:16:40Z</date>
            <content format="SNCM" schemaVersion="1.0" encoding="XML">
                <fileURL>https://sampleurl.sampledomain.com/fileXXXXXXXX-1.xml</fileURL>
            </content>
        </queryResponseItem>
        <queryResponseItem>
            <date>2021-10-04T16:16:40Z</date>
            <content format="SNCM" schemaVersion="1.0" encoding="XML">
                <fileURL>https://sampleurl.sampledomain.com/fileXXXXXXXX-2.xml</fileURL>
            </content>
        </queryResponseItem>
        <queryResponseItem>
            <date>2021-10-04T16:16:40Z</date>
            <content format="SNCM" schemaVersion="1.0" encoding="XML">
                <fileURL>https://sampleurl.sampledomain.com/fileXXXXXXXX-3.xml</fileURL>
            </content>
        </queryResponseItem>
        <queryResponseItem>
            <date>2021-10-04T16:16:40Z</date>
            <content format="EPCIS" schemaVersion="2.0" encoding="XML">
                <fileURL>https://sampleurl.sampledomain.com/fileXXXXXXXX-4.xml</fileURL>
            </content>
            <additionalInfo>
                <info key="AttorneyAuthorization">https://files.xxxx.com/0000000111212.xml</info>
            </additionalInfo>
        </queryResponseItem>       
    </response>
</QueryResponse>
```
##### Sample with Error

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<QueryResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-04T16:16:40Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
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
			<errorCode>400</errorCode>
			<errorDescription>Unable to process</errorDescription>
		</error>
    </response>
</QueryResponse>
```
### Sample with messages

#### QueryResponse with Message

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<QueryResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-06T12:52:01Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
    	   <partnerKey>CNPJ</partnerKey>
        <partnerKey>83042274000167</partnerKey>
    </receiver>
    <response>
        <message>
            <messageCode>200</messageCode>
            <messageDescription>Message Accepted</messageDescription>
        </message>
    </response>
</QueryResponse>
```

The messages and the errors were inspired in HTTP request codes and you can see below the small list of codes allowed.

> This is a start point of the message and error list.<br>
> The list can be improved in the future.

### List of message codes

|Message Code|Message Description|Note|
|----------|-----------------|------|
|200|Message Accepted|The message was accepted|
|201|Message Processed|The Message was Processed|


### List of error codes

|Error Code|Error Description|Note|
|----------|-----------------|------|
|400|Unable to process|The server is unable to process the request due to problems in the message|
|401|Unauthorized|The sender is not authorized to send messages to this server|
|500|Server Error|The server is unable to process the request due to problems in the server| 
