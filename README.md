# 🎵 Pulse: Audio Waveform Video Generator

Generate beautiful, dynamic waveform videos from any audio file. This [Cog](https://github.com/replicate/cog) model creates a stylish dotted waveform and overlays it on a background image that can pulse to the music or slowly zoom in.

[**Run this model on Replicate »**](https://replicate.com/craftfulcharles/waveform)

## ✨ Features

This model takes any audio file and an optional image and turns them into a shareable MP4 video.

  * **Dotted Waveform:** Creates a "dot" style audio visualization.
  * **Image Background:** Overlay the waveform on any background image.
  * **Dynamic Effects:**
      * **Pulse:** Make the image "thump" or pulse in time with the music's amplitude.
      * **Zoom In:** Add a slow, cinematic zoom-in effect to the image.
  * **Smooth Pulse:** The pulse effect is smoothed to look more natural and less "jerky."
  * **Auto-Fill & Crop:** Your background image is automatically scaled to fill the entire video frame, cropping from the center (no black bars\!).
  * **Customizable:** Control dot size, color, spacing, FPS, and more.

## 🚀 Using the Replicate API

You can run this model directly from your own Python code using the [Replicate API client](https://github.com/replicate/replicate-python).

First, install the client:

```bash
pip install replicate
```

Then, set your API token as an environment variable:

```bash
export REPLICATE_API_TOKEN=[your_api_token]
```

Now you can run predictions:

```python
import replicate

# --- Example 1: Pulsing Image ---
output_pulse = replicate.run(
    "your-username/your-model-name:version-id",
    input={
        "audio_file": open("path/to/my-song.mp3", "rb"),
        "image_file": open("path/to/my-image.jpg", "rb"),
        "image_effect": "pulse",
        "dot_color": "#FF0080",
        "pulse_intensity": 0.5,
        "pulse_smoothing": 0.7
    }
)
print(f"Pulsing video at: {output_pulse}")


# --- Example 2: Zoom-In Effect ---
output_zoom = replicate.run(
    "your-username/your-model-name:version-id",
    input={
        "audio_file": open("path/to/my-audio.wav", "rb"),
        "image_file": open("path/to/my-background.png", "rb"),
        "image_effect": "zoom_in",
        "dot_color": "#FFFFFF",
        "zoom_start": 1.0,
        "zoom_end": 1.5
    }
)
print(f"Zooming video at: {output_zoom}")
```

## ⚙️ Model Inputs

The model accepts the following inputs:

| Parameter | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| `audio_file` | `Path` | Input audio file. | *Required* |
| `image_file` | `Path` | Optional background image. | `None` |
| `dot_size` | `int` | Size of dots in pixels. | `6` |
| `dot_spacing` | `int` | Spacing between dots in pixels. | `6` |
| `height` | `int` | Height of the output video. | `720` |
| `width` | `int` | Width of the output video. | `1280` |
| `max_height` | `int` | Max height of visualization as a % of frame. | `30` |
| `dot_color` | `str` | Dot color in hex format. | `"#00FFFF"` |
| `fps` | `int` | Frames per second. | `10` |
| `image_effect` | `str` | Effect to apply to the image. (`pulse`, `zoom_in`, `none`) | `"pulse"` |
| `pulse_intensity` | `float` | Intensity of the pulse effect (max scale added to base). | `0.1` |
| `pulse_smoothing`| `float` | Smoothing factor for the pulse (0.0 = jerky, 0.9 = smooth).| `0.7` |
| `zoom_start` | `float` | Base image scale (or zoom start scale). | `1.0` |
| `zoom_end` | `float` | Ending zoom scale (for 'zoom\_in' effect). | `1.2` |

## 📤 Model Output

The model returns a `Path` (string URL) to the generated `.mp4` video file.

-----

## 💻 Local Development

To run this model locally, you'll need to install [Cog](https://github.com/replicate/cog).

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/your-username/your-repo-name.git
    cd your-repo-name
    ```

2.  **Install dependencies:**
    The `cog.yaml` file lists all system and Python dependencies. They will be automatically installed inside a Docker container when you run the model.

3.  **Run a prediction:**

    ```bash
    cog run python predict.py \
      -i audio_file=@"path/to/song.mp3" \
      -i image_file=@"path/to/image.png" \
      -i image_effect="pulse" \
      -i pulse_intensity=0.5
    ```

The output video will be saved to `/tmp/output.mp4` inside the container.
