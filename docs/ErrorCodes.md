ErrorCodes
=========

## HTTP Return Codes

###  Code detail
	* HTTP `4XX` return codes are used for malformed requests;the issue is on the sender's side.
	* HTTP `401` return code is used when signature parameters are missing or signature verification fails.
	* HTTP `403` return code is used when there is no relevant permission to request the interface.
	* HTTP `412` return code is used when some required parameters are missing.
	* HTTP `429` return code is used when breaking a request rate limit.
	* HTTP `5XX` return codes are used for internal errors; the issue is on  DFX's side. It is important to **NOT** treat this as a failure operation; the execution status is **UNKNOWN** and could have been a success.


## Error Codes

### Any endpoint can return an ERROR,Sample Payload below:

#### code=401

``` java
{
		"code": "401",
	"msg": "public-key has not been uploaded or has expired"
}
```

``` java
{
		"code": "403",
	"msg": "Insufficient permissions or IP is not in the whitelist"
}
```


``` java
{
		"code": "412",
	"msg": "The request header is missing `EXCHANGE-API-SIGN` parameters"
}
```


``` java
{
	"code": "500",
	"msg": "Server internal exception"
}
```
