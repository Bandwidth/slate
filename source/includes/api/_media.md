# Media
The Media resource lets you upload your media files to Bandwidth API servers so they can be used in applications without requiring a separate hosting provider. You can upload files up to `65MB` and file storage is free for an unlimited number of files. Files you upload can only be accessed by you when you supply your API access `token` and `secret`. They are not available to anonymous users. Bandwidth API supports the `Cache-Control` header when you upload files.

<aside class="notice">
You can upload files up to `65MB` and file storage is free for an unlimited number of files.
</aside>

## GET media
Gets a list of your media files. No query parameters are supported.

### Example: List Your Media Files


```shell
curl -v -X GET https://api.catapult.inetwork.com/v1/users/{userId}/media \
	-u {token}:{secret} \
	-H "Content-type: application/json"
```

```js
client.Media.list()
then(function (media) {
  console.log(media);
});
```

```csharp
var list = client.Media.List();
Console.WriteLine(list.First().MediaName);
// {mediaName}
```

```ruby
list = Media.list(client)
```

```go
list, _ := client.GetMediaFiles()
```


> The above command returns JSON structured like this:

```json
[
  {
    "contentLength": 561276,
    "mediaName": "{mediaName1}",
    "content": "api.catapult.inetwork.com/.../media/{mediaName1}"
  },
  {
    "contentLength": 2703360,
    "mediaName": "{mediaName2}",
    "content": "https://api.catapult.inetwork.com/.../media/{mediaName2}"
  },
  {
    "contentLength": 2257901,
    "mediaName": "{mediaName3}",
        "content": "https://api.catapult.inetwork.com/.../media/{mediaName3}"
  }
]
```

## PUT media/{mediaName}
Uploads a file the normal HTTP way. You may add headers to the request in order to provide some control to your media-file.

| Header         | Description                                                                                                                        | Mandatory |
|:---------------|:-----------------------------------------------------------------------------------------------------------------------------------|:----------|
| Content-Length | Indicates the size of the entity-body.                                                                                             | Yes       |
| Cache-Control  | General-header field is used to specify directives that MUST be obeyed by all caching mechanisms along the request/response chain. | No        |
| Content-Type   | The media type of the entity-body.                                                                                                 | No        |

### Example: Upload an MP3 File

```csharp
await client.Media.UploadAsync(new UploadMediaData{
		MediaName = "file.mp3",
		Path = "/path/to/file.mp3",
		ContentType = "audio/mp3"
	}
);
```

```ruby
Media.upload(client, "file.mp3", File.open("/path/to/file.mp3"), "audio/mp3")
```

```go
client.UploadMediaFile("file.mp3", "/path/to/file.mp3", "audio/mp3")
```

## GET media/{mediaName}
Downloads a media file you previously uploaded.

### Example: Download an MP3 File

```csharp
using(var data = await client.Media.DownloadAsync("file.mp3"))
{
  var fileContent = await data.ReadAsStreamAsync();
  // fileContent is stream object
}
```

```ruby
content, media_type = Media.download(client, "file.mp3")
```

```go
stream, contentType, _ := client.DownloadMediaFile("file.mp3")
```


## DELETE media/{mediaName}
Deletes a media file from Bandwidth API server. Make sure you don't have any application scripts still using the media before you delete. If you accidentally delete a media file, you can immediately upload a new file with the same name.

### Example: Delete an MP3 File

```csharp
await client.Media.DeleteAsync("file.mp3");
```

```ruby
Media.delete(client, "file.mp3")
```

```go
client.DeleteMediaFile("file.mp3")
```
