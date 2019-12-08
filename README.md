# NeFFmpegCommand FFmpeg������⣨Windows)
## һ������
### 1.1 ��Ƶ�������ܹ�
![image](https://github.com/tianyalu/NeFFmpegCommand/blob/master/show/video_structure.png)
### 1.2 ��Ⱦ����
![image](https://github.com/tianyalu/NeFFmpegCommand/blob/master/show/rendering_process.png)

## ����׼������
* ��[http://ffmpeg.org/download.html](http://ffmpeg.org/download.html)����FFmpeg Windows�汾����ѹ  
* �ѽ�ѹ·��`D:\CommonDev\FFmpeg\FFmpegWindows\ffmpeg-20191207-70e292b-win64-static\bin`���ӵ�����������

## ����FFmpeg��������
### 3.1 FFmpeg¼������
`ffmpeg -f gdigrab -framerate 30 -offset_x 0 -offset_y 0 -video_size 1920*1080 -i desktop out.mpg`  
> gdigrab������ͨ��gdiץ���ķ�ʽ��mac�� avfoundation)  
> -framerate 30����ʾ¼�Ƶ�֡��Ϊ30  
> -offset_x������ƫ����x  
> -offset_y������ƫ����y  
> -video_size����Ҫ¼�ƵĿ��Ⱥ͸߶ȣ�����¼�Ƶ���������Ļ  
> -i������·���������Լ���ʽmpg  
> desktop������FFmpeg����¼�Ƶ�����Ļ��������һ�����ڣ�����¼��һ�����ڣ��������ô��ڵ�ID��  
`Ctrl + c` ȡ��¼������  

### 3.2 FFmpeg�ֽ⸴������
���壺����������Ƶ�ļ����в�֣�����ֵ���Ϣ��Ϊ�زģ��ϳ�����Ҫ������Ƶ��  
#### 3.2.1 ��ȡ��Ƶ��
`ffmpeg -i input.mp4 -acodec copy -vn out.aac`  
> acodec��ָ����Ƶ��������copy ָ��ֻ���������������  
> vn��v������Ƶ��n����noҲ��������Ƶ����˼  
#### 3.2.2 ��ȡ��Ƶ��
`ffmpeg -i input.mp4 -vcodec copy -an out.h264`  
> vcodec��ָ����Ƶ��������copy ָ��ֻ���������������  
> an��a������Ƶ��n����noҲ��������Ƶ����˼  
#### 3.2.3 �ϳ���Ƶ
`ffmpeg -i out.h264 -i out.aac -vcodec copy -acodec copy out.mp4`  

### 3.3 FFmpeg����ԭʼ��������
���壺��ȡδ��������Ļ������Ƶ��������Ϣһ��Ϊyuv����Ƶ��ϢΪpcm��  
#### 3.3.1 ��ȡYUV����
`ffmpeg -i input.mp4 -an -c:v rawvideo -pix_fmt yuv420p out.yuv`  
> -c:v rawvideo ָ������Ƶת��ԭʼ����  
> -pixel_format yuv420p ָ��ת����ʽΪyuv420p  
δ���������������Ҫ�õ�ffplay���ţ�`ffplay -video_size 1920*1080 out.yuv`  
**�������⣺**  
���ô��ַ�ʽ��ȡ����ƵԴ�ļ�����ʱ�ٶ����Լӿ�ܶ࣬��֪�ιʣ�  
#### 3.3.2 ��ȡPCM���� 
`ffmpeg -i input.mp4 -vn -ar 44100 -ac 2 -f s16le out.pcm`  
> -ar��ָ����Ƶ������44100 ��44.1KHz  
> -ac��ָ����Ƶ����channel 2 Ϊ˫����  
> -f�����ݴ洢��ʽ s��Signed �з��ŵģ�16��ÿһ����ֵ��16λ��ʾ��l��little��e��end  
δ���������������Ҫ�õ�ffplay���ţ�`ffplay -ar 44100 -ac 2 -f s16le out.pcm`  

### 3.4 FFmpeg�˾�����
�˾�ʵ�ֹ������£�  
![image](https://github.com/tianyalu/NeFFmpegCommand/blob/master/show/ffmpeg_filter.png)

#### 3.4.1 �ü��˾�
`ffmpeg -i input.mp4 -vf crop=in_w-200:in_h-200 -c:v libx264 -c:a copy crop.mp4`  
> crop=in_w-200:in_h-200 �ü���Ƶ��Ŀ��ߣ���������Ƶԭ���Ŀ���-200��  
> -c:v libx264 ͨ��libx264���������б���  
> -c:a copy ����Ƶֱ�ӽ��п���
#### 3.4.2 ��ȡPCM����
`ffmpeg -i input.mp4 -vn -ar 44100 -ac 2 -f s16le out.pcm`

### 3.5 ��ʽת������
`ffmpeg -i out.mp4 -vcodec copy -acodec copy out.flv`  