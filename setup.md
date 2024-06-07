## setting up the models


```
# getting all the models and having them in a place
# %mkdir models
# %cd models
# !pip install gdown
# !git lfs install
# !gdown 154JgKpzCPW82qINcVieuPH3fZ2e0P812
# !wget https://download.pytorch.org/models/resnet18-5c106cde.pth
# !git clone https://huggingface.co/yzd-v/DWPose
# !git clone https://huggingface.co/stabilityai/sd-vae-ft-mse
# !git clone https://huggingface.co/TMElyralab/MuseTalk
# !wget https://openaipublic.azureedge.net/main/whisper/models/65147644a518d12f04e32d6f3b26facc3f8dd46e5390956a9424a650c0ce22b9/tiny.pt

# this line is download models
# !mkdir face-parse-bisent
# !cp -r resnet18-5c106cde.pth face-parse-bisent
# !cp -r 79999_iter.pth face-parse-bisent
# !mkdir whisper
# !mv tiny.pt whisper/tiny.pt
# !mv MuseTalk/musetalk .
# !mkdir dwpose
# !cp -r DWPose/dw-ll_ucoco_384.pth dwpose
# %cd /content
# !mkdir /content/drive/MyDrive/Teja_SignLangauge/musevmodels
# !mv models /content/drive/MyDrive/Teja_SignLangauge/musevmodels
```



The models should of the dir tree
```
./models/
├── musetalk
│   └── musetalk.json
│   └── pytorch_model.bin
├── dwpose
│   └── dw-ll_ucoco_384.pth
├── face-parse-bisent
│   ├── 79999_iter.pth
│   └── resnet18-5c106cde.pth
├── sd-vae-ft-mse
│   ├── config.json
│   └── diffusion_pytorch_model.bin
└── whisper
    └── tiny.pt
```



Get the driving video, if has 2 phases

Phase 1: preprocessing stage

The lip sync will be done in the mouth region, so facial box and landmarks are obtained at the begining. Instead of recomputing them all the time, it can be cached for that you need to set prepration to be true for the first time.

for doing the preparation set the data_preparation flag to True.
for changing the video please check the line no 332 in scripts/audio_inference.py.

Phase 2: Test Phase
based on the no of frames we should be able to run the realtime inference given the audio file.

```
python -m scripts.audio_inference  --batch_size 1 --audio_clips_dir data/audio 
```

the data/audio can have a single or multiple audio file, this option is given incase if the user wants to truncate the audio into multiple clips and send to the user.