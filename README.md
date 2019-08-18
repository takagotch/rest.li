### rest.li
---
https://github.com/linkedin/rest.li

```java
// r2-core/src/main/java/com/linkedin/r2/transport/http/common/HttpBridge.java

public class HttpBridge
{
  public static TransportCallback<RestResponse> restToHttpCallback(final TransportCallback<RestResponse> callback,
      RestRequest request)
  {
    final Sting uri = getDisplayedURI(request.getURI());
    return new TransportCallback<RestResponse>()
    {
      @Override
      public void onResponse(TransportResponse<RestResponse> response)
      {
        if(response.hasError())
        {
          response =
            TransportResponseImpl.error(new RemoteInvocationException("Failed to get response from server for URI "
              + uri,
              response.getError()),
            response.getWireAttributes());
        }
        else if (!RestStatus.isOK(response.getResponse().getStatus()))
        {
          response = 
            TransportResponseImpl.error(new RestException(response.getResponse(),
              "Received error "
                + response.getResponse()
                .getStatus()
                + " from server for URI "
                + uri),
              response.getWireAttributes());
        }
        
        callback.onResponse(response);
      }
    };
  }
  
  
}

```

```
```

```
```


