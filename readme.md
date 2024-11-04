# 原github项目
https://github.com/NVlabs/instant-ngp

# 项目环境
按照requirements.txt进行安装
在上传的内容中缺失dependencies，和build需要重新去原项目中下载。


# 已有的数据
有一段围绕着充电器头旋转的视频
有一段围绕着巧克力包装袋旋转的视频
有四段在腹腔模型旋转的视频
视频路径在:S:\baidu\sjwlab\chenyinda\project\腹腔3D建模\data

# 项目使用
使用Developer Command Prompt
conda activate ngp
J盘yinda\npg-end\intstant-ngp-master
1.视频转图片
.\scripts\convert_video.py --input 视频路径 --output 图片存放路径 --show_image 1 --scale 2(分辨率缩小2倍) --fps_output 5

(分辨率缩小2倍)(每5帧保存一张图片)

2.colmap重建(colmap在J盘yinda\soft\colmap\COLMAP-3.9.1-windows-cuda中)

进行Colmap重建，分别进行特征提取、匹配、稀疏重建，导出稀疏模型文件。
打开Colmap，点击file--->new project，在自定义数据文件夹下创建database文件，图片来源选择images文件夹，点击Save。
 随后点击Processing---Feature extraction，不需要更改任何数据，直接点Extract即可。
然后选择Processing---Feature matching，同样不需要更改任何数据，点击Run。
点击Reconstruction---Start reconstruction进行重建。 

在自定义数据集文件夹下新建sparse\0文件夹（注意！一定要按照这个命名，否则后边会出错），点击File---export model as text，将重建数据放到sparse\0文件夹中。 

原文链接：https://blog.csdn.net/MARCOLU6/article/details/129987714


3.将colmap输出文件转成模型需要的transforms.json文件
python .\scripts\colmap2nerf.py --aabb_scale 16 --images .\scripts\image --text .\scripts\sparse\0 --out 
图片路径 colmap输出文件 输出路径

4.运行
.\build\testbed.exe --mode nerf --scene trainsforms.json路径


