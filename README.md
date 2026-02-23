# 🚀 Compose Multiplatform Library Collection

A curated list of essential libraries for Kotlin Multiplatform (KMP) development, covering everything from logging to animations.

---

## 📝 Logging: Napier

A logger library for Kotlin Multiplatform.

* **Support:** Android, iOS, Desktop, Web
* **Link:** [Napier GitHub](https://github.com/AAkira/Napier)

### How to use

```kotlin
// Initialize Napier
Napier.base(DebugAntilog())

// Usage
Napier.d(tag = "HomeScreen") { "FilePicker initialized" }

```

---

## 🔐 Permissions (Calf)

Simple permission handling for Compose Multiplatform.

* **Support:** Android, iOS
* **Version:** `0.8.0`
* **Link:** [Calf Documentation](https://mohamedrejeb.github.io/Calf/permissions/)

### How to use

```kotlin
val cameraPermissionState = rememberPermissionState(Permission.Camera)
cameraPermissionState.launchPermissionRequest()

```

---

## 📁 File Picker (Calf)

A native file picker for KMP.

* **Support:** Android, iOS, Web, Desktop
* **Version:** `0.8.0`
* **Link:** [Calf FilePicker](https://mohamedrejeb.github.io/Calf/filepicker/)

### How to use

```kotlin
val pickerLauncher = rememberFilePickerLauncher(
    type = FilePickerFileType.All,
    selectionMode = FilePickerSelectionMode.Single,
    onResult = { files ->
        scope.launch {
            files.firstOrNull()?.let { file ->
                // Access file data
                val bytes = file.readByteArray(context)
            }
        }
    }
)

// Trigger the picker
pickerLauncher.launch()

```

---

## 🍞 Toast Messages: Compose Sonner

A beautiful, customizable toast library.

* **Support:** Android, iOS, Desktop, Web
* **Link:** [Compose Sonner GitHub](https://github.com/dokar3/compose-sonner)

### Setup & Usage

**settings.gradle.kts**

```kotlin
dependencyResolutionManagement {
    repositories {
        maven { url = uri("https://jitpack.io") }
    }
}

```

**Implementation**

```kotlin
val toaster = rememberToasterState()

Button(onClick = { toaster.show("Hello world!") }) {
    Text("Show a toast")
}

Toaster(state = toaster)

```

---

## ⏰ Date and Time

The official Kotlin Multiplatform date/time library.

* **Implementation:** `implementation("org.jetbrains.kotlinx:kotlinx-datetime:0.7.1")`

### How to use

```kotlin
val format = LocalDateTime.Format {
    byUnicodePattern("yyyy-MM-dd h:mm")
}
val instance = Clock.System.now().toLocalDateTime(TimeZone.currentSystemDefault())
val formatted = format.format(instance)

Text("Date: $formatted")

```

---

## 🎨 Lottie Animations: Compottie

Lottie rendering for Compose Multiplatform.

* **Link:** [Compottie GitHub](https://github.com/alexzhirkevich/compottie)
* **Assets:** [IconScout](https://iconscout.com) (Recommended for Lottie icons)

### How to use

```kotlin
val composition by rememberLottieComposition {
    LottieCompositionSpec.JsonString(
        Res.readBytes("drawable/loading.json").decodeToString()
    )
}

val progress by animateLottieCompositionAsState(
    composition = composition,
    iterations = Compottie.IterateForever
)

Image(
    painter = rememberLottiePainter(composition = composition, progress = { progress }),
    contentDescription = "Lottie animation",
    modifier = Modifier.size(200.dp)
)

```

---

## 📱 Device Info: KDeviceInfo

Easily fetch hardware and OS metadata.

* **Support:** Android, iOS, Web (Wasm), Desktop
* **Link:** [KDeviceInfo GitHub](https://github.com/swapnil-musale/KDeviceInfo)

---

## 🖱️ Drag Select Compose

Google Photos-style drag-to-select functionality.

* **Support:** Android, iOS, Web (JS/Wasm), Desktop
* **Link:** [Drag Select GitHub](https://github.com/jordond/drag-select-compose)

---

## 🌐 Connectivity Monitor

Monitor network status across platforms.

* **Support:** Android, iOS, Web (Wasm), Desktop
* **Link:** [CMP Connectivity Monitor](https://github.com/Chaintech-Network/CMPConnectivityMonitor)

---

## 🔳 Barcode & QR Code: QRose

A lightweight and powerful library for generating QR codes and barcodes in Compose Multiplatform.

* **Support:** Android, iOS, Desktop, Web (Wasm/JS)
* **Link:** [QRose GitHub](https://github.com/alexzhirkevich/qrose)


---

## 📏 Scalable Layouts: SDP/SSP

A library for scalable units (**sdp** for layout sizes and **ssp** for text sizes). It helps maintain a consistent UI across different screen sizes and densities.

* **Support:** Android, iOS, Desktop, Web (Wasm/JS)
* **Link:** [SDP-SSP GitHub](https://github.com/Chaintech-Network/sdp-ssp-compose-multiplatform)

---


