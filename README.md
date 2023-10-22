# jingle

**Quickly generate a Jingle using Text-to-Speech**

Sometimes you just quickly need a short jingle with a bumper, and have no speaker available. Or sit hundreds of miles away and must do it on your server.

This is a little bash script that does just that, using a TTS (Text-to-Speech) engine in a nice way. It can:

- generate an MP3 file from either PicoTTS (local) or gtts (Google TTS)
- perform a little sound optimization on the TTS voice
- add a starting/ending bumper, using a sound file
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

_Hint:_ If working on a server (no audio hardware), comment out the `play` command at the end!

**Enjoy!**
