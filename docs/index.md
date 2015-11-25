# Threat Lab

[Threat Lab](http://www.threatlab.io) is a PCAP analysis tool that uses [Snort](https://www.snort.org) and [Suricata](http://suricata-ids.org/) to scan network packet captures.<br/>
[EmergingThreats](http://www.emergingthreats.net/open-source/etopen-ruleset) rules are used for generating alerts.

# APIs

>You can interact and test the APIs in your browser:
>
>[http://www.threatlab.io/api/console/](http://www.threatlab.io/api/console/)

## PCAP Upload

Upload PCAP file and put in queue for analysis.

Response will include an ID that you can use in other calls, such as checking task status and retrieving alerts and errors.

```/api/pcap/v1/upload/```  

Method: ```PUT```

### Parameters

<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Parameter Type</th>
            <th>Data Type</th>
            <th>Required</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>file</td>
            <td>body</td>
            <td>file</td>
            <td>Yes</td>
            <td>Pcap file to analyze</td>
        </tr>
            <tr>
            <td>private</td>
            <td>query</td>
            <td>boolean</td>
            <td>No</td>
            <td>Hide results from public</td>
        </tr>
    </tbody>
</table>

### Error Status Codes

<table>
    <thead>
        <tr>
            <th>HTTP Status Code</th>
            <th>Reason</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>400</td>
            <td>Invalid file format</td>
        </tr>
        <tr>
            <td>200</td>
            <td>Analysis task queued successfully</td>
        </tr>
    </tbody>
</table>

### Testing with CURL

```bash
curl 'http://www.threatlab.io/api/pcap/v1/upload' --upload-file ~/Downloads/sample.pcap
```

### Sample response body

```json
{
    "id": "f7c14dc9-100d-4a01-8c9e-fe7e40b7c548"
}
```


## PCAP Status

PCAP analysis status

```/api/pcap/v1/status/{id}/```    

Method: ```GET```


### Parameters

<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Parameter Type</th>
            <th>Data Type</th>
            <th>Required</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>id</td>
            <td>path</td>
            <td>string</td>
            <td>Yes</td>
            <td>Upload ID</td>
        </tr>
    </tbody>
</table>

### Error Status Codes

<table>
    <thead>
        <tr>
            <th>HTTP Status Code</th>
            <th>Reason</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>404</td>
            <td>ID Not Found</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ID found</td>
        </tr>
    </tbody>
</table>


### Sample response body

```json
{
    "status": "READY"
}
```


## PCAP Detail

PCAP object details.

```/api/pcap/v1/detail/{id}/```  

Method: ```GET```


### Parameters

<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Parameter Type</th>
            <th>Data Type</th>
            <th>Required</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>id</td>
            <td>path</td>
            <td>string</td>
            <td>Yes</td>
            <td>Upload ID</td>
        </tr>
    </tbody>
</table>

### Error Status Codes

<table>
    <thead>
        <tr>
            <th>HTTP Status Code</th>
            <th>Reason</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>404</td>
            <td>ID Not Found</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ID found</td>
        </tr>
    </tbody>
</table>


### Sample response body

```json
{
      "id": "bd508819-79d9-4c5d-b09a-4996a067d066",
      "status": "READY",
      "is_private": false,
      "created": "2015-10-17T22:47:40.094372Z",
      "alerts": 63,
      "errors": 3
}
```


## PCAP Alerts

Return list of all IDS Alerts generated for the PCAP file.

```/api/pcap/v1/alerts/{id}/```  

Method: ```GET```


### Parameters

<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Parameter Type</th>
            <th>Data Type</th>
            <th>Required</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>id</td>
            <td>path</td>
            <td>string</td>
            <td>Yes</td>
            <td>Upload ID</td>
        </tr>
    </tbody>
</table>

### Error Status Codes

<table>
    <thead>
        <tr>
            <th>HTTP Status Code</th>
            <th>Reason</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>404</td>
            <td>ID Not Found</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ID found</td>
        </tr>
    </tbody>
</table>


### Sample response body

```json
{
    "count": 7,
    "next": null,
    "previous": null,
    "results": [
        {
            "text": "ET EXPLOIT Possible Internet Explorer VBscript failure to handle error case information disclosure CVE-2014-6332 Common Function Name",
            "protocol": "TCP",
            "classification": "Attempted User Privilege Gain",
            "priority": 1,
            "src_ip": "157.193.55.183",
            "dst_ip": "192.168.96.10",
            "src_port": 80,
            "dst_port": 1042,
            "tool": "SURICATA"
        },
        ...
    ]
}
```

## PCAP Errors

Errors logged during analysis.

```/api/pcap/v1/errors/{id}/```    

Method: ```GET```

### Parameters

<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Parameter Type</th>
            <th>Data Type</th>
            <th>Required</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>id</td>
            <td>path</td>
            <td>string</td>
            <td>Yes</td>
            <td>Upload ID</td>
        </tr>
    </tbody>
</table>

### Error Status Codes

<table>
    <thead>
        <tr>
            <th>HTTP Status Code</th>
            <th>Reason</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>404</td>
            <td>ID Not Found</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ID found</td>
        </tr>
    </tbody>
</table>

### Sample response body

```json
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "error": "Invalid file format",
            "tool": "SNORT",
            "pcap": "http://www.threatlab.io/api/pcap/v1/3dbcaa40-cd9b-4fdf-87ec-8cf226e582ff"
        },
        ...
    ]
}
```

# Pagination

ThreatLab API uses "Limit-Offset" pagination.
The client includes both a "limit" and an "offset" query parameter. 
The limit indicates the maximum number of items to return. The default limit size is 10. 
The offset indicates the starting position of the query in relation to the complete set of unpaginated items.

Request example:

```curl
GET http://www.threatlab.io/api/pcap/v1/alerts/3dbcaa40-cd9b-4fdf-87ec-8cf226e582ff/?limit=5&offset=5
```

Response:

```json
{
    "count": 10,
    "next": null,
    "previous": "http://www.threatlab.io/api/pcap/v1/alerts/3dbcaa40-cd9b-4fdf-87ec-8cf226e582ff/?limit=5",
    "results": [
        ...
    ]
}
```
