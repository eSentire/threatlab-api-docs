# Client Libraries

## Python

### slumber

Slumber is a python library that provides a convenient yet powerful object orientated interface to ReSTful APIs. It acts as a wrapper around the excellent requests library and abstracts away the handling of urls, serialization, and processing requests.

Source: [https://github.com/samgiles/slumber](https://github.com/samgiles/slumber)

Usage example:

```python
>>> import slumber
>>> ## Connect to http://www.threatlab.io/api/pcap/v1/ with no authentication
>>> api = slumber.API("http://www.threatlab.io/api/pcap/v1/")
>>> ## GET http://www.threatlab.io/api/pcap/v1/pcap/f7c14dc9-100d-4a01-8c9e-fe7e40b7c548
>>> api.pcap('f7c14dc9-100d-4a01-8c9e-fe7e40b7c548').get()
>>> ## GET http://www.threatlab.io/api/pcap/v1/pcap/f7c14dc9-100d-4a01-8c9e-fe7e40b7c548/alerts
>>> api.pcap('f7c14dc9-100d-4a01-8c9e-fe7e40b7c548').alerts().get()
```