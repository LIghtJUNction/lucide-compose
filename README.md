# Lucide Compose

Kotlin Multiplatform Compose bindings for [Lucide Icons](https://lucide.dev/).
The library supports Android, Desktop/JVM, JavaScript, WebAssembly, iOS, and
macOS targets.

## Install

This fork serves Android artifacts anonymously with the fixed snapshot version
`1.0.0-SNAPSHOT`. Source provenance and rebuild steps are in [PUBLIC_MAVEN.md](PUBLIC_MAVEN.md).

```kotlin
repositories {
    maven {
        url = uri("https://raw.githubusercontent.com/LIghtJUNction/lucide-compose/Moe/maven")
    }
}

dependencies {
    implementation("io.github.YumeYucca:lucide-compose:1.0.0-SNAPSHOT")
}
```

Replace `Moe` in the repository URL with the publication commit for a pinned build.
Other platform artifacts can be built from source using the upstream targets.

## Use icons

```kotlin
import androidx.compose.foundation.Image
import androidx.compose.ui.graphics.vector.rememberVectorPainter
import io.github.yumeyucca.lucide.Lucide
import io.github.yumeyucca.lucide.LucideRegistry

@Composable
fun IconExamples() {
    Image(
        painter = rememberVectorPainter(Lucide.Info),
        contentDescription = "Information",
    )

    LucideRegistry.searchIcon("building").forEach { icon ->
        Image(
            painter = rememberVectorPainter(icon),
            contentDescription = null,
        )
    }
}
```

The icon vectors are standard Compose `ImageVector` values, so they work with
`Image` and any custom Compose UI component.
