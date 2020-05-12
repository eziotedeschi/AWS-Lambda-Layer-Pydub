# AWS Lambda Layer - Pydub

A Lambda Layer containing a static version of FFmpeg / FFprobe binaries built on an Amazon Linux 2.x instance. The python package Pydub has been installed as well and its `utils.py` script slightly modified in order to import the binaries correctly during a Lambda execution.

## Usage

Simply compress the `python` folder and upload it as a new Layer with `python 3.7` as runtime. Once created, you can link the Layer to your Lambda using the AWS console, [AWS CLI](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html#configuration-layers-using) or your preferred deployment tool.

Your Lambda should now be able to execute FFmpeg commands as well as using it through the Pydub module.
```python
print(os.popen("/opt/python/ffmpeg --help").read())
```
```python
from pydub import AudioSegment


def lambda_handler(event, context):
    sound = AudioSegment.from_file("song.mp3", "mp3")

    return True
```

## Components

Lambda runtime (expected) `3.7`

- [FFmpeg](https://johnvansickle.com/ffmpeg/) `4.2.2`
- [Pydub](https://github.com/jiaaro/pydub) `0.24.0`

## License

This repository inherits its license from the [FFMPEG](https://ffmpeg.org/legal.html) project.
