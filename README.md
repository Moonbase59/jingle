# jingle

**If you like what you got, please consider to [![Donate with Paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/donate/?hosted_button_id=PBPR63362LDEU). Thank you! ❤️**

**Quickly generate a Jingle using Text-to-Speech**

Sometimes you just quickly need a short jingle with a bumper, and have no speaker available. Or sit hundreds of miles away and must do it on your server.

This is a little bash script that does just that, using a TTS (Text-to-Speech) engine in a nice way. It can:

- generate an MP3 file from either PicoTTS (local) or gtts (Google TTS)
- perform a little sound optimization on the TTS voice (bass/treble correction, compressor/limiter)
- add a starting/ending bumper, using a sound file
- add starting/ending _silence_ (for dumb crossfaders)
- add a nice ID3 tag (fills in Title, Artist, Album, Year, Genre)
- perform ReplayGain calculation and add ReplayGain tags using [loudgain](https://github.com/Moonbase59/loudgain)

### Requirements

You’ll need:

- a Linux machine (can even be your server)
- `sox` installed
- `pico2wave` (from PicoTTS) —or— `gtts-cli` (Google TTS)
- `mid3iconv` from the Mutagen package (optional)
- `loudgain` for ReplayGain (optional)
- a minimum understanding of how to edit code. No worries. It’s very well commented!

### Installation

1. Download `jingle`, make it executable, and put it somewhere in your path. `~/bin`, `~/.local/bin` or `/usr/local/bin` are good places.
2. Install missing dependencies (see above).
3. Edit `jingle` using a text editor and change output folder and bumper sound file:
   ```bash
   media_folder="$(xdg-user-dir MUSIC)/Other/Jingles/Programm/"
   ```
   ```bash
   logo="$(xdg-user-dir MUSIC)/Other/Sounds/MCH/Whoosh2.flac"
   ```
4. Read the comments at the beginning of the file—you might want to change other options like:
   - TTS engine
   - TTS language
   - silence generation at start and end (specify in seconds)
   - Album and Genre ID3 tags
   - comment out the `play` command at the end of the file

### Make a jingle

The syntax is `jingle` `filename` `text to speak`. Use quotes as appropriate. The filename part will also be used as the ID3 Title tag, so use a "speaking" name.

Typing `jingle` without parameters shows a little help screen.

Let’s make a test jingle:
```
jingle 'This is a test' 'This is only a test.'
```

It will be processed, played aloud and and stored in `media_folder`. Depending on your installed software, it should have correct ID3 tags and ReplayGain data.

Here is the audio generated by above command:  
https://github.com/Moonbase59/jingle/raw/master/This%20is%20a%20test.mp3

The auto-generated ID3 tags look like this:

![Auswahl_288](https://github.com/Moonbase59/jingle/assets/3706922/955387f9-e135-4f4d-96ef-962c258969f5)

_Hint:_ If working on a server (no audio hardware), comment out the `play` command at the end!

**Enjoy!**
