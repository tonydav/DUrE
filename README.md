# DUrE
DUrE - Davo's Ultimate reEncoder

 Single pass NVENC encoder. Will reecode video based on tiers and can optionally downscale 4k to 1080p. If target rate percentage is lower than tier will scale to that. Reencodes HEVC files but target percentage is always 1. Will removes audio and subtitles that are not in the configured language or marked as commentary. v6 now will give priority options if there are multiple audio tracks. E.g. truehd>dts>ac3. v7 now allows optional reencoding of audio with bitrate per channel and desired codec and number of channels. Default is still to copy the audio though.

To install you simply need to copy to your local plugins directory. 
In my case: /appdata/tdarr/server/Tdarr/Plugins/local

IMPORTANT NOTE:
If you are intending to reencode HVEC to HVEC (so to reduce high bitrate to lower bitrate saving space) you must have a rename in your flow.  In my case I add Davo265 at the end of the file in the flow and then the flow is set to ignore any file with "Davo" in it.  If you don't do this you will continually loop. Message me if you need assistance or a copy of my flow. I have included a sample flow that I use for action movies.
Basically I have a number of flows setup for different scenarios. E.g.

Blockbuster - keep really high video (say 5000-10000kbps at 21 quality) and copy the audio as I want to keep it in TrueHD etc.

TV - downscale to 2000kbps (quality 23) (at 1080p - less for other resolutions), reduce audio to EAC3 at 64K/channel with 6 channels.

But of course this all depends on your requirements. I don't want to have a 45GB blueray file that is a drama that I can't tell any difference if I reduce to a 2000kbps file with EAC3/96/6 channels. But we're all different so hence the user options to change.

It will also enable you to choose your preferred audio codec (e.g. DTS rather than TrueAudio) and keep others always (say AAC always is retained).

Some of the initial code was from the DOOM script which had great stuff. I've extensively modified it but as this was my first script was helpful to use the DOOM script as a guide.

It's at v11 at the moment and I haven't found any (more) bugs lately. 

IMPORTANT NOTE:
If you are intending to reencode HVEC to HVEC (so to reduce high bitrate to lower bitrate saving space) you must have a rename in your flow.  In my case I add Davo265 at the end of the file in the flow and then the flow is set to ignore any file with "Davo" in it.  If you don't do this you will continually loop.

An example of a flow processing a TV Series via the plugin (this log output):

2024-11-06T08:08:06.261Z "Starting video configuration...",

2024-11-06T08:08:06.261Z "Within buildVideoConfiguration...",

2024-11-06T08:08:06.261Z "Processing video stream id: 0, codec: h264",

2024-11-06T08:08:06.261Z "Calculated bitrate: 7424676 bps",

2024-11-06T08:08:06.261Z "Bitrate for video stream 0: 7424676 bps",

2024-11-06T08:08:06.261Z "Video stream codec is: h264",

2024-11-06T08:08:06.261Z "bitrateprobe: 7424676",

2024-11-06T08:08:06.261Z "target_pct_reduction_value: 0.5",

2024-11-06T08:08:06.261Z "target_bitrate: 2000000",

2024-11-06T08:08:06.261Z "Using target bitrate: 2000000 bps.",

2024-11-06T08:08:06.261Z "Target bitrate for output: 2000 kbps",

2024-11-06T08:08:06.261Z "Buffer size: 4000 kbps",

2024-11-06T08:08:06.261Z "Transcoding to HEVC using NVidia NVENC",

2024-11-06T08:08:06.261Z "videoSettings: -map -0:d? -map 0:0 -c:v hevc_nvenc -qmin 0 -cq:v 23 -b:v 2000k -maxrate 2000k -bufsize 4000k",

2024-11-06T08:08:06.261Z "Ending video configuration...",

2024-11-06T08:08:06.261Z "Starting audio configuration...",

2024-11-06T08:08:06.261Z "Audio languages specified: eng, und",

2024-11-06T08:08:06.261Z "Processing priority input for codec: truehd with value: 1",

2024-11-06T08:08:06.261Z "Processing priority input for codec: dts_hd_ma with value: 2",

2024-11-06T08:08:06.261Z "Processing priority input for codec: dts_hd with value: 3",

2024-11-06T08:08:06.261Z "Processing priority input for codec: dts with value: 4",

2024-11-06T08:08:06.261Z "Processing priority input for codec: atmos with value: 5",

2024-11-06T08:08:06.261Z "Processing priority input for codec: flac with value: 6",

