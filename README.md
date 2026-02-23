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



---

# Compose Media Player 🎬

A powerful, lightweight Media Player for **Compose Multiplatform**. One codebase to handle video playback across all major platforms.

* **Support:** Android, iOS, Desktop, Web (Wasm/JS)
* **Link:** [ComposeMediaPlayer](https://github.com/kdroidFilter/ComposeMediaPlayer)

## 🛠 Usage

Integrating the media player into your Composable is straightforward. Below is a complete example of a custom video player with controls.

```kotlin
@Composable
fun VideoPlayer(videoUrl: String) {
    val playerState = rememberVideoPlayerState()

    // Extract duration and calculate current time for the UI
    val durationMs = playerState.metadata.duration ?: 0L
    val currentTimeMs = (playerState.sliderPos / 1000f * durationMs).toLong()

    // Initialize/Load Video
    LaunchedEffect(videoUrl) {
        playerState.openUri(videoUrl)
    }

    Column(modifier = Modifier.fillMaxSize().background(Color.Black)) {
        Box(
            modifier = Modifier.weight(1f).fillMaxWidth(),
            contentAlignment = Alignment.Center
        ) {
            // The Video Surface
            VideoPlayerSurface(
                playerState = playerState,
                modifier = Modifier.fillMaxSize(),
                contentScale = ContentScale.Fit
            ) {
                // UI Overlay Layer
                Box(modifier = Modifier.fillMaxSize()) {

                    // Loading Indicator
                    if (playerState.isLoading) {
                        CircularProgressIndicator(
                            modifier = Modifier.align(Alignment.Center),
                            color = Color.Green
                        )
                    }

                    // Error Handling
                    playerState.error?.let { error ->
                        Text(
                            text = "Error: $error",
                            color = Color.Red,
                            modifier = Modifier.align(Alignment.Center).padding(16.dp)
                        )
                    }

                    // Bottom Control Bar
                    PlayerControls(playerState, currentTimeMs, durationMs)
                }
            }
        }
    }
}

@Composable
fun BoxScope.PlayerControls(
    playerState: VideoPlayerState,
    currentTimeMs: Long,
    durationMs: Long
) {
    Column(
        modifier = Modifier
            .align(Alignment.BottomCenter)
            .fillMaxWidth()
            .background(Color.Black.copy(alpha = 0.6f))
            .padding(horizontal = 16.dp, vertical = 8.dp)
    ) {
        // --- Seek Bar & Time ---
        Row(
            modifier = Modifier.fillMaxWidth(),
            verticalAlignment = Alignment.CenterVertically
        ) {
            Text(formatDuration(currentTimeMs), color = Color.White, fontSize = 12.sp)

            Slider(
                value = playerState.sliderPos,
                onValueChange = {
                    playerState.sliderPos = it
                    playerState.userDragging = true
                },
                onValueChangeFinished = {
                    playerState.userDragging = false
                    playerState.seekTo(playerState.sliderPos)
                },
                valueRange = 0f..1000f,
                modifier = Modifier.weight(1f).padding(horizontal = 8.dp),
                colors = SliderDefaults.colors(thumbColor = Color.White, activeTrackColor = Color.Red)
            )

            Text(formatDuration(durationMs), color = Color.White, fontSize = 12.sp)
        }

        // --- Action Buttons ---
        Row(
            modifier = Modifier.fillMaxWidth(),
            verticalAlignment = Alignment.CenterVertically,
            horizontalArrangement = Arrangement.spacedBy(16.dp)
        ) {
            // Play/Pause
            IconButton(onClick = { if (playerState.isPlaying) playerState.pause() else playerState.play() }) {
                Icon(
                    painter = if (playerState.isPlaying) painterResource(Res.drawable.ic_pause) else painterResource(Res.drawable.ic_play),
                    contentDescription = "Play/Pause",
                    tint = Color.White,
                    modifier = Modifier.size(32.dp)
                )
            }

            // Stop
            IconButton(onClick = { playerState.stop() }) {
                Icon(painterResource(Res.drawable.ic_stop), "Stop", tint = Color.White)
            }

            // Volume
            Icon(painterResource(Res.drawable.ic_volume_up), null, tint = Color.White, modifier = Modifier.size(20.dp))
            Slider(
                value = playerState.volume,
                onValueChange = { playerState.volume = it },
                valueRange = 0f..1f,
                modifier = Modifier.width(100.dp)
            )

            Spacer(Modifier.weight(1f))

            // Fullscreen
            IconButton(onClick = { playerState.toggleFullscreen() }) {
                Icon(
                    painter = if (playerState.isFullscreen) painterResource(Res.drawable.ic_minimize) else painterResource(Res.drawable.ic_full_size),
                    contentDescription = "Toggle Fullscreen",
                    tint = Color.White
                )
            }
        }
    }
}

// helper format duration
fun formatDuration(ms: Long): String {
    val totalSeconds = ms / 1000
    val minutes = (totalSeconds / 60) % 60
    val seconds = totalSeconds % 60
    val hours = totalSeconds / 3600

    return if (hours > 0) {
        "${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}"
    } else {
        "${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}"
    }
}



```





