# Whisper ASR Box

Whisper ASR Box is a general-purpose speech recognition toolkit. Whisper Models are trained on a large dataset of diverse audio and is also a multitask model that can perform multilingual speech recognition as well as speech translation and language identification.

## rbb Features (for GPU acceleration and persistent cache)

To support voice_activity_detection the faster_whisper model has to be used:

- [SYSTRAN/faster-whisper](https://github.com/SYSTRAN/faster-whisper)@[v1.1.0](https://github.com/SYSTRAN/faster-whisper/releases/tag/v1.1.0)


Before starting the container, create a .env file with the content from the .env.example file.

The container then has to be started with the following commands:

```shell
docker run -d -p 9000:9000 \
  --env-file ./.env \
  --gpus all \
  -v $PWD/cache:/data/whisper \
  image_name
```

## Environment Variables

Key configuration options:

- `ASR_ENGINE`: Engine selection (openai_whisper, faster_whisper, whisperx)
- `ASR_MODEL`: Model selection (tiny, base, small, medium, large-v3, etc.)
- `ASR_MODEL_PATH`: Custom path to store/load models
- `ASR_DEVICE`: Device selection (cuda, cpu)
- `MODEL_IDLE_TIMEOUT`: Timeout for model unloading

## Documentation

For complete documentation, visit:
[https://ahmetoner.github.io/whisper-asr-webservice](https://ahmetoner.github.io/whisper-asr-webservice)


## Credits

- This software uses libraries from the [FFmpeg](http://ffmpeg.org) project under the [LGPLv2.1](http://www.gnu.org/licenses/old-licenses/lgpl-2.1.html)
