# [Music Downloader Telegram Bot](https://t.me/scdlbot)

[![Updates](https://pyup.io/repos/github/gpchelkin/scdlbot/shield.svg?token=376ffde2-5188-4912-bf3c-5f316e52d43f)](https://pyup.io/repos/github/gpchelkin/scdlbot/)
[![Python 3](https://pyup.io/repos/github/gpchelkin/scdlbot/python-3-shield.svg?token=376ffde2-5188-4912-bf3c-5f316e52d43f)](https://pyup.io/repos/github/gpchelkin/scdlbot/)
[![Telegram Bot](https://img.shields.io/badge/telegram-bot-blue.svg)](https://t.me/scdlbot)


## Usage

Send `/start` or `/help` command to [bot](https://t.me/scdlbot) or refer directly to the [help message](scdlbot/messages/help.tg.md).

## Development

### Supported Sites and Requirements

- [**Python 3.6**](https://www.python.org/): [pyenv](https://github.com/pyenv/pyenv) recommended
- [**Telegram Bot API**](https://core.telegram.org/bots/api): [python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot)
- [**SoundCloud**](https://soundcloud.com): [scdl](https://github.com/flyingrub/scdl)
- [**Bandcamp**](https://bandcamp.com): [bandcamp-dl](https://github.com/iheanyi/bandcamp-dl)
- [**YouTube**](https://www.youtube.com/), [**Mixcloud**](https://www.mixcloud.com/), etc.: [youtube-dl](https://rg3.github.io/youtube-dl)
- [**FFmpeg**](https://ffmpeg.org): [Windows builds](https://ffmpeg.zeranoe.com/builds/), [Linux builds](https://johnvansickle.com/ffmpeg/)
- Use [SoundScrape](https://github.com/Miserlou/SoundScrape) in the future?

### Environment Variables

#### Required
- `TG_BOT_TOKEN` — Telegram Bot API Token, [obtain here](https://t.me/BotFather)
- `STORE_CHAT_ID` — Chat ID for storing audios for inline mode
- `SC_AUTH_TOKEN` — SoundCloud Auth Token, [obtain here](https://flyingrub.github.io/scdl/)

#### Optional
- `NO_CLUTTER_CHAT_IDS` — Comma-separated chat IDs with no replying and caption hashtags
- `BIN_PATH` — Custom directory with `scdl` and `bandcamp-dl` binaries are available
- `DL_DIR` — Parent directory for MP3 download directory, default: ~ (user's home directory)

### Running Locally
Install Python 3.6 and FFmpeg.
```
python3 -m scdlbot
```

### Deploying to [Heroku](https://heroku.com/)

#### Automatically

Press this button:

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

#### Manually

Register on Heroku, install [Heroku Toolbelt](https://toolbelt.heroku.com/), then:

```
git clone https://github.com/gpchelkin/scdlbot.git
cd scdlbot
# Login to Heroku:
heroku login
# Create app with Python3 buildpack:
heroku create --buildpack heroku/python
# Set Python3 buildpack for upcoming builds:
heroku buildpacks:set heroku/python
# Add FFmpeg buildpack for youtube-dl:
heroku buildpacks:add --index 1 https://github.com/laddhadhiraj/heroku-buildpack-ffmpeg.git --app scdlbot
# Deploy this app to Heroku:
git push heroku master
# Set config vars:
heroku config:set SC_AUTH_TOKEN='<SC_AUTH_TOKEN>' TG_BOT_TOKEN='<TG_BOT_TOKEN>' STORE_CHAT_ID='<STORE_CHAT_ID>'
# Start 1 worker dyno:
heroku ps:scale worker=1
# Stop worker dyno:
heroku ps:stop worker
# Stop worker dyno:
heroku ps:stop worker
# Restart worker dyno:
heroku ps:restart worker
# Attach to logs:
heroku logs -t -p worker
# Test run
heroku run "ffprobe -version"
```

[More Heroku information](https://devcenter.heroku.com/articles/dynos).
