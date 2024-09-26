OpenApi Key
=============


**What are 'Public Key' and 'Api Key'**

Public key is your local public key generated using the ed25519 algorithm. The private key is kept by you. DFX will never ask you for the private key at any time. Api key is the identity assigned to you after you upload the public key to dfx.

You can create an API-KEY for your own account, or you can create a unique API-KEY for each sub-user. If you need to replace an API-KEY, you must first delete the old one before creating a new one.

**1. How do you generate public and private keys? If you have any questions about generating private and public keys, you can refer to the specific steps at the bottom of the article in detail. [please refer Here.](https://github.com/dfxlabs/dfxlabs.github.io/blob/main/docs/Open%20Api.md#generating-ed25519-public-and-private-keys-using-command-line-on-windows-and-mac)**

To generate an Ed25519 key pair in the command line and convert the private key to a Base64 encoded string, you can use the OpenSSL tool.
Here's a way to generate an Ed25519 public and private key in the MacOS command line and convert it to a Base64-encoded string:


* 1.Generate private key + output content to console:

	```javascript
	openssl genpkey -algorithm ed25519 -out private_key.pem
	cat private_key.pem
    ```

	```javascript
	If you are prompted "Algorithm ed25519 not found" after executing the command,
	this error may be because your OpenSSL version does not support the Ed25519 algorithm.
	Ed25519 is a relatively new encryption algorithm that requires OpenSSL version 1.1.1
	or above to support it.
	Please make sure your version of OpenSSL meets the requirements. If not, you can try to
	upgrade OpenSSL or use other tools that support the Ed25519 algorithm.
    ```
* 2.You will get the following content:

	```javascript
	MC4CAQAwBQYDK2VwBCIEIE3cC2U0982hn5lbePlFjfaxLKSxSdkwzIr1H4dCBN6V
	```

* 3.Generate the public key + output the content to the console:
	```javascript
	openssl pkey -in private_key.pem -pubout -out public_key.pem
	cat public_key.pem
	```
* 4.You will get the following content:

	```javascript
	MCowBQYDK2VwAyEAjUsfgTzAktJvlhsz43RyWho+7NEK6u6+qJUIFlEWTWA=
	```




### Api Key permission

| Url | Method | What roles can access |Describe|
| --- | --- | --- |--- |
|/api/v1/spot/depth| GET| ALL|
|/api/v1/symbols| GET| ALL|
|/api/v1/spot/trade| GET| ALL|
|/api/v1/spot/kline| GET| ALL|
|/api/v1/spot/ticker/24hr| GET| ALL|
|/api/v1/spot/ticker/price| GET| ALL|
|/api/v1/spot/ticker/book_ticker| GET| ALL|
|/ws/**| GET| ALL| Websocket|
|/api/v1/user/info| GET| Administrator、Trader|
|/api/v1/account/balance| GET| Administrator、Trader|
|/api/v1/account/trades| GET| Administrator、Trader|Check account transaction｜
|/api/v1/spot/test/order| POST| Administrator、Trader|Test whether the order can be created｜
|/api/v1/spot/order| POST| Administrator、Trader|Create order|
|/api/v1/spot/order| DELETE| Administrator、Trader|Cancel order|
|/api/v1/spot/batch/order| DELETE| Administrator、Trader|Batch cancel order|
|/api/v1/spot/order| GET| Administrator、Trader|Search order|
|/api/v1/spot/open_order| GET| Administrator、Trader|Get pending orders|
|/api/v1/spot/finish_order| GET| Administrator、Trader|Get completed orders|


### Rate Limit

<table>
    <tr>
        <td>Endpoint</td>
        <td>Rate limit rule</td>
        <td>API Request</td>
				<td>Description</td>
				<td>Rate limit</td>
    </tr>
    <tr>
        <td rowspan=7 colspan=1>Market Data</td>
        <td rowspan=7 colspan=1>IP+API Request</td>
				<td rowspan=1 colspan=1>GET /api/v1/spot/depth</td>
				<td rowspan=1 colspan=1>Get Depth information</td>
				<td rowspan=1 colspan=1>1 every 2 second</td>
    </tr>
    <tr>
				<td rowspan=1 colspan=1>GET /api/v1/spot/trade</td>
				<td rowspan=1 colspan=1>Get Recent Transaction Records information</td>
				<td rowspan=1 colspan=1>1 every 2 second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/spot/kline</td>
			<td rowspan=1 colspan=1>Get Kline information</td>
			<td rowspan=1 colspan=1>1 every 2 second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/spot/ticker/24hr</td>
			<td rowspan=1 colspan=1>Get Quotes in the last 24 hours information</td>
			<td rowspan=1 colspan=1>1 every 2 second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/spot/ticker/price</td>
			<td rowspan=1 colspan=1>Get Latest price information</td>
			<td rowspan=1 colspan=1>1 every 2 second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/spot/ticker/book_ticker</td>
			<td rowspan=1 colspan=1>Get Symbol Order Top Of Book information</td>
			<td rowspan=1 colspan=1>1 every 2 second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/symbols</td>
			<td rowspan=1 colspan=1>Get Symbol Basic information</td>
			<td rowspan=1 colspan=1>1 every 2 second</td>
    </tr>
    <tr>
      <td rowspan=6 colspan=1>Order</td>
      <td rowspan=6 colspan=1>API KEY+API Request</td>
			<td rowspan=1 colspan=1>POST /api/v1/spot/order</td>
			<td rowspan=1 colspan=1>Create  Order</td>
			<td rowspan=1 colspan=1>10 per second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>DELETE /api/v1/spot/order</td>
			<td rowspan=1 colspan=1>Cancel a single order</td>
			<td rowspan=1 colspan=1>10 per second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>DELETE /api/v1/spot/batch/order</td>
			<td rowspan=1 colspan=1>Batch Cancel Order</td>
			<td rowspan=1 colspan=1>1 per second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/spot/order</td>
			<td rowspan=1 colspan=1>Get User Order List</td>
			<td rowspan=1 colspan=1>1 per second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/spot/finish_order</td>
			<td rowspan=1 colspan=1>Get completed orders information</td>
			<td rowspan=1 colspan=1>1 per second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/spot/open_order</td>
			<td rowspan=1 colspan=1>Query unfinished orders information</td>
			<td rowspan=1 colspan=1>1 per second</td>
    </tr>
    <tr>
      <td rowspan=3 colspan=1>Account</td>
      <td rowspan=3 colspan=1>API KEY+API Request</td>
			<td rowspan=1 colspan=1>GET /api/v1/user/info</td>
			<td rowspan=1 colspan=1>Get User information</td>
			<td rowspan=1 colspan=1>1 per second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/account/balance</td>
			<td rowspan=1 colspan=1>Get Account Balance information</td>
			<td rowspan=1 colspan=1>1 per second</td>
    </tr>
    <tr>
			<td rowspan=1 colspan=1>GET /api/v1/account/trades</td>
			<td rowspan=1 colspan=1>Get Account Trade List information</td>
			<td rowspan=1 colspan=1>1 per second</td>
    </tr>
</table>



#### Upload the Public Key to DFX

  Congratulations, you have completed most of the steps and victory lies ahead. Next, you need to upload the ciphertext of the generated public key to the DFX API. The specific steps are as follows:

### step 1
![Image title](https://dfx-test-public.s3.ap-east-1.amazonaws.com/image/step-1.png)

### step 2
![Image title](https://dfx-test-public.s3.ap-east-1.amazonaws.com/image/step-2.png)

### step 3
![Image title](https://dfx-test-public.s3.ap-east-1.amazonaws.com/image/step-3.png)

### step 4
![Image title](https://dfx-test-public.s3.ap-east-1.amazonaws.com/image/step-4.png)


* Note
```
Once the client uploads the ED25519 public key, the DFX platform will generate a 96-character string as the
unique identifier for the ED25519 key pair. The client needs to click the "View" button next to the newly
created API key. After authentication, this string will be displayed on the screen. The client needs to
download it and paste it into the EXCHANGE-API-KEY field in the header of each RESTful request.
```
```
Please note that the selection of API key permission types is only applicable to institutional clients and
is currently not available for individual clients.
```

#### Use ‘Api-Key’ as ‘EXCHANGE-API-KEY’ in the request header

#### Example: Add EXCHANGE-API-KEY to Headers

``` java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class HttpGetExample {
	public static void main(String[] args) throws IOException {
		String url = "https://$HOST/api/v1/symbols?clientType=OP";
		HttpURLConnection connection = (HttpURLConnection) new URL(url).openConnection();
		connection.setRequestMethod("GET");

		// Set request header
		connection.setRequestProperty("EXCHANGE-API-KEY", "YOUR API-KEY");
		connection.setRequestProperty("EXCHANGE-API-TIMESTAMP", "1711351755000");
		connection.setRequestProperty("EXCHANGE-API-SIGN", signResult);


		int responseCode = connection.getResponseCode();
		System.out.println("Response Code: " + responseCode);

		BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
		StringBuilder response = new StringBuilder();
		String line;
		while ((line = reader.readLine()) != null) {
			response.append(line);
		}
		reader.close();

		System.out.println("Response Body: " + response.toString());

		connection.disconnect();
	}
}
```


# Generating ed25519 Public and Private Keys Using Command Line on Windows and Mac

You can generate ed25519 public and private keys using the command line on Windows and Mac through OpenSSL or ssh-keygen. Below are the detailed steps:

## Using ssh-keygen to Generate ed25519 Key Pair

### On Windows (requires Git Bash or Windows Subsystem for Linux)

1. **Install Git Bash:**
   - If you don't have Git Bash installed, download and install it from the [Git website](https://git-scm.com/downloads).

2. **Open Git Bash:**
   - Find and open Git Bash from the Start menu.

3. **Generate ed25519 Key Pair:**
	```sh
	ssh-keygen -t ed25519 -C "your_email@example.com"

	`-t ed25519` specifies the key type as ed25519.
	`-C "your_email@example.com"` is a comment to identify the key.
	```

4. **Follow the Prompts:**
   -  When prompted to enter the file in which to save the key, press Enter to save it to the default path (usually ~/.ssh/id_ed25519).
   - When prompted to enter a passphrase, you can set one or press Enter to skip.
## On Mac
1. Open Terminal:
   - Use Spotlight to search for and open Terminal, or find it in Applications.
2. Generate ed25519 Key Pair:
    ```sh
	ssh-keygen -t ed25519 -C "your_email@example.com"
    ```
    - The steps are the same as those for using Git Bash on Windows.
Using OpenSSL to Generate ed25519 Key Pair


## On Windows (requires OpenSSL installation)
1. Install OpenSSL:
    - Download and install OpenSSL for Windows from Shining Light Productions.
2. Open Command Prompt or PowerShell:
    - Press the Windows key, search for cmd or PowerShell, and open it.

3. Generate ed25519 Key Pair:

	```sh
	openssl genpkey -algorithm ed25519 -out private_key.pem
	openssl pkey -in private_key.pem -pubout -out public_key.pem
    ```

	- private_key.pem is the generated private key file.
	- public_key.pem is the generated public key file.


## On Mac (usually comes with OpenSSL pre-installed)
1. Open Terminal:
    - Use Spotlight to search for and open Terminal, or find it in Applications.
2. Generate ed25519 Key Pair:
```sh
openssl genpkey -algorithm ed25519 -out private_key.pem
openssl pkey -in private_key.pem -pubout -out public_key.pem
```

   - The steps are the same as those for using OpenSSL on Windows.

## Summary
   - Whether on Windows or Mac, you can use ssh-keygen or OpenSSL to generate ed25519 public and private keys. ssh-keygen is simpler and more straightforward, suitable for most users, while OpenSSL offers more flexibility and options for those needing a customized key generation process.
