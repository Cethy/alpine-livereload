Alpine-livereload
===

Simple docker image based on alpine3.6 with [livereload](https://github.com/napcs/node-livereload) installed.

| **ENTRYPOINT** | **CMD** |
|:---:|:---:|
| `node bin/livereload.js` | `/usr/src/livereload-watch -u true -d` |

## Requirements
In the current implementation, you will need the [livereload extension](http://livereload.com/extensions/) for your web browser.

## How to use
Since this image is designed to watch changes in a directory, you need to share it as a volume.


### `docker run`

    docker run -v $PWD/your/watch/directory:/usr/src/livereload-watch cethy/alpine-livereload:v1.0

**Note :** `docker run` only works for local directory, use docker-compose for other directories (see below).

### `docker-compose`

    version: '2'

    services:
      livereload:
        image: cethy/alpine-livereload:v1.0
        ports:
          - "35729:35729"
        volumes:
          - /your/watch/directory:/usr/src/livereload-watch

## Configuration

It's possible to override the `command` to [change the livereload options](https://github.com/napcs/node-livereload#command-line-options) :

    docker run -v $PWD/your/watch/directory:/usr/src/livereload-watch \
    	cethy/alpine-livereload:v1.0 \
    	/usr/src/livereload-watch -u true -d --exts 'css,js,html'

or

    services:
      livereload:
        # ...
        command: "/usr/src/livereload-watch -u true -d --exts 'css,js,html'"


## Original work
[docker-livereload](https://github.com/franckdelage/docker-livereload)
