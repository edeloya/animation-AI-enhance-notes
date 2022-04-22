This is going to be mostly stream of consciousness until/if I decide to turn this into something. This project is to see how well video enhancing models have progressed about 2 years since the last time I put out something I was happy enough to keep. In the past, I was using [Video2x](https://github.com/k4yt3x/video2x) (and in the before-before times, I was using .bat scripts, [waifu2x](https://github.com/nagadomi/waifu2x), and ffmpeg to compile frames into video - we don't talk about those dark times) to upscale great media that hasn't held up to now or that could only be found as second-hand encodes from decades ago. Animation has always been the only real viable genre for this, although the last year or two Ive seen others using super resolution upscaling frameworks on non-animation. For this, Im using Topaz Video Enhance AI, since it's been leading in quality output in compartison to the free, OSS. I may try to use an updated version of Real-ESRGAN to compare eventually but as of now (early 2022), Topaz is my pick.

Topaz Video Enhance AI:

    •Proteus - Fine Tune
    •Model Parameters - 100 44 35 41 63 38
    •Grain - 1.0 - 1.0
    


![image](https://user-images.githubusercontent.com/54195989/154736019-5154f0e9-a167-410c-b0bc-a5405112d80e.png)

Mediainfo claims this is progressive and constant FPS, meaning I shouldnt expect any interla-

![image](https://user-images.githubusercontent.com/54195989/154736402-9a668a0f-ae70-41bf-9ac7-83740e0bed13.png)
<img src="https://user-images.githubusercontent.com/54195989/154736522-69b059c3-fd85-417d-9afc-9d8bded5f378.png" height="297">

<br>(I actually only noticed the interlacing after a few test runs comparing settings and models 😅)











Here's some of the initial "quality" tests:<br>
<p float="left">

<img src="https://user-images.githubusercontent.com/54195989/154741823-683e611a-001a-42c0-b014-458cae973347.png" width=49.75% />
<img src="https://user-images.githubusercontent.com/54195989/154741825-82cf06bf-942b-48d8-84b8-599b835e9b27.png" width=49.75% /> 
<br>
<br>
<img src="https://user-images.githubusercontent.com/54195989/154743865-be46b7c0-eec1-4721-be32-af8b6c4a93cb.png" width=49.75% />
<img src="https://user-images.githubusercontent.com/54195989/154743867-213cd5b2-1b6b-4544-af89-3a11bf554a2d.png" width=49.75% />
<br>
<br>
<img src="https://user-images.githubusercontent.com/54195989/154743889-298f80b5-0fc0-4bef-8541-bd83f14b7427.png" width=49.75% />
<img src="https://user-images.githubusercontent.com/54195989/154743888-d4e8e427-3588-46c6-8236-805ac652d252.png" width=49.75% />
<br>
<br>
<img src="https://user-images.githubusercontent.com/54195989/154743901-91bfc8a5-b925-4dfd-83d6-d61d2a16b477.png" width=49.75% />
<img src="https://user-images.githubusercontent.com/54195989/154743899-807746ed-bea7-497d-b58e-6117bdabb5b1.png" width=49.75% />
<br>
<br>
<img src="https://user-images.githubusercontent.com/54195989/154743917-8adab5d4-d654-4e3a-b201-ea027ab55850.png" width=49.75% />
<img src="https://user-images.githubusercontent.com/54195989/154743916-33a61be5-1eaa-4de4-a967-d1d2d6aa7930.png" width=49.75% />
<br>
<br>
<img src="https://user-images.githubusercontent.com/54195989/154743934-e3f99866-1dd6-4cd2-bd2f-02eefe5f2f41.png" width=49.75% />
<img src="https://user-images.githubusercontent.com/54195989/154743937-bfe553cc-1dbc-47c4-a01b-5fe2bc50f797.png" width=49.75% />
<br>
<br>
<img src="https://user-images.githubusercontent.com/54195989/154743953-b2f7cc26-7c4e-4f02-9b04-0a0d15b4b80d.png" width=49.75% />
<img src="https://user-images.githubusercontent.com/54195989/154743954-b4e74a85-3375-4b64-af3a-7f30cc11657c.png" width=49.75% />
<br>
<br>
<img src="https://user-images.githubusercontent.com/54195989/154743995-263fb414-a6b0-46e4-ba67-e1dbabdfd196.png" width=49.75% />
<img src="https://user-images.githubusercontent.com/54195989/154743996-f615b28a-5616-48a9-8f1d-6ce632454661.png" width=49.75% />
<br>
<br>
<img src="https://user-images.githubusercontent.com/54195989/154744010-620094d7-5181-4fb4-b84f-21224167a166.png" width=49.75% />
<img src="https://user-images.githubusercontent.com/54195989/154744009-407cc155-b2e4-4d79-bb3e-01d91005028d.png" width=49.75% />
<br>
<br>
</p>

```
ffmpeg `
-r 24000/1001 -i '<INPUT>' `
-r 24000/1001 -i '<INPUT>' `
-filter_complex "[0]crop=iw/2:ih:0:0[left];`
[1]crop=iw/2:ih:iw/2:0[right];`
[left][right]scale2ref[old][new];`
[old]pad=(iw+2):color=red[L];`
[L][new]hstack=inputs=2[all]" `
-map "[all][1:a]" -c:v libx265 -preset slow -crf 24 `
-c:a libopus -b:a 128k '<OUTPUT>' -y
```
    
Refs/related:
<br>[DeInterlacing/DeTelecining Guide](https://www.techpowerup.com/forums/threads/hats-ntsc-guide-to-dvd-bd-ripping.221062/)
<br>[AviSynth101](https://www.l33tmeatwad.com/avisynth101)
