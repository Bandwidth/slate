## Go Library

A go client library for the [Bandwidth Application Platform](http://bandwidth.com/products/application-platform?utm_medium=social&utm_source=github&utm_campaign=dtolb&utm_content=_)

[![github](images/github_logo.png)](https://github.com/bandwidthcom/go-bandwidth)

### Installing the SDK

	// Add to code
	import "github.com/bandwidthcom/go-bandwidth"

### Supported Versions
`go-bandwidth should work on Go 1.6+.

| Version                           | Support Level |
|:----------------------------------|:--------------|
| <1.6                              | Unsupported   |
| 1.6                               | Supported     |
| 1.7                               | Supported     |


### Client initialization

All interaction with the API is done through a type `Client`. The function `bandwidth.new` takes next parameters:

| Argument    | Description           | Default value                       | Required |
|:------------|:----------------------|:------------------------------------|:---------|
| `UserID`    | Your user ID          | none                                | Yes      |
| `APIToken`  | Your API token        | none                                | Yes      |
| `APISecret` | Your API secret       | none                                | Yes      |
| `APIVersion`   | The Bandwidth API version | `v1` | No       |
| `APIEndPoint`   | The Bandwidth API URL | `https://api.catapult.inetwork.com` | No       |

To initialize the `Client` instance, provide your API credentials which can be found on your account page in [the portal](https://catapult.inetwork.com/pages/catapult.jsf).

```go
client := bandwidth.New("userId", "apiToken", "apiSecret")
```

Your `client` object is now ready to use the API.


### Send a SMS

```go
messageId, _ := client.CreateMessage(&bandwidth.CreateMessageData{From: "+19195551212", To: "+191955512142", Text:"Test"})
```

### Make a call

```go
callId, _ := client.CreateCall(&bandwidth.CreateCallData{From: "+19195551212",  To: "+191955512142"})
```
### Providing feedback

For current discussions please see the [Issues section on GitHub](https://github.com/bandwidthcom/go-bandwidth/issues). To start a new topic,  please open an issue. Your feedback is greatly appreciated!
