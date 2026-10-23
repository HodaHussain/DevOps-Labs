# Lab 4: Docker Image Optimization

## Objective
Optimize a Docker image using a multi-stage build, reduce image size, and run the application using a non-root user.

## Steps Performed

### 1. Create the Original Image
Built the original Docker image using the Maven base image and saved it as `image1`.

### 2. Optimize the Dockerfile
Used a multi-stage build to separate the build environment from the runtime environment.

- Build stage: `maven:3.9.15-eclipse-temurin-17-alpine`
- Runtime stage: `eclipse-temurin:17-jre-alpine`
- Copied only the generated JAR file into the final image.
- Created a non-root user named `appuser`.
- Configured the application to run on port `8080`.

### 3. Build the Optimized Image
Built the optimized image and tagged it as `image2`.

### 4. Compare Image Sizes

| Image | Size on Disk |
|---|---:|
| Original (`image1`) | 671 MB |
| Optimized (`image2`) | 294 MB |

The optimized image reduced disk usage by approximately 56%.

### 5. Run and Test the Application
Ran the original and optimized containers on separate host ports.

- Original container: port `18081`
- Optimized container: port `18082`
- Verified the optimized container runs as `appuser`.
- Tested the application and received HTTP 200 with the response: `Hello from Dockerized Spring Boot!`

### 6. Save the Image
Exported the optimized image to a TAR archive using `docker save`.

## Result
The multi-stage build reduced image size and allowed the application to run as a non-root user.

## Screenshots
Screenshots will be added to this repository after uploading them.
<img width="1021" height="557" alt="Screenshot 2026-10-23 104512" src="https://github.com/user-attachments/assets/547f349d-0415-4d69-8bee-7807f56b2888" />
<img width="1007" height="450" alt="Screenshot 2026-10-23 174312" src="https://github.com/user-attachments/assets/abaf9587-c07e-4cdd-b0d2-8755c7261dc0" />
<img width="1021" height="250" alt="Screenshot 2026-10-23 173449" src="https://github.com/user-attachments/assets/ee1927fe-29a5-4742-b578-a73250dec540" />
<img width="1060" height="95" alt="Screenshot 2026-10-23 171510" src="https://github.com/user-attachments/assets/f955aff1-f718-46e3-aba7-c52401f2e4f6" />
<img width="1012" height="447" alt="Screenshot 2026-10-23 112019" src="https://github.com/user-attachments/assets/227aa6be-2bd5-469b-916b-ae7e8b5f7471" />
<img width="997" height="328" alt="Screenshot 2026-10-23 111534" src="https://github.com/user-attachments/assets/7e349b42-63d4-4d24-8cc2-0e2e43e8c9ec" />
<img width="880" height="726" alt="Screenshot 2026-10-23 110447" src="https://github.com/user-attachments/assets/7a8b8371-4d1e-44a9-b6cb-29f3d3d20c44" />

