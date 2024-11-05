# DUrE
DUrE - Davo's Ultimate reEncoder

 Single pass NVENC encoder. Will reecode video based on tiers and can optionally downscale 4k to 1080p. If target rate percentage is lower than tier will scale to that. Reencodes HEVC files but target percentage is always 1. Will removes audio and subtitles that are not in the configured language or marked as commentary. v6 now will give priority options if there are multiple audio tracks. E.g. truehd>dts>ac3. v7 now allows optional reencoding of audio with bitrate per channel and desired codec and number of channels. Default is still to copy the audio though.

Basically I have a number of flows setup for different scenarios. E.g.

Blockbuster - keep really high video (say 5000-10000kbps at 21 quality) and copy the audio as I want to keep it in TrueHD etc.

TV - downscale to 2000kbps (quality 23) (at 1080p - less for other resolutions), reduce audio to EAC3 at 64K/channel with 6 channels.

But of course this all depends on your requirements. I don't want to have a 45GB blueray file that is a drama that I can't tell any difference if I reduce to a 2000kbps file with EAC3/96/6 channels. But we're all different so hence the user options to change.

It will also enable you to choose your preferred audio codec (e.g. DTS rather than TrueAudio) and keep others always (say AAC always is retained).

Some of the initial code was from the DOOM script which had great stuff. I've extensively modified it but as this was my first script was helpful to use the DOOM script as a guide.

It's at v11 at the moment and I haven't found any (more) bugs lately. 
