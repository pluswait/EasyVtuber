# EasyVtuber
![](assets/sample_luda.gif)

利用Facial landmark和GAN的Character Face Generation
请在Google Meets, Zoom等用自己独有的网络漫画，漫画人物进行对话!
饰品加多少都能正常工作!
不幸的是，RTX 2070以下可能无法实时启动

<br/><br/>

## Demo
![](assets/sample_luda_debug.gif)
![](assets/sample_zoom.gif)

<br/><br/>

## Requirements
- Python >= 3.8 
- Pytorch >= 1.7 
- pyvirtualcam
- mediapipe
- opencv-python

<br/><br/>

## Quick Start
- ※ 这个项目在使用前必须先安装OBS
- 请一定要遵守下面的设置顺序!

1. [OBS studio 设置](<https://obsproject.com/ko>)
   - 为了使用OBS virtualcam，首先要安装OBS Studio
2. ```pip install -r requirements.txt```
   - 必须安装OBS virtualcam才能正常安装并使用requirements中包含的pyvirtualcam
3. [pretrianed model download](<https://www.dropbox.com/s/tsl04y5wvg73ij4/talking-head-anime-2-model.zip?dl=0>)
   - 请把下面的文件放进pretrained folder
     - `combiner.pt`
     - `eyebrow_decomposer.pt`
     - `eyebrow_morphing_combiner.pt`
     - `face_morpher.pt`
     - `two_algo_face_rotator.pt`
4. 请把character image放进character folder
   - character image文件必须满足以下条件
     - 包含alpha频道(png扩展名)
     - 一个人形的角色
     - 正面
     - 角色的头部将在128x128 pixel内(因为基本是256 x 256是resize，所以256 x 256必须是128x128)
    
    <p align="center">
        <img src="./assets/img.png" alt="Example image is refenced by TalkingHeadAnime2" width="50%" height="50%"/>
    </p>


5.`python main.py --webcam_output`
   - 如果你想看看实际的facial feature是怎么捕捉的，请单击 debug 选项来执行


<br/><br/>

## How to make Custom Character
1. 请在naver、谷歌等网站上寻找自己喜欢的角色!
-请尽量满足上面四个条件!
![google search](assets/01_sample_search.gif)
<br/><br/>
2. 在找到的图片中，为了让角色的脸向中央，请以长宽1:1的比例剪掉!
-[形象剪切网站](https://iloveimg/ko/crop-image)
![crop image](assets/02_sample_crop.gif)
<br/><br/>
3. 删除图像背景，创建alpha频道!
   - [背景去除网站](https://remove.bg/ko)
![google search](assets/03_sample_remove_backgroud.gif)
<br/><br/>
4. 完成!
   - 将图像放入character folder `python main.py --output_webcam --character (.png_之外的_角色文件名)` 继续!

<br/><br/>

## Folder Structure

```
      │
      ├── character/ - character images 
      ├── pretrained/ - save pretrained models 
      ├── tha2/ - Talking Head Anime2 Library source files 
      ├── facial_points.py - facial feature point constants
      ├── main.py - main script to excute
      ├── models.py - GAN models defined
      ├── pose.py - process facial landmark to pose vector
      └── utils.py - util fuctions for pre/postprocessing image
```

<br/><br/>

## Usage
### 传送到webcam时
- `python main.py --output_webcam`
### 指定角色
- `python main.py --character (除character folder 中.png以外的角色文件名称)`
### facial feature 확인 시
- `python main.py --debug`
### 视频文件 inference
- `python main.py --input video 文件路径 --output_dir frame_要保存的_目录`

<br/><br/>

## TODOs
- [ ] Add eyebrow feature 
- [ ] Parameter Controller GUI 
- [ ] Automation of Making Drivable Character 

<br/><br/>

## Thanks to
- `이루다` 이미지 사용을 허락해주신 [스캐터랩 이루다팀](https://scatterlab.co.kr), `똘순이 MK1` 이미지 사용을 허락해주신 [순수한 불순물](https://pixiv.net/users/21097691) 님, 늦은 밤까지 README 샘플 영상 만들기 위해 도와주신 [성민석 멘토님](https://github.com/minsuk-sung), [박성호](https://github.com/naem1023), [박범수](https://github.com/hanlyang0522) 캠퍼님, 프로젝트 방향성 조언을 해주신 [김보찬 멘토님](https://github.com/MoMentum99) 모두 감사합니다!

<br/><br/>

## Acknowledgements
- EasyVtuber [TalkingHeadAnime2](<https://github.com/pkhungurn/talking-head-anime-2-demo>)基于. 
- 请确认并使用tha2 folder의 source와 pretrained model file은 원저작자 repo의 Liscense
