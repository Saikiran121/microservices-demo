# ---- Build stage ----
FROM eclipse-temurin:21-jdk AS builder
WORKDIR /src
COPY gradlew settings.gradle build.gradle ./
COPY gradle ./gradle
RUN chmod +x gradlew
COPY . .
RUN ./gradlew clean installDist

# ---- Runtime stage ----
FROM eclipse-temurin:21-jre
WORKDIR /opt/hipstershop

# Copy the full distribution (bin + lib) into /opt/hipstershop
COPY --from=builder /src/build/install/hipstershop/ ./

EXPOSE 9099
# Run the generated startup script
ENTRYPOINT ["./bin/AdService"]
