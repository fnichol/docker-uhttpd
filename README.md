# docker-uhttpd

A [Docker][docker] micro image for [uhttpd][uhttp], a tiny, lightweight web server. The image is built using [progrium/busybox][progrium_busybox] to keep the footprint as small as possible. If you need a quick and small static HTTP server, give this one a go!

## Getting the Image

This image is hosted on the Docker index as a trusted build and can be pulled down with:

		docker pull fnichol/uhttpd

## Usage

To run a simple detached container:

		docker run -d -p 80 fnichol/uhttpd

If you want to serve the contents of the current directory in the container (warning, the directory will be local to the system running the `docker` daemon):

		docker run -d -p 80 -v `pwd`:/www fnichol/uhttpd

Alternatively, you can use the [data container pattern](http://docs.docker.io/use/working_with_volumes/) by creating a "data" container and mounting its volumes into the web server container. Let's use named containers to make this easier:

		docker run -v /www --name www_data busybox true
		docker run -d -p 80 --volumes-from www_data --name www fnichol/uhttpd

For fun, we'll run a container just to create an index file:

		docker run --rm --volumes-from www_data busybox \
			/bin/sh -c 'echo "<h1>Hey there</h1>" > /www/index.html'

## Development

* Source host at [GitHub][repo]
* Report issues/questions/feature requests on [GitHub Issues][issues]

Pull requests are very welcome! Make sure your patches are well tested. Ideally create a topic branch for every separate change you make. For example:

1. Fork the repo
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add support for feature'`)
4. Push to the branch (`git push origin my-new-feature`)

## Authors

Created and maintained by [Fletcher Nichol][fnichol] (<fnichol@nichol.ca>).

## License

MIT (see [License.txt][license])

[fnichol]:  https://github.com/fnichol
[repo]:     https://github.com/fnichol/docker-uhttpd
[issues]:   https://github.com/fnichol/docker-uhttpd/issues
[license]:  https://github.com/fnichol/docker-uhttpd/blob/master/License.txt

[docker]:           https://www.docker.io/
[progrium_busybox]: https://github.com/progrium/busybox
[uhttpd]:           http://wiki.openwrt.org/doc/howto/http.uhttpd
