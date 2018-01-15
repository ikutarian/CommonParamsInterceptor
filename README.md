# CommonParamsInterceptor

Add common parameters when serve http through okhttp.
You can add common parameters to

* Header
* HTTP GET's url as query parameter
* HTTP POST's body

when you serve internet through [OkHttp](https://github.com/square/okhttp)

## How to use?

`CommonParamsInterceptor` expose 3 mothods:

* `Map<String, String> getHeaderMap()`
* `Map<String, String> getQueryParamMap()`
* `Map<String, String> getFormBodyParamMap()`

you can add common parameters like this below code

```Java
private RxRequestHelper(Interceptor commonParamsInterceptor) {
    OkHttpClient.Builder clientBuilder = new OkHttpClient.Builder();

    if (commonParamsInterceptor != null) {
        clientBuilder.addInterceptor(new CommonParamsInterceptor() {
            @Override
            public Map<String, String> getHeaderMap() {  // Header
                Map<String, String> headersMap =  new HashMap<>();
                headersMap.put("v", "1.0");
                return headersMap;
            }

            @Override
            public Map<String, String> getQueryParamMap() { // URL Query
                Map<String, String> queryParamMap =  new HashMap<>();
                queryParamMap.put("v", "1.0");
                return queryParamMap;
            }

            @Override
            public Map<String, String> getFormBodyParamMap() { // POST body
                Map<String, String> formBodyParamMap =  new HashMap<>();
                formBodyParamMap.put("v", "1.0");
                return formBodyParamMap;
            }
        });
    }

    sRetrofit = new Retrofit.Builder()
            .baseUrl(BuildConfig.BASE_SERVER_URL)
            .addConverterFactory(GsonConverterFactory.create())
            .addCallAdapterFactory(RxJavaCallAdapterFactory.create())
            .client(clientBuilder.build())
            .build();
}
```

## License

```
        DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE
                    Version 2, December 2004

 Copyright (C) 2004 Sam Hocevar <sam@hocevar.net>

 Everyone is permitted to copy and distribute verbatim or modified
 copies of this license document, and changing it is allowed as long
 as the name is changed.

            DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

  0. You just DO WHAT THE FUCK YOU WANT TO.
  ```
