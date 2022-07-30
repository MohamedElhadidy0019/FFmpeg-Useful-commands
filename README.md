# Repo to save most common FFmpeg commands



## repeat an image and output it as a video

`ffmpeg -loop 1 -i in.png -c:v libx264 -t 15 -pix_fmt yuv420p -vf scale=1280:720 out.mp4`


## change the format of a picture or video
` ./ffmpeg -i in.jpg -preset ultrafast out.png`

## use accelrated Cuda chroma key filter

`
ffmpeg -v verbose
-hwaccel cuda -hwaccel_output_format cuda -i input_chroma_video.mp4  
-hwaccel cuda -hwaccel_output_format cuda -i overlay_video.mp4 
-init_hw_device cuda 
-filter_complex 
" 
[0:v]chromakey_cuda=0x25302D:0.1:0.12:1[overlay_video];
[1:v]scale_cuda=format=yuv420p[base];
[base][overlay_video]overlay_cuda" \
-an -sn -c:v h264_nvenc -cq 20 overlay_test.mp4
`



