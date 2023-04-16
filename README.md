This script takes an epub and creates mp3's of the chapters, read by https://github.com/coqui-ai/TTS

I have not had good luck getting Coqui-AI to run on an M1 mac but it runs great on Linux. You CAN however run this on a mac with docker. Should work with [LIMA](https://github.com/lima-vm/lima), just remember to [make your home directory writable](https://github.com/lima-vm/lima#filesystem-is-not-writable) for the docker template, otherwise saving the voice model will fail.

I recognize this is not very user friendly, but I wanted to share in case folks thought it was useful. If there are a few more people than myself that find this is useful I will keep working on turning it into something that could be used by someone without dev experience.

## Docker usage:
Voice models will be saved locally in `~/.local/share/tts`

Change to directory containing your epub and run with:
```
docker run -v "$PWD:$PWD" -v ~/.local/share/tts:/root/.local/share/tts -w "$PWD" -e BOOK=your-book.epub ghcr.io/aedocw/epub2tts:release
```

## INSTALLATION:

For  now I've only tested this on a linux machine (Ubuntu 22 in my case). Ensure you have `ffmpeg` installed before use.

```
#clone the repo
git clone https://github.com/aedocw/epub2tts
cd epub2tts
pip install .
```

Usage: `epub2tts my-book.epub`

## DEVELOPMENT INSTALL:

For  now I've only tested this on a linux machine (Ubuntu 22 in my case)

```
#clone the repo
git clone https://github.com/aedocw/epub2tts
cd epub2tts
#create a virtual environment
python3 -m venv .venv
#activate the virtual environment
source .venv/bin/activate
#install dependencies
sudo apt install espeak-ng ffmpeg
pip3 install -r requirements.txt
```

Usage: `python3 epub2tts.py my-book.epub`