# Receiving Sample

Following the supply chain flow, after the Shipment by one of the trading partners we have the receiving of goods by the other one.

For a better understanding of this Receiving simulation, please refer to the Shipment Sample.

[Shipment Sample](ShipmentSample.md)

In the Receiving scenario, we will process the message that was sent by a trading partner.

If in the last example (Shipment), the sender was a manufacturer with the CNPJ 15042274000195, now we need to reverse the trading partners’ CNPJs because the flow now is focused on the distributor that needs to confirm the receiving of the goods.

- Sender - CNPJ 83042274000167 (Distributor)
- Receiver - CNPJ 15042274000195 (Manufacturer)

> Just be aware that the messages 
> in this example do not have 
> the SIGNATURE tags

### Communication flow

![image info](../images/ReceivingImage.jpg)

### Sending message to SNCM

This is the message to be sent to the SNCM:


```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<msgEvtIn xmlns="http://sncm.anvisa.gov.br/">
    <docId>38C78456D9444E609F4E</docId>
    <ccTime>2021-08-19T19:29:31Z</ccTime>
    <ver>0.01</ver>
    <lc>pt-BR</lc>
    <env>1</env>
    <declarant>
        <cnpj>83042274000167</cnpj>
    </declarant>
    <mbrAgt>83042274000167</mbrAgt>
    <usrAgt>T2 Software S.A - V1.0</usrAgt>
    <evts>
        <rec>
            <evtNotifId>73A1E095C3B547F281FF</evtNotifId>
            <realTime>true</realTime>
            <pastTime>2021-08-19T19:29:31Z</pastTime>
            <fit>false</fit>
            <prtnr>
                <cnpj>15042274000195</cnpj>
            </prtnr>
            <carrs>
                <car>
                    <cnpj>73042274000167</cnpj>
                </car>
            </carrs>
            <pld>
                <dui>
                    <gtin>07891234545454</gtin>
                    <serl>01010101001010</serl>
                    <exp>2021-08</exp>
                    <lot>LOTE</lot>
                </dui>
                <dui>
                    <gtin>07891234545454</gtin>
                    <serl>01010101001011</serl>
                    <exp>2021-08</exp>
                    <lot>LOTE</lot>
                </dui>
                <dui>
                    <gtin>07891234545454</gtin>
                    <serl>01010101001012</serl>
                    <exp>2021-08</exp>
                    <lot>LOTE</lot>
                </dui>                
            </pld>
        </rec>
    </evts>
</msgEvtIn>
```

### Preparing the Horizontal Communication

Once the message is ready, the distributor needs to inform the manufacturer that the goods were received.

To perform this operation the distributor needs to package this information into the Horizontal Communication message called InboundMessage and the distributor also needs to know the address of the manufacturer’s webservice.

There are two options to handle the information within the InboundMessage message.

- Store the message in a public address and use the fileurl tag;
- Encode the message in a BASE64 format and use the filecontent tag

In this example, we will use the base64 format.

The message above in BASE64 seems like below.

