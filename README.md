# HTTP Request Parser
A http request parser for parsing url, search query, headers and form data.

## Usage
- Import Module
```
    import HttpParser "mo:HttpParser";
```
- Parse incoming http request
-  ex:  retrieving the `name` field from the url query
```motoko
    public query func http_request(rawReq: HttpParser.HttpRequest) : async HttpParser.HttpResponse {
        let req = HttpParser.parse(rawReq);

        let name = switch(req.url.queryObj.get("name")){
            case (?name) name;
            case (_) "";
        };

        let result = "<html><head><title> http_request </title></head><body><h1> Hello, " # name # "! </h1></body></html>";

        {
            status_code = 200;
            headers = [("Content-Type", "text/html")];
            body = Text.encodeUtf8 (result);
        }
    };
```

Check out the data types [documentation](./docs.md) for supported fields and methods