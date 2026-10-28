# curl-impersonate-links

Builds of [libcurl-impersonate](https://github.com/lexiforest/curl-impersonate) with Chrome's HTTP/2 stream
dependencies ("links") added back.

Chrome links each HTTP/2 stream it opens beside others to the newest open stream of the same priority, or else the
nearest higher one, and to 0 when none is open. Upstream sends 0 on every stream. Each release here is upstream's
source at one tag plus one small patch (`links.patch`, attached to the release), built with upstream's own
`Makefile` and CMake for:

- `x86_64-linux-gnu` (glibc 2.17 or newer)
- `arm64-macos`

A call asks for the links by setting `CURLOPT_STREAM_DEPENDS_E` to any handle. That option has been a no-op since
curl 8.21. A call that doesn't ask sends exactly what upstream's library sends.

Releases are named `<upstream tag>-links.<n>`, for example `v2.3.1-links.1`. Each one carries `SHA256SUMS`.

This repository holds only the release builds, the patch and the licenses. It is built and published by an
automated job elsewhere; issues and pull requests are not watched.

## Licenses

curl-impersonate is MIT licensed (`LICENSE`). Each release tarball includes, in `licenses/`, the license of every
component it bundles: curl, BoringSSL, nghttp2, nghttp3, ngtcp2, brotli, zlib, zstd and c-ares, collected as
upstream's own release does. `links.patch` is a patch to curl and is offered under curl's license.
