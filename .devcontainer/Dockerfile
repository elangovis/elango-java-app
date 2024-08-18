# Use a base image with Java installed (openjdk 11)
FROM openjdk:11-jdk-slim

# Define the Gradle version to be installed
ENV GRADLE_VERSION=7.5.1

# Install system dependencies required for downloading and extracting Gradle
RUN apt-get update && apt-get install -y \
    wget \
    unzip \
    curl \
    build-essential \
    && apt-get clean

# Download and install Gradle
RUN wget https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -P /tmp && \
    unzip /tmp/gradle-${GRADLE_VERSION}-bin.zip -d /opt && \
    ln -s /opt/gradle-${GRADLE_VERSION} /opt/gradle && \
    rm /tmp/gradle-${GRADLE_VERSION}-bin.zip

# Set environment variables for Gradle and Java
ENV GRADLE_HOME=/opt/gradle
ENV JAVA_HOME=/usr/local/openjdk-11
ENV PATH="${GRADLE_HOME}/bin:${JAVA_HOME}/bin:${PATH}"

# Set the working directory for the project
WORKDIR /workspace

# Copy the project files into the container
COPY . /workspace

# Verify Gradle installation
RUN gradle -v

# Expose a bash command as the default entrypoint
CMD ["/bin/bash"]
