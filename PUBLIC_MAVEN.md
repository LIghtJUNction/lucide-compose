# Public Android Maven repository

Android artifacts in `maven/` are served anonymously over HTTPS.

```kotlin
maven {
    url = uri("https://raw.githubusercontent.com/LIghtJUNction/lucide-compose/Moe/maven")
}
```

Consumers should replace `Moe` with the repository commit containing the artifacts to pin the complete publication.

## Source

- Upstream source commit `a634bb98c87df94fac8e44dc168d06689ee9a249`.
- Upstream source repository `https://github.com/YumeYucca/lucide-compose`.
- Android and Kotlin Multiplatform metadata publications are included.
- Existing Maven coordinates, licenses and upstream POM attribution are preserved.
- `maven/SHA256SUMS` records the published files and their SHA-256 hashes for verification. Rebuilding a SNAPSHOT generates new timestamps and metadata.

## Rebuild

Clone the upstream source at the commit above into a separate build directory. For Lucide, also run `git submodule update --init --depth 1`. Use the source checkout's Gradle Wrapper, JDK 21 and Android SDK platform 36 (`platforms;android-36`). The consuming Github app and Miuix also require platform 37 (`platforms;android-37.0`) and Build Tools 37.0.0.

Set `PUBLIC_MAVEN_DIR` to this fork's absolute `maven/` directory and pass this fork's `public-maven.init.gradle` to the source checkout's Wrapper.

```sh
export ANDROID_HOME=/absolute/path/to/android-sdk
export PUBLIC_MAVEN_DIR=/absolute/path/to/lucide-compose/maven
bash ./gradlew -I /absolute/path/to/lucide-compose/public-maven.init.gradle \
    publishAndroidPublicationToPublicMavenRepository publishKotlinMultiplatformPublicationToPublicMavenRepository \
    --no-configuration-cache --max-workers=2 \
    '-Dorg.gradle.jvmargs=-Xmx2g -Dfile.encoding=UTF-8' \
    -Pkotlin.compiler.execution.strategy=in-process
```

Review the generated Maven files, regenerate `SHA256SUMS`, and commit and push the publication to this fork's existing branch. GitHub Packages credentials are unnecessary for this output repository.