2024-11-06T08:08:06.261Z "Processing priority input for codec: tta with value: 7",

2024-11-06T08:08:06.261Z "Processing priority input for codec: aac with value: 8",

2024-11-06T08:08:06.261Z "Processing priority input for codec: eac3 with value: 9",

2024-11-06T08:08:06.261Z "Processing priority input for codec: ac3 with value: 10",

2024-11-06T08:08:06.261Z "Processing priority input for codec: mp3 with value: 11",

2024-11-06T08:08:06.261Z "Processing priority input for codec: vorbis with value: 12",

2024-11-06T08:08:06.261Z "Processing priority input for codec: opus with value: 13",

2024-11-06T08:08:06.261Z "Processing priority input for codec: wav with value: 14",

2024-11-06T08:08:06.261Z "Processing priority input for codec: pcm_s16le with value: 15",

2024-11-06T08:08:06.261Z "Processing priority input for codec: pcm_s24le with value: 16",

2024-11-06T08:08:06.261Z "Processing priority input for codec: pcm_s32le with value: 17",

2024-11-06T08:08:06.261Z "Processing priority input for codec: wma with value: 18",

2024-11-06T08:08:06.261Z "Processing priority input for codec: ra with value: 19",

2024-11-06T08:08:06.261Z "Processing priority input for codec: ape with value: 20",

2024-11-06T08:08:06.261Z "Audio priority map: {\"truehd\":1,\"dts_hd_ma\":2,\"dts_hd\":3,\"dts\":4,\"atmos\":5,\"flac\":6,\"tta\":7,\"aac\":8,\"eac3\":9,\"ac3\":10,\"mp3\":11,\"vorbis\":12,\"opus\":13,\"wav\":14,\"pcm_s16le\":15,\"pcm_s24le\":16,\"pcm_s32le\":17,\"wma\":18,\"ra\":19,\"ape\":20}",

2024-11-06T08:08:06.261Z "Processing audio track (stream id: 1, language: eng)",

2024-11-06T08:08:06.261Z "Calculated bitrate: 640000 bps",

2024-11-06T08:08:06.261Z "Stream Details (id: 1):",

2024-11-06T08:08:06.261Z " Codec: eac3",

2024-11-06T08:08:06.261Z " Profile: unknown",

2024-11-06T08:08:06.261Z " Bitrate: 640000",

2024-11-06T08:08:06.261Z " Channels: 6",

2024-11-06T08:08:06.261Z " Layout: 5.1(side)",

2024-11-06T08:08:06.261Z " Language: eng",

2024-11-06T08:08:06.261Z " Commentary: no",

2024-11-06T08:08:06.261Z "Mapping highest priority audio track (stream id: 1, codec: eac3, priority: 9)",

2024-11-06T08:08:06.261Z "Starting audio configuration...",

2024-11-06T08:08:06.261Z "Retained audio tracks: 1",

2024-11-06T08:08:06.261Z "Processing retained audio track (ID: 1, Codec: eac3, Channels: 6, Bitrate: 640000)",

2024-11-06T08:08:06.261Z "Checking bitrate for downscaling. Original bitrate: 640000, calculated target: 576000 bps for 6 channels.",

2024-11-06T08:08:06.261Z "Audio track (stream id: 1) will be downscaled to 576 kbps with codec: eac3 and channels: 6.",

2024-11-06T08:08:06.261Z "Audio track processing completed.",

2024-11-06T08:08:06.261Z "audioSettings from function: -map 0:1 -c:a eac3 -b:a 576k -ac 6",

2024-11-06T08:08:06.261Z "Ending audio configuration...",

2024-11-06T08:08:06.261Z "Starting subtitle configuration...",

2024-11-06T08:08:06.261Z "Within Subtitle function",

2024-11-06T08:08:06.261Z "File name: /mnt/media/tv/Superman & Lois/Superman & Lois - S04E06 - When the Lights Come On - h264 EAC3 - WEBDL-1080p.mkv",

