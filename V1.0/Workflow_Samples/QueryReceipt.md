# QueryMessage Sample

Following the workflow samples, in this document, we will explain how to query a HC Server to retrieve the results of processing.

In this scenario, you are the CNPJ 15042274000195 and your trading partner has the CNPJ 83042274000167 that is a Distributor.

You want to know how can you send the messages to his server.

- Sender - CNPJ 15042274000195 (Manufacturer)
- Receiver - CNPJ 83042274000167 (Distributor)

> Just to give a clear information, 
> the messages in this sample
> do not have the SIGNATURE tags


### Communication flow

![image info](../images/getPreferences.jpg)

Based on the scenario above, the Manufacturer will call the getMessage method in the webservice of the Distributor.

To do this, we have to create the QueryRequest message and send it through the Distributor Webservice.


### Creating the QueryRequest

```xml
<?xml version="1.0" encoding="UTF-8"?><QueryRequest xmlns="http://hc.gs1br.org.br/" date="2021-09-27T06:13:29Z" id="123456978696050595050AAAABBBDDDDD" schemaVersion="1.0">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
    	   <partnerKey>CNPJ</partnerKey>
        <partnerKey>83042274000167</partnerKey>
    </receiver>
    <queryRequestItem>
        <parameterKey>sender.Key</parameterKey>
        <parameterValue>CNPJ</parameterValue>
    </queryRequestItem>
    <queryRequestItem>
        <parameterKey>sender.Value</parameterKey>
        <parameterValue>15042274000195</parameterValue>
    </queryRequestItem>
	<queryRequestItem>
        <parameterKey>receiver.Key</parameterKey>
        <parameterValue>CNPJ</parameterValue>
    </queryRequestItem>
    <queryRequestItem>
        <parameterKey>receiver.Value</parameterKey>
        <parameterValue>83042274000167</parameterValue>
    </queryRequestItem>
    <queryRequestItem>
        <parameterKey>receipt.id</parameterKey>
        <parameterValue>01919199103294949</parameterValue>
    </queryRequestItem>
</QueryRequest>
```

The Distributor webservice will answer with the list of the errors.

> if you receive a message with 0 errors

### QueryResponse with Message

````xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<QueryResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-06T12:52:01Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </receiver>
    <response>
        <message>
            <messageCode>9999</messageCode>
            <messageDescription>Message Received</messageDescription>
        </message>
    </response>
</QueryResponse>
```

### QueryResponse with Error

````xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<QueryResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-06T12:52:01Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
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
            <errorCode>1001</errorCode>
            <errorDescription>Unknown Error</errorDescription>
        </error>
    </response>
</QueryResponse>

```