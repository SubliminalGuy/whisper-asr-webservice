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
  -v ISILON_transcript_files:/app/files \
  image_name
```

## Environment Variables

Key configuration options (see .env.example for default values):

- `ASR_ENGINE`: Engine selection (openai_whisper, faster_whisper, whisperx)
- `ASR_MODEL`: Model selection (tiny, base, small, medium, large-v3, etc.)
- `ASR_MODEL_PATH`: Custom path to store/load models
- `ASR_DEVICE`: Device selection (cuda, cpu)

## Request URL Query Params

| Name            | Values                                         | Description                                                    |
|-----------------|------------------------------------------------|----------------------------------------------------------------|
| file_name     | `text`                                          | Basename of Audio or video file to transcribe                              |
| output          | `text` (default), `json`, `vtt`, `srt`, `tsv` | Output format                                                  |
| task            | `transcribe`, `translate`                      | Task type - transcribe in source language or translate to English |
| language        | `en` (default is auto recognition)             | Source language code (see supported languages)                 |
| word_timestamps | false (default)                                | Enable word-level timestamps (Faster Whisper only)             |
| vad_filter      | false (default)                                | Enable voice activity detection filtering (Faster Whisper only) |
| encode          | true (default)                                 | Encode audio through FFmpeg before processing                  |
| diarize         | false (default)                                | Enable speaker diarization (WhisperX only)                     |
| min_speakers    | null (default)                                 | Minimum number of speakers for diarization (WhisperX only)     |
| max_speakers    | null (default)                                 | Maximum number of speakers for diarization (WhisperX only)     |

## Documentation

For complete documentation, visit:
[https://ahmetoner.github.io/whisper-asr-webservice](https://ahmetoner.github.io/whisper-asr-webservice)

## Info about NVIDIA libraries that need to be installed

[github.com](https://github.com/SYSTRAN/faster-whisper?tab=readme-ov-file#gpu)

## Credits

- This software uses libraries from the [FFmpeg](http://ffmpeg.org) project under the [LGPLv2.1](http://www.gnu.org/licenses/old-licenses/lgpl-2.1.html)