2024-11-06T08:08:06.261Z "Full stream data: {\n \"index\": 2,\n \"codec_name\": \"subrip\",\n \"codec_long_name\": \"SubRip subtitle\",\n \"codec_type\": \"subtitle\",\n \"codec_tag_string\": \"[0][0][0][0]\",\n \"codec_tag\": \"0x0000\",\n \"r_frame_rate\": \"0/0\",\n \"avg_frame_rate\": \"0/0\",\n \"time_base\": \"1/1000\",\n \"start_pts\": 0,\n \"start_time\": \"0.000000\",\n \"duration_ts\": 2547754,\n \"duration\": \"2547.754000\",\n \"disposition\": {\n \"default\": 0,\n \"dub\": 0,\n \"original\": 1,\n \"comment\": 0,\n \"lyrics\": 0,\n \"karaoke\": 0,\n \"forced\": 0,\n \"hearing_impaired\": 0,\n \"visual_impaired\": 0,\n \"clean_effects\": 0,\n \"attached_pic\": 0,\n \"timed_thumbnails\": 0,\n \"captions\": 0,\n \"descriptions\": 0,\n \"metadata\": 0,\n \"dependent\": 0,\n \"still_image\": 0\n },\n \"tags\": {\n \"language\": \"eng\",\n \"BPS\": \"71\",\n \"DURATION\": \"00:42:22.040000000\",\n \"NUMBER_OF_FRAMES\": \"731\",\n \"NUMBER_OF_BYTES\": \"22845\",\n \"_STATISTICS_WRITING_APP\": \"mkvmerge v85.0 ('Shame For You') 64-bit\",\n \"_STATISTICS_TAGS\": \"BPS DURATION NUMBER_OF_FRAMES NUMBER_OF_BYTES\"\n }\n}",

2024-11-06T08:08:06.261Z "Detected subtitle stream: ID=2, Codec=subrip",

2024-11-06T08:08:06.261Z "Retaining subtitle track in language eng (stream id: 2)",

2024-11-06T08:08:06.261Z "Full stream data: {\n \"index\": 3,\n \"codec_name\": \"subrip\",\n \"codec_long_name\": \"SubRip subtitle\",\n \"codec_type\": \"subtitle\",\n \"codec_tag_string\": \"[0][0][0][0]\",\n \"codec_tag\": \"0x0000\",\n \"r_frame_rate\": \"0/0\",\n \"avg_frame_rate\": \"0/0\",\n \"time_base\": \"1/1000\",\n \"start_pts\": 0,\n \"start_time\": \"0.000000\",\n \"duration_ts\": 2547754,\n \"duration\": \"2547.754000\",\n \"disposition\": {\n \"default\": 0,\n \"dub\": 0,\n \"original\": 1,\n \"comment\": 0,\n \"lyrics\": 0,\n \"karaoke\": 0,\n \"forced\": 0,\n \"hearing_impaired\": 1,\n \"visual_impaired\": 0,\n \"clean_effects\": 0,\n \"attached_pic\": 0,\n \"timed_thumbnails\": 0,\n \"captions\": 0,\n \"descriptions\": 0,\n \"metadata\": 0,\n \"dependent\": 0,\n \"still_image\": 0\n },\n \"tags\": {\n \"language\": \"eng\",\n \"title\": \"SDH\",\n \"BPS\": \"78\",\n \"DURATION\": \"00:42:22.040000000\",\n \"NUMBER_OF_FRAMES\": \"818\",\n \"NUMBER_OF_BYTES\": \"25091\",\n \"_STATISTICS_WRITING_APP\": \"mkvmerge v85.0 ('Shame For You') 64-bit\",\n \"_STATISTICS_TAGS\": \"BPS DURATION NUMBER_OF_FRAMES NUMBER_OF_BYTES\"\n }\n}",

2024-11-06T08:08:06.261Z "Detected subtitle stream: ID=3, Codec=subrip",

2024-11-06T08:08:06.261Z "Retaining subtitle track in language eng (stream id: 3)",

2024-11-06T08:08:06.261Z "Final subtitle settings: No settings available",

2024-11-06T08:08:06.261Z "subtitleSettings: -c:s copy -map 0:2 -map 0:3",

2024-11-06T08:08:06.261Z "Ending subtitle configuration...",

2024-11-06T08:08:06.261Z "Response.preset: -hwaccel cuda -hwaccel_output_format cuda <io> -map -0:d? -map 0:0 -c:v hevc_nvenc -qmin 0 -cq:v 23 -b:v 2000k -maxrate 2000k -bufsize 4000k -map 0:1 -c:a eac3 -b:a 576k -ac 6 -c:s copy -map 0:2 -map 0:3 -max_muxing_queue_size 9999 -bf 5 -analyzeduration 2147483647 -probesize 2147483647 -map_metadata 0 -metadata DavoProcessed=\"true\"",



