# Image Digest Buildkite Plugin

A [Buildkite plugin](https://buildkite.com/docs/plugins) to retrieve the digest of a specified Docker image.

## Example

```yaml
steps:
  - label: "Get image digest"
    plugins:
      - image-digest#v1.0.0:
          image: "alpine:latest"
```

## Configuration

### `image` (required)

The name of the Docker image to retrieve the digest for.

## Output

This plugin exports the image digest in two ways:

1. As an environment variable: `BUILDKITE_PLUGIN_IMAGE_DIGEST_RESULT`
2. As Buildkite meta-data with the key `image-digest`

You can use the digest in subsequent steps like this:

```yaml
steps:
  - label: "Get image digest"
    plugins:
      - image-digest#v1.0.0:
          image: "alpine:latest"
          
  - label: "Use the digest"
    command: |
      echo "The digest is: $BUILDKITE_PLUGIN_IMAGE_DIGEST_RESULT"
      # or
      echo "The digest is: $(buildkite-agent meta-data get image-digest)"
```

## Requirements

* Docker must be installed and available in the path

## License

MIT (see [LICENSE](LICENSE))