```base64
PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9InllcyI/Pgo8bXNnRXZ0SW4geG1sbnM9Imh0dHA6Ly9zbmNtLmFudmlzYS5nb3YuYnIvIj4KICAgIDxkb2NJZD4zOEM3ODQ1NkQ5NDQ0RTYwOUY0RTwvZG9jSWQ+CiAgICA8Y2NUaW1lPjIwMjEtMDgtMTlUMTk6Mjk6MzFaPC9jY1RpbWU+CiAgICA8dmVyPjAuMDE8L3Zlcj4KICAgIDxsYz5wdC1CUjwvbGM+CiAgICA8ZW52PjE8L2Vudj4KICAgIDxkZWNsYXJhbnQ+CiAgICAgICAgPGNucGo+ODMwNDIyNzQwMDAxNjc8L2NucGo+CiAgICA8L2RlY2xhcmFudD4KICAgIDxtYnJBZ3Q+ODMwNDIyNzQwMDAxNjc8L21ickFndD4KICAgIDx1c3JBZ3Q+VDIgU29mdHdhcmUgUy5BIC0gVjEuMDwvdXNyQWd0PgogICAgPGV2dHM+CiAgICAgICAgPHJlYz4KICAgICAgICAgICAgPGV2dE5vdGlmSWQ+NzNBMUUwOTVDM0I1NDdGMjgxRkY8L2V2dE5vdGlmSWQ+CiAgICAgICAgICAgIDxyZWFsVGltZT50cnVlPC9yZWFsVGltZT4KICAgICAgICAgICAgPHBhc3RUaW1lPjIwMjEtMDgtMTlUMTk6Mjk6MzFaPC9wYXN0VGltZT4KICAgICAgICAgICAgPGZpdD5mYWxzZTwvZml0PgogICAgICAgICAgICA8cHJ0bnI+CiAgICAgICAgICAgICAgICA8Y25waj4xNTA0MjI3NDAwMDE5NTwvY25waj4KICAgICAgICAgICAgPC9wcnRucj4KICAgICAgICAgICAgPGNhcnJzPgogICAgICAgICAgICAgICAgPGNhcj4KICAgICAgICAgICAgICAgICAgICA8Y25waj43MzA0MjI3NDAwMDE2NzwvY25waj4KICAgICAgICAgICAgICAgIDwvY2FyPgogICAgICAgICAgICA8L2NhcnJzPgogICAgICAgICAgICA8cGxkPgogICAgICAgICAgICAgICAgPGR1aT4KICAgICAgICAgICAgICAgICAgICA8Z3Rpbj4wNzg5MTIzNDU0NTQ1NDwvZ3Rpbj4KICAgICAgICAgICAgICAgICAgICA8c2VybD4wMTAxMDEwMTAwMTAxMDwvc2VybD4KICAgICAgICAgICAgICAgICAgICA8ZXhwPjIwMjEtMDg8L2V4cD4KICAgICAgICAgICAgICAgICAgICA8bG90PkxPVEU8L2xvdD4KICAgICAgICAgICAgICAgIDwvZHVpPgogICAgICAgICAgICAgICAgPGR1aT4KICAgICAgICAgICAgICAgICAgICA8Z3Rpbj4wNzg5MTIzNDU0NTQ1NDwvZ3Rpbj4KICAgICAgICAgICAgICAgICAgICA8c2VybD4wMTAxMDEwMTAwMTAxMTwvc2VybD4KICAgICAgICAgICAgICAgICAgICA8ZXhwPjIwMjEtMDg8L2V4cD4KICAgICAgICAgICAgICAgICAgICA8bG90PkxPVEU8L2xvdD4KICAgICAgICAgICAgICAgIDwvZHVpPgogICAgICAgICAgICAgICAgPGR1aT4KICAgICAgICAgICAgICAgICAgICA8Z3Rpbj4wNzg5MTIzNDU0NTQ1NDwvZ3Rpbj4KICAgICAgICAgICAgICAgICAgICA8c2VybD4wMTAxMDEwMTAwMTAxMjwvc2VybD4KICAgICAgICAgICAgICAgICAgICA8ZXhwPjIwMjEtMDg8L2V4cD4KICAgICAgICAgICAgICAgICAgICA8bG90PkxPVEU8L2xvdD4KICAgICAgICAgICAgICAgIDwvZHVpPiAgICAgICAgICAgICAgICAKICAgICAgICAgICAgPC9wbGQ+CiAgICAgICAgPC9yZWM+CiAgICA8L2V2dHM+CjwvbXNnRXZ0SW4+
```

### Packaging the SNCM message within the HC InboundMessage Envelope.

Now the distributor needs to package the message into the InboundMessage in order to allow the message routing between the trading partners in the supply chain.

