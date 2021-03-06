Change Log
==========

## Version 1.5.0

_2014-03-07_


##### OkHttp no longer uses the default SSL context.

Applications that want to use the global SSL context with OkHttp should configure their
OkHttpClient instances with the following:

```java
okHttpClient.setSslSocketFactory(HttpsURLConnection.getDefaultSSLSocketFactory());
```

A simpler solution is to avoid the shared default SSL socket factory. Instead, if you
need to customize SSL, do so for your specific OkHttpClient instance only.

##### Synthetic headers have changed

Previously OkHttp added a synthetic response header, `OkHttp-Selected-Transport`. It
has been replaced with a new synthetic header, `OkHttp-Selected-Protocol`.

##### Changes

 * New: Support for `HTTP-draft-09/2.0`.
 * New: Support for `spdy/3.1`. Dropped support for `spdy/3`.
 * New: Use ALPN on Android platforms that support it (4.4+)
 * New: CacheControl model and parser.
 * New: Protocol selection in MockWebServer.
 * Fix: Route selection shouldn't use TLS modes that we know will fail.
 * Fix: Cache SPDY responses even if the response body is closed prematurely.
 * Fix: Use strict timeouts when aborting a download.
 * Fix: Support Shoutcast HTTP responses like `ICY 200 OK`.
 * Fix: Don't unzip if there isn't a response body.
 * Fix: Don't leak gzip streams on redirects.
 * Fix: Don't do DNS lookups on invalid hosts.
 * Fix: Exhaust the underlying stream when reading gzip streams.
 * Fix: Support the `PATCH` method.
 * Fix: Support request bodies on `DELETE` method.
 * Fix: Drop the `okhttp-protocols` module.
 * Internal: Replaced internal byte array buffers with pooled buffers ("OkBuffer").


## Version 1.3.0

_2014-01-11_

 * New: Support for "PATCH" HTTP method in client and MockWebServer.
 * Fix: Drop `Content-Length` header when redirected from POST to GET.
 * Fix: Correctly read cached header entries with malformed header names.
 * Fix: Do not directly support any authentication schemes other than "Basic".
 * Fix: Respect read timeouts on recycled connections.
 * Fix: Transmit multiple cookie values as a single header with delimiter.
 * Fix: Ensure `null` is never returned from a connection's `getHeaderFields()`.
 * Fix: Persist proper `Content-Encoding` header to cache for GZip responses.
 * Fix: Eliminate rare race condition in SPDY streams that would prevent connection reuse.
 * Fix: Change HTTP date formats to UTC to conform to RFC2616 section 3.3.
 * Fix: Support SPDY header blocks with trailing bytes.
 * Fix: Allow `;` as separator for `Cache-Control` header.
 * Fix: Correct bug where HTTPS POST requests were always automatically buffered.
 * Fix: Honor read timeout when parsing SPDY headers.


## Version 1.2.1

_2013-08-23_

 * Resolve issue with 'jar-with-dependencies' artifact creation.
 * Fix: Support empty SPDY header values.


## Version 1.2.0

_2013-08-11_

 *  New APIs on OkHttpClient to set default timeouts for connect and read.
 *  Fix bug when caching SPDY responses.
 *  Fix a bug with SPDY plus half-closed streams. (thanks kwuollett)
 *  Fix a bug in `Content-Length` reporting for gzipped streams in the Apache
    HTTP client adapter. (thanks kwuollett)
 *  Work around the Alcatel `getByInetAddress` bug (thanks k.kocel)
 *  Be more aggressive about testing pooled sockets before reuse. (thanks
    warpspin)
 *  Include `Content-Type` and `Content-Encoding` in the Apache HTTP client
    adapter. (thanks kwuollett)
 *  Add a media type class to OkHttp.
 *  Change custom header prefix:

    ```
    X-Android-Sent-Millis is now OkHttp-Sent-Millis
    X-Android-Received-Millis is now OkHttp-Received-Millis
    X-Android-Response-Source is now OkHttp-Response-Source
    X-Android-Selected-Transport is now OkHttp-Selected-Transport
    ```
 *  Improve cache invalidation for POST-like requests.
 *  Bring MockWebServer into OkHttp and teach it SPDY.


## Version 1.1.1

_2013-06-23_

 * Fix: ClassCastException when caching responses that were redirected from
   HTTP to HTTPS.


## Version 1.1.0

_2013-06-15_

 * Fix: Connection reuse was broken for most HTTPS connections due to a bug in
   the way the hostname verifier was selected.
 * Fix: Locking bug in SpdyConnection.
 * Fix: Ignore null header values (for compatibility with HttpURLConnection).
 * Add URLStreamHandlerFactory support so that `URL.openConnection()` uses
   OkHttp.
 * Expose the transport ("http/1.1", "spdy/3", etc.) via magic request headers.
   Use `X-Android-Transports` to write the preferred transports and
   `X-Android-Selected-Transport` to read the negotiated transport.


## Version 1.0.2

_2013-05-11_

 * Fix: Remove use of Java 6-only APIs.
 * Fix: Properly handle exceptions from `NetworkInterface` when querying MTU.
 * Fix: Ensure MTU has a reasonable default and upper-bound.


## Version 1.0.1

_2013-05-06_

 * Correct casing of SSL in method names (`getSslSocketFactory`/`setSslSocketFactory`).


## Version 1.0.0

_2013-05-06_

Initial release.

