# My slides
[![Godoc](https://img.shields.io/badge/present-documentation-blue.svg)](https://godoc.org/golang.org/x/tools/present)
[![Godoc](https://img.shields.io/badge/present-documentation2-blue.svg)](https://godoc.org/golang.org/x/tools/cmd/present)
[![JavaScriptdoc](https://img.shields.io/badge/reveal.js-documentation-yellow.svg)](https://github.com/hakimel/reveal.js)

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
-v ${PWD}/2017:/slides/2017 \
-v ${PWD}/present:/slides/present \
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
-v ${PWD}/2017:/slides/2017 \
-v ${PWD}/reveal/css:/slides/css \
-p 8000:8000 \
--name js-slides \
jorge-js-slides

# or

$ docker-compose up -d js
```
## Variables
If you are running it with docker-compose, which I recommend, you can set the
variables in the .env file.
```zsh
# Common variables
FOLDER=2018

# *.slides variables
PRESENT=present
GOPORT=3999

# *.html variables
REVEALCSS=reveal/css
JSPORT=8000
```
