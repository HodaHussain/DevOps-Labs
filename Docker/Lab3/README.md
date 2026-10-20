# Lab 3: Creating Docker Images for a Java Application

## Objective
Create Docker images for the CalculatorMavenApp using two approaches and compare their sizes.

## Repository
[CalculatorMavenApp on GitHub](https://github.com/Ibrahim-Adel15/CalculatorMavenApp)

## Part 1: Build inside Docker

### Dockerfile observed in `~/test/lab1/CalculatorMavenApp`
```dockerfile
FROM maven:3.10-eclipse-temurin-17-noble

WORKDIR /app

COPY . .

RUN mvn package

CMD ["java","-jar","target/calculator.jar"]

EXPOSE 8080
```

### Steps evidenced by the terminal output
1. Used a Maven image based on Java 17.
2. Set `/app` as the working directory.
3. Copied the project files into the image.
4. Ran `mvn package` during the image build.
5. Configured the container command to run `target/calculator.jar`.
6. Exposed port `8080`.
7. Tagged the image as `app1:latest`.

### Image size observed
- `app1:latest` disk usage: **807 MB**
- `app1:latest` content size: **251 MB**

The terminal shows that `app1:latest` was tagged from the image previously named `lab3:latest`. The current Dockerfile shown does not create a non-root user, so add that requirement only after updating the Dockerfile and rebuilding, if the instructor requires it.

## Part 2: Build locally and use a Java runtime image

### Dockerfile observed in `~/test/CalculatorMavenApp`
```dockerfile
FROM amazoncorretto:17-alpine3.21-full

WORKDIR /app

COPY target/calculator.jar .

CMD ["java","-jar","calculator.jar"]
```

### Steps evidenced by the terminal output
1. Used an already-generated JAR from `target/calculator.jar`.
2. Used an Amazon Corretto Java 17 base image.
3. Set `/app` as the working directory.
4. Copied `calculator.jar` into the image.
5. Configured the container command to run the JAR.
6. Tagged the image as `app2:latest`.

### Image size observed
- `app2:latest` disk usage: **453 MB**
- `app2:latest` content size: **153 MB**

The terminal shows that `app2:latest` was tagged from the image previously named `new-image:latest`. The shown Dockerfile does not include `EXPOSE 8080` or configure a non-root user. If these are mandatory, update the Dockerfile and rebuild before final submission.

## Image comparison
The two image tags currently show the following sizes:

| Image | Disk usage shown by Docker | Content size shown by Docker |
|---|---:|---:|
| `app1:latest` | 807 MB | 251 MB |
| `app2:latest` | 453 MB | 153 MB |
| Difference (`app1 - app2`) | **354 MB** | **98 MB** |

Based on the displayed disk-usage values, `app2` is smaller by **354 MB**. The displayed content-size difference is **98 MB**. Keep the two measurements distinct because Docker reports both figures.

## Verification still needed
The shared terminal output confirms the image tags and sizes, and confirms that the JAR exists. It does **not by itself prove** that both containers started successfully or that the application responded on port 8080. Add your screenshots of the container status, logs, and application test to document this.

## Screenshots
Put your real screenshots in `screenshots/lab3/` and update with the exact filenames:
- `docker images` showing `app1` and `app2`
- First Dockerfile and build output
- Second Dockerfile and local JAR
- Container status/logs for each approach
- Successful application test for each approach

> The image sizes above are taken from the terminal output you provided. Container verification and compliance with the non-root-user requirement should be documented separately.
