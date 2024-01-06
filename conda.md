镜像： https://mirror.tuna.tsinghua.edu.cn/help/anaconda/

常用命令：
conda env list
conda create -n openai-whisper python=3.9
conda activate openai-whisper
conda deactivate
conda remove --name openai-whisper --all

whisper 示例：
whisper 1.1-1.mp3 --model small

