With your upload (≈162 Mbps), bandwidth shouldn’t be the limiter—missing minutes usually come from brief disconnects or bursts of dropped frames. Set OBS to be more tolerant **and** keep recording quality high by splitting Streaming vs Recording settings.

# Step-by-step (YouTube 1080p60 target)

## 1) Video

* **Settings → Video**

  * **Base (Canvas):** your display
  * **Output (Scaled):** **1920×1080**
  * **Downscale filter:** **Lanczos (36 samples)**
  * **FPS:** **60** (use 30 if mostly slides)

## 2) Output mode

* **Settings → Output → Output Mode:** **Advanced**

## 3) Streaming (stable)

* **Encoder:** Prefer **NVENC (H.264)** (or x264 if no NVENC)
* **Rate Control:** **CBR**
* **Bitrate:** **8000 kbps** (safe for 1080p60 and leaves big headroom)
* **Keyframe Interval:** **2 s**
* **Preset (NVENC):** **Quality** (or **P5 Quality** on new NVENC)
* **Profile:** **High**
* **Look-ahead:** **Off**
* **Psycho Visual Tuning:** **On**
* **Max B-frames:** **2**
* **Audio Track:** 1 at **320 kbps** (see “Audio” below)

> If you want 1440p60, set bitrate **12,000–18,000 kbps**; for 4K60, **25,000–45,000 kbps**—only if your GPU/CPU can handle it.

## 4) Recording (high quality archive)

* **Type:** Standard
* **Recording Format:** **MKV**

  * Check **Automatically remux to MP4** (so crashes don’t corrupt files).
* **Encoder:** **NVENC (H.264)** (separate from stream)
* **Rescale Output:** **Off** (records at canvas/output res)
* **Rate Control:** **CQP**
* **CQ:** **18–20** (18 = visually lossless-ish; raise number for smaller files)
* **Keyframe Interval:** **2 s**
* **Preset:** **Quality** (or **P5 Quality**)
* **Profile:** **High**
* **Max B-frames:** **2**
* **Tracks:** enable 1–2; set **320 kbps** per track (see next)

## 5) Audio

* **Settings → Audio**

  * **Sample Rate:** **48 kHz**, **Channels:** **Stereo**
* **Settings → Output → Audio**

  * **Track 1 (Stream):** **320 kbps**
  * **Track 2 (Recording, optional separate mic):** **320 kbps**

## 6) Advanced → Network (protect the stream)

* **Enable Dynamic Bitrate:** **On** (lets OBS lower bitrate temporarily instead of dropping)
* **Enable Network Optimizations:** **On** (if available)
* **Automatically Reconnect:** **On**, **Retry Delay:** **5–10 s**, **Max Retries:** **20**
* **Stream Delay:** **Off** unless you need it (reduces complexity)

## 7) YouTube settings

* **Service:** YouTube-RTMPS
* In YouTube Live Control Room, choose **Normal latency** (or **Low** if you need interaction).
* When ending, **Stop Streaming in OBS**, then **End Stream** in YouTube—don’t close OBS abruptly.

## 8) Reliability checklist

* Use **wired Ethernet** (avoid Wi-Fi/VPN).
* While live, **View → Stats** in OBS; watch **Dropped Frames (Network)**—anything above \~0.2% indicates issues.
* Close cloud backups/large uploads during the stream.
* Router QoS: give your PC upload priority if others share the network.

---

### Why this helps

* **Dynamic Bitrate + moderate 8 Mbps stream** prevents big drops even if your ISP briefly dips.
* **Separate high-quality CQP recording** keeps your local copy pristine regardless of stream conditions.
* **MKV + auto-remux** protects recordings from power/app crashes.

If you want presets for **1440p60** or **4K30/60**, tell me your GPU/CPU and I’ll give exact values.
