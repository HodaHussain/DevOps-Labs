# Bonus: Compare Docker Image Sizes

## Goal
Compare the image built with Maven inside Docker (`app1`) with the image created using a pre-built JAR and a Java 17 base image (`app2`).

## Measured results from `docker images`

| Image | Disk usage | Content size |
|---|---:|---:|
| `app1:latest` | 807 MB | 251 MB |
| `app2:latest` | 453 MB | 153 MB |
| Difference (`app1 - app2`) | **354 MB** | **98 MB** |

## Explanation
`app1` was built from a Maven/Java 17 base image and runs `mvn package` during the Docker build. `app2` uses an Amazon Corretto Java 17 base image and copies an already-generated JAR into the image.

The second approach is generally expected to be smaller because it avoids including the Maven build process and source files in the final image. The actual difference depends on the base image and Dockerfile contents. In this case, the `docker images` output shows `app2` is smaller by 354 MB in the displayed disk-usage column, and by 98 MB in the content-size column.

## Conclusion
The bonus comparison is supported by the image-size output provided. To make the bonus fully convincing, include a screenshot showing both image tags and their sizes. Separately verify that both containers run correctly; image sizes alone do not prove application functionality.

## Screenshot
Add the actual screenshot of `docker images` showing `app1:latest` and `app2:latest`.
