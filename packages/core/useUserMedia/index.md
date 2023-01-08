---
category: Sensors
related: useDevicesList, usePermission
---

# useUserMedia

Reactive [`mediaDevices.getUserMedia`](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia) streaming.

## Usage

```js
import { useUserMedia } from '@vueuse/core'

const { stream, start } = useUserMedia()

start()
```

```ts
const video = document.getElementById('video')

watchEffect(() => {
  // preview on a video element
  video.srcObject = stream.value
})
```

### Constraints

```js
import { useUserMedia } from '@vueuse/core'

const { stream, start } = useUserMedia({
  video: {
    facingMode: 'environment'
  },
  audio: {
    sampleRate: 44100
  }
})

start()
```

### Devices

```js
import { useDevicesList, useUserMedia } from '@vueuse/core'

const {
  videoInputs: cameras,
  audioInputs: microphones,
} = useDevicesList({
  requestPermissions: true,
})
const currentCamera = computed(() => cameras.value[0]?.deviceId)
const currentMicrophone = computed(() => microphones.value[0]?.deviceId)

const { stream } = useUserMedia({
  videoDeviceId: currentCamera,
  audioDeviceId: currentMicrophone,
})
```
or with constraints:
```js
const { stream } = useUserMedia({
  video: {
    deviceId: currentCamera,
    // ...other video constraints
  },
  audio: {
    deviceId: currentMicrophone,
    // ...other audio constraints
  }
})
```