When the distributor packs this message into the InboundMessage, the XML below is created.

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<InboundMessage id="123456978696050595050AAAABBBDDDDD" date="2021-09-29T10:26:49Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>83042274000167</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </receiver>
    <carrier>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>73042274000167</partnerValue>
    </carrier>
    <content format="SNCM" schemaVersion="1.0" encoding="XML"> <fileContent>PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9InllcyI/Pgo8bXNnRXZ0SW4geG1sbnM9Imh0dHA6Ly9zbmNtLmFudmlzYS5nb3YuYnIvIj4KICAgIDxkb2NJZD4zOEM3ODQ1NkQ5NDQ0RTYwOUY0RTwvZG9jSWQ+CiAgICA8Y2NUaW1lPjIwMjEtMDgtMTlUMTk6Mjk6MzFaPC9jY1RpbWU+CiAgICA8dmVyPjAuMDE8L3Zlcj4KICAgIDxsYz5wdC1CUjwvbGM+CiAgICA8ZW52PjE8L2Vudj4KICAgIDxkZWNsYXJhbnQ+CiAgICAgICAgPGNucGo+ODMwNDIyNzQwMDAxNjc8L2NucGo+CiAgICA8L2RlY2xhcmFudD4KICAgIDxtYnJBZ3Q+ODMwNDIyNzQwMDAxNjc8L21ickFndD4KICAgIDx1c3JBZ3Q+VDIgU29mdHdhcmUgUy5BIC0gVjEuMDwvdXNyQWd0PgogICAgPGV2dHM+CiAgICAgICAgPHJlYz4KICAgICAgICAgICAgPGV2dE5vdGlmSWQ+NzNBMUUwOTVDM0I1NDdGMjgxRkY8L2V2dE5vdGlmSWQ+CiAgICAgICAgICAgIDxyZWFsVGltZT50cnVlPC9yZWFsVGltZT4KICAgICAgICAgICAgPHBhc3RUaW1lPjIwMjEtMDgtMTlUMTk6Mjk6MzFaPC9wYXN0VGltZT4KICAgICAgICAgICAgPGZpdD5mYWxzZTwvZml0PgogICAgICAgICAgICA8cHJ0bnI+CiAgICAgICAgICAgICAgICA8Y25waj4xNTA0MjI3NDAwMDE5NTwvY25waj4KICAgICAgICAgICAgPC9wcnRucj4KICAgICAgICAgICAgPGNhcnJzPgogICAgICAgICAgICAgICAgPGNhcj4KICAgICAgICAgICAgICAgICAgICA8Y25waj43MzA0MjI3NDAwMDE2NzwvY25waj4KICAgICAgICAgICAgICAgIDwvY2FyPgogICAgICAgICAgICA8L2NhcnJzPgogICAgICAgICAgICA8cGxkPgogICAgICAgICAgICAgICAgPGR1aT4KICAgICAgICAgICAgICAgICAgICA8Z3Rpbj4wNzg5MTIzNDU0NTQ1NDwvZ3Rpbj4KICAgICAgICAgICAgICAgICAgICA8c2VybD4wMTAxMDEwMTAwMTAxMDwvc2VybD4KICAgICAgICAgICAgICAgICAgICA8ZXhwPjIwMjEtMDg8L2V4cD4KICAgICAgICAgICAgICAgICAgICA8bG90PkxPVEU8L2xvdD4KICAgICAgICAgICAgICAgIDwvZHVpPgogICAgICAgICAgICAgICAgPGR1aT4KICAgICAgICAgICAgICAgICAgICA8Z3Rpbj4wNzg5MTIzNDU0NTQ1NDwvZ3Rpbj4KICAgICAgICAgICAgICAgICAgICA8c2VybD4wMTAxMDEwMTAwMTAxMTwvc2VybD4KICAgICAgICAgICAgICAgICAgICA8ZXhwPjIwMjEtMDg8L2V4cD4KICAgICAgICAgICAgICAgICAgICA8bG90PkxPVEU8L2xvdD4KICAgICAgICAgICAgICAgIDwvZHVpPgogICAgICAgICAgICAgICAgPGR1aT4KICAgICAgICAgICAgICAgICAgICA8Z3Rpbj4wNzg5MTIzNDU0NTQ1NDwvZ3Rpbj4KICAgICAgICAgICAgICAgICAgICA8c2VybD4wMTAxMDEwMTAwMTAxMjwvc2VybD4KICAgICAgICAgICAgICAgICAgICA8ZXhwPjIwMjEtMDg8L2V4cD4KICAgICAgICAgICAgICAgICAgICA8bG90PkxPVEU8L2xvdD4KICAgICAgICAgICAgICAgIDwvZHVpPiAgICAgICAgICAgICAgICAKICAgICAgICAgICAgPC9wbGQ+CiAgICAgICAgPC9yZWM+CiAgICA8L2V2dHM+CjwvbXNnRXZ0SW4+</fileContent>
    </content>
