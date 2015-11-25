# Client Libraries

## Python

### slumber

[Slumber](https://github.com/samgiles/slumber) is a python library that provides a convenient yet powerful object orientated interface to ReSTful APIs. It acts as a wrapper around the excellent requests library and abstracts away the handling of urls, serialization, and processing requests.

Installation:

```bash
pip install slumber
```

Usage example:

```python
>>> import slumber
>>> ## Connect to http://www.threatlab.io/api/pcap/v1/ with no authentication
>>> api = slumber.API("http://www.threatlab.io/api/pcap/v1/")
>>> ## Upload file for analysis
>>> api.upload.put(files={'file': open('sample.pcap', 'r')})
>>> ## GET http://www.threatlab.io/api/pcap/v1/pcap/detail/f7c14dc9-100d-4a01-8c9e-fe7e40b7c548
>>> api.detail('f7c14dc9-100d-4a01-8c9e-fe7e40b7c548').get()
>>> ## GET http://www.threatlab.io/api/pcap/v1/pcap/alerts/f7c14dc9-100d-4a01-8c9e-fe7e40b7c548
>>> api.alerts('f7c14dc9-100d-4a01-8c9e-fe7e40b7c548').get()
```