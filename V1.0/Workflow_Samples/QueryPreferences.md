# QueryMessage Sample

Following the workflow samples, in this document we will explain how to query a HC Server to retrieve the partner Preferences.

In this scenario, you are the CNPJ 15042274000195 and your trading partner has the CNPJ 83042274000167 that is a Distributor.

You want to know how can you send the messages to his server.

- Sender - CNPJ 15042274000195 (Manufacturer)
- Receiver - CNPJ 83042274000167 (Distributor)

> Just to give a clear information, 
> the messages in this sample
> do not have the SIGNATURE tags


### Communication flow

![image info](../images/getPreferences.jpg)

Based on the scenario above, the Manufacturer will call the getPreferences method in the webservice of the Distributor.

To do this, we have to create the QueryRequest message and send throught the Manufacturer Webservice.

### Creating the QueryRequest

```xml
<?xml version="1.0" encoding="UTF-8"?>
<QueryRequest xmlns="http://hc.gs1br.org.br/" date="2021-09-28T04:57:01Z" id="123456978696050595050AAAABBBDDDDD" schemaVersion="1.0">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>83042274000167</partnerValue>
    </receiver>
    <queryRequestItem>
        <parameterKey>index</parameterKey>
        <parameterValue>0</parameterValue>
    </queryRequestItem>
    <queryRequestItem>
        <parameterKey>offset</parameterKey>
        <parameterValue>10</parameterValue>
    </queryRequestItem>
</QueryRequest>
```

The Manufacturer webservice will answer with the list of messages involved in that transaction.

### QueryResponse

````xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<QueryResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-04T16:16:40Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>83042274000167</partnerValue>
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