</InboundMessage>
```

### Sending the message through the DataWS Webservice.

Once the XML is created, the distributor needs to send the InboundMessage to the receiver (manufacturer) webservice using the sendMessage method.

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ws="http://ws.med.healthcare.gs1br.org/">
   <soapenv:Header/>
   <soapenv:Body>
      <ws:sendMessage>
         <inboundMessage><![CDATA[<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<InboundMessage id="123456978696050595050AAAABBBDDDDD" date="2021-09-29T10:26:49Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>83042274000167</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </receiver>
    <carrier>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>73042274000167</partnerValue>
    </carrier>
    <content format="SNCM" schemaVersion="1.0" encoding="XML"> <fileContent>PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9InllcyI/Pgo8bXNnRXZ0SW4geG1sbnM9Imh0dHA6Ly9zbmNtLmFudmlzYS5nb3YuYnIvIj4KICAgIDxkb2NJZD4zOEM3ODQ1NkQ5NDQ0RTYwOUY0RTwvZG9jSWQ+CiAgICA8Y2NUaW1lPjIwMjEtMDgtMTlUMTk6Mjk6MzFaPC9jY1RpbWU+CiAgICA8dmVyPjAuMDE8L3Zlcj4KICAgIDxsYz5wdC1CUjwvbGM+CiAgICA8ZW52PjE8L2Vudj4KICAgIDxkZWNsYXJhbnQ+CiAgICAgICAgPGNucGo+ODMwNDIyNzQwMDAxNjc8L2NucGo+CiAgICA8L2RlY2xhcmFudD4KICAgIDxtYnJBZ3Q+ODMwNDIyNzQwMDAxNjc8L21ickFndD4KICAgIDx1c3JBZ3Q+VDIgU29mdHdhcmUgUy5BIC0gVjEuMDwvdXNyQWd0PgogICAgPGV2dHM+CiAgICAgICAgPHJlYz4KICAgICAgICAgICAgPGV2dE5vdGlmSWQ+NzNBMUUwOTVDM0I1NDdGMjgxRkY8L2V2dE5vdGlmSWQ+CiAgICAgICAgICAgIDxyZWFsVGltZT50cnVlPC9yZWFsVGltZT4KICAgICAgICAgICAgPHBhc3RUaW1lPjIwMjEtMDgtMTlUMTk6Mjk6MzFaPC9wYXN0VGltZT4KICAgICAgICAgICAgPGZpdD5mYWxzZTwvZml0PgogICAgICAgICAgICA8cHJ0bnI+CiAgICAgICAgICAgICAgICA8Y25waj4xNTA0MjI3NDAwMDE5NTwvY25waj4KICAgICAgICAgICAgPC9wcnRucj4KICAgICAgICAgICAgPGNhcnJzPgogICAgICAgICAgICAgICAgPGNhcj4KICAgICAgICAgICAgICAgICAgICA8Y25waj43MzA0MjI3NDAwMDE2NzwvY25waj4KICAgICAgICAgICAgICAgIDwvY2FyPgogICAgICAgICAgICA8L2NhcnJzPgogICAgICAgICAgICA8cGxkPgogICAgICAgICAgICAgICAgPGR1aT4KICAgICAgICAgICAgICAgICAgICA8Z3Rpbj4wNzg5MTIzNDU0NTQ1NDwvZ3Rpbj4KICAgICAgICAgICAgICAgICAgICA8c2VybD4wMTAxMDEwMTAwMTAxMDwvc2VybD4KICAgICAgICAgICAgICAgICAgICA8ZXhwPjIwMjEtMDg8L2V4cD4KICAgICAgICAgICAgICAgICAgICA8bG90PkxPVEU8L2xvdD4KICAgICAgICAgICAgICAgIDwvZHVpPgogICAgICAgICAgICAgICAgPGR1aT4KICAgICAgICAgICAgICAgICAgICA8Z3Rpbj4wNzg5MTIzNDU0NTQ1NDwvZ3Rpbj4KICAgICAgICAgICAgICAgICAgICA8c2VybD4wMTAxMDEwMTAwMTAxMTwvc2VybD4KICAgICAgICAgICAgICAgICAgICA8ZXhwPjIwMjEtMDg8L2V4cD4KICAgICAgICAgICAgICAgICAgICA8bG90PkxPVEU8L2xvdD4KICAgICAgICAgICAgICAgIDwvZHVpPgogICAgICAgICAgICAgICAgPGR1aT4KICAgICAgICAgICAgICAgICAgICA8Z3Rpbj4wNzg5MTIzNDU0NTQ1NDwvZ3Rpbj4KICAgICAgICAgICAgICAgICAgICA8c2VybD4wMTAxMDEwMTAwMTAxMjwvc2VybD4KICAgICAgICAgICAgICAgICAgICA8ZXhwPjIwMjEtMDg8L2V4cD4KICAgICAgICAgICAgICAgICAgICA8bG90PkxPVEU8L2xvdD4KICAgICAgICAgICAgICAgIDwvZHVpPiAgICAgICAgICAgICAgICAKICAgICAgICAgICAgPC9wbGQ+CiAgICAgICAgPC9yZWM+CiAgICA8L2V2dHM+CjwvbXNnRXZ0SW4+</fileContent>
    </content>
</InboundMessage>]]></inboundMessage>
      </ws:sendMessage>
   </soapenv:Body>
</soapenv:Envelope>
```

