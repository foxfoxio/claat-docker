# foxfoxio/claat docker image

A docker image for claat [Codelabs command line tool](https://github.com/googlecodelabs/tools/tree/master/claat), see for [usage](https://github.com/googlecodelabs/tools/blob/master/README.md)

## pull

```bash
docker pull foxfoxio/claat:latest
```

## run

### help command

view all available options

  ```bash
  docker run --rm foxfoxio/claat -h
  ```

### export command

export codelab document from one or more source files, see [FORMAT-GUIDE.md](https://github.com/googlecodelabs/tools/blob/master/FORMAT-GUIDE.md)

- __markdown format:__ create a codelab file in markdown format and run this command

  ```bash
  docker run --rm -v $(pwd):/app foxfoxio/claat export codelab-file.md
  ```

  - note: `claat` may show the following error if it cannot download the markdown file does not exist, as it tries to download the file as `google-doc-id`

    ```bash
    ➜ docker run --rm -v $(pwd):/app foxfoxio/claat export codelab-file.md
    err     codelab-file.md unable to obtain access token for "goog"
    Authorize me at following URL, please:

    https://accounts.google.com/o/oauth2/auth?access_type=offline&client_id=183908478743-e8rth9fbo7juk9eeivgp23asnt791g63.apps.googleusercontent.com&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive.readonly&state=unused

    Code: %
    ```

- __google doc:__ provide google doc id in the export command

  ```bash
  docker run -it --rm -v $(pwd):/app foxfoxio/claat export 1rpHleSSeY-MJZ8JvncvYA8CFqlnlcrW8-a4uEaqizP
  ```

  - authorization may be prompted:

    ```bash
      ➜ docker run -it --rm -v $(pwd):/app foxfoxio/claat export 1rpHleSSeY-MJZ8JvncvYA8CFqlnlcrW8-a4uEaqizP
    Authorize me at following URL, please:

    https://accounts.google.com/o/oauth2/auth?access_type=offline&client_id=183908478743-e8rth9fbo7juk9eeivgp23asnt791g63.apps.googleusercontent.com&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive.readonly&state=unused

    Code:
    ```

### serve command

run claat local server

  ```bash
  docker run --rm -v $(pwd):/app -p 9090:9090 foxfoxio/claat serve -addr 0.0.0.0:9090
  ```

## build

```bash
docker build -t foxfoxio/claat:latest .
```
