# My slides
[![Docker](https://quay.io/repository/orggue/talks/status "Docker")](https://quay.io/repository/orggue/talks)
[![Godoc](https://img.shields.io/badge/documentation-present-blue.svg)](https://godoc.org/golang.org/x/tools/present)
[![JavaScriptdoc](https://img.shields.io/badge/documentation-reveal.js-yellow.svg)](https://github.com/hakimel/reveal.js)

## Install & Run
### If the slide is *.slide
#### Local
```zsh
$ go get golang.org/x/tools/cmd/present
$ present -base present -notes
```
#### Docker
```zsh
$ docker build \
-t jorge-go-slides \
-f Dockerfile-go .

$ docker run -d \
-v ${PWD}/2018:/slides/2018 \
-v ${PWD}/present:/slides/present \
-v .${PWD}/common:/slides/common \
-p 3999:3999 \
--name go-slides \
jorge-go-slides

# or

$ docker-compose up -d go
```
### If the slide is *.html
#### Local
Follow the instructions you will find in the ![reveal.js documentation](https://github.com/hakimel/reveal.js).
#### Docker
```zsh
$ docker build \
-t jorge-js-slides \
-f Dockerfile-js .

$ docker run -d \
-v ${PWD}/2018:/slides/2018 \
-v ${PWD}/reveal/css:/slides/css \
-v .${PWD}/common:/slides/common \
-p 8000:8000 \
--name js-slides \
jorge-js-slides

# or

$ docker-compose up -d js

# or

$ docker pull quay.io/orggue/talks

$ docker run -p 8000:8000 quay.io/orggue/talks -d
```
## Variables
If you are running it with docker-compose, which I recommend, you can set the
variables in the .env file.
```zsh
# Common variables
COMMONDIR=common

# *.slides variables
PRESENT=present
GOPORT=3999

# *.html variables
REVEALCSS=reveal/css
JSPORT=8000
```
## Notes
If the file starts with *note-*, It is just a note not a slide.