### Webservice Response

The webservice will receive the message and will need to return an InboundResponse message which contains a receipt identification that must be stored by the sender in order to have the confirmation of the receiver.

```xml
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns2:sendMessageResponse xmlns:ns2="http://ws.med.healthcare.gs1br.org/">
         <return><![CDATA[<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<InboundResponse id="097752CF6D5549229D1A74CCE982FE96" date="2021-10-01T17:28:35Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>83042274000167</partnerValue>
    </sender>
	<receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </receiver>
    <receipt>097752CF6D5549229D1A</receipt>
</InboundResponse>]]></return>
      </ns2:sendMessageResponse>
   </soap:Body>
</soap:Envelope>
```

If the receiver has any problem with the message in receiving process, the server needs to send an InboundResponse with an error that indicates a problem and the message is not processed.

Problems can happen if the trading is unknown to the receiver, problems with the message format, problems with the Authorization, with the certificate, with the signature etc.


### Webservice Response with Error

Below you can find an InboundResponse confirming an Error has occurred.

If an error tag appears in the message instead of a receipt confirmation, be aware that the message cannot be considered as delivered.


```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<InboundResponse id="123456978696050595050AAAABBBDDDDD" date="2021-09-29T10:26:49Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>83042274000167</partnerValue>
    </receiver>
    <error>
        <errorCode>401</errorCode>
        <errorDescription>Unauthorized</errorDescription>
    </error>
</InboundResponse>
```
