# About

[ThreatLab](http://www.threatlab.io) is a PCAP analysis tool that uses [Snort](https://www.snort.org) and [Suricata](http://suricata-ids.org/) to scan network packet captures.<br/>
[EmergingThreats](http://www.emergingthreats.net/open-source/etopen-ruleset) rules are used for generating alerts.


# Pagination

ThreatLab API uses "Limit-Offset" pagination.
The client includes both a "limit" and an "offset" query parameter. 
The limit indicates the maximum number of items to return. The default limit size is 10. 
The offset indicates the starting position of the query in relation to the complete set of unpaginated items.

Request example:

```curl
GET http://www.threatlab.io/api/pcap/v1/3dbcaa40-cd9b-4fdf-87ec-8cf226e582ff/alerts/?limit=5&offset=5
```

Response:

```json
{
    "count": 10,
    "next": null,
    "previous": "http://www.threatlab.io/api/pcap/v1/3dbcaa40-cd9b-4fdf-87ec-8cf226e582ff/alerts/?limit=5",
    "results": [
        ...
    ]
}
```

# APIs

>You can interact and test the APIs in your browser:
>
>[http://www.threatlab.io/api/console/](http://www.threatlab.io/api/console/)

## PCAP Upload

Upload PCAP file for analysis

```/api/pcap/v1/upload/{filename}```  

Method: ```PUT```

<table>
<tr>
<th>Parameter</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td>filename</td>
<td>String</td>
<td>Yes</td>
<td>File name</td>
</tr>
</table>


### Testing with CURL

```bash
curl 'http://www.threatlab.io/api/pcap/v1/upload/' --upload-file ~/Downloads/sample.pcap
```

### Sample response body

```json
{
    "id": "f7c14dc9-100d-4a01-8c9e-fe7e40b7c548"
}
```


## PCAP Status

PCAP analysis status

```/api/pcap/v1/{id}/status/```    

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td>id</td>
<td>String</td>
<td>Yes</td>
<td>Upload ID</td>
</tr>
</table>


### Sample response body

```json
{
    "status": "READY"
}
```


## PCAP Detail

PCAP object details.

```/api/pcap/v1/{id}/```  

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td>id</td>
<td>String</td>
<td>Yes</td>
<td>Upload ID</td>
</tr>
</table>


### Sample response body

```json
{
    "id": "3dbcaa40-cd9b-4fdf-87ec-8cf226e582ff",
    "status": "READY",
    "is_private": false,
    "created": "2015-10-07T21:47:51.224781Z",
    "alerts": "http://www.threatlab.io/api/pcap/v1/3dbcaa40-cd9b-4fdf-87ec-8cf226e582ff/alerts",
    "errors": "http://www.threatlab.io/api/pcap/v1/3dbcaa40-cd9b-4fdf-87ec-8cf226e582ff/errors"
}
```


## PCAP Alerts

IDS alerts generated during analysis.

```/api/pcap/v1/{id}/alerts/```  

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td>id</td>
<td>String</td>
<td>Yes</td>
<td>Upload ID</td>
</tr>
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

```/api/pcap/v1/{id}/errors/```    

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td>id</td>
<td>String</td>
<td>Yes</td>
<td>Upload ID</td>
</tr>
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
