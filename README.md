# Tbbox

A extreme tiny building sandbox to compile or runing programs without dirty your host

# Installation

- Install dependency 'bubllewrap'

    for Arch user: `pacman -S bubblewrap`

    for Fedora user: `dnf install bubblewrap`

    for Debian user: `apt install bubblewrap`

- Just put file 'tbbox' in your '$PATH', suggest under '/usr/bin'.


# What does this script do

- fix 'Argument List too long' error
- find out the dirty file created by unknown program

If you has any idea, an issue is welcome!

# How to use?

Just entering your project directory, then type `tbbox` in terminal, and 
the terminal will enter into sandbox mode

Use `tbbox -c` to find out the file created in sandbox

If you want to quit, just type `exit` in shell, only file in project directory will be kept.

# Function1: fix 'Argument List too long' error

This error often occur with third party 'OpenWrt' project. Because they often use the command below

`echo ${rm-files}} | xargs rm -f `

If your project path prefix is too long, for example:

`/home/code-server/project/EmbeddedProject/openwrt`

The command will become

```
rm -f /home/code-server/project/EmbeddedProject/openwrt/a.txt /home/code-server/project/EmbeddedProject/openwrt/b.txt ...
```

It is very easy to occur 'Argument List too long' error, and this error cannot be easily fix by changing system configure file

Use 'tbbox -s' can solve this problem

```
[code-server@suzakuwcx-server openwrt]$ tbbox -s
==> warp from '/home/code-server/project/EmbeddedProject/openwrt' to '/home/code-server/openwrt'

(tbbox) [code-server@suzakuwcx-server openwrt]$ pwd
/home/code-server/openwrt
```

# Function2: find out the dirty file

Do you has the following troubles?

- Running an unknown program and worry about the program will write some file into your host?

Don't worry! This shell script wil find out those file, for example:

```
[code-server@suzakuwcx-server funasr]$ tbbox 
==> warp from '/home/code-server/project/PythonProject/asr/funasr' to '/home/code-server/project/PythonProject/asr/funasr'

(tbbox) [code-server@suzakuwcx-server funasr]$ ./venv/bin/python vad.py 
2024-03-29 11:56:39,331 - modelscope - INFO - PyTorch version 2.1.1 Found.
2024-03-29 11:56:39,331 - modelscope - INFO - Loading ast index from /home/code-server/.cache/modelscope/ast_indexer
2024-03-29 11:56:39,332 - modelscope - INFO - No valid ast index found from /home/code-server/.cache/modelscope/ast_indexer, generating ast index from prebuilt!
2024-03-29 11:56:39,433 - modelscope - INFO - Loading done! Current index file version is 1.10.0, with md5 7b3836bb1ffab40ed1ea4b37aa5f0537 and a total number of 946 components indexed
2024-03-29 11:56:44,453 - modelscope - WARNING - Model revision not specified, use revision: v1.2.0
Downloading: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 518/518 [00:00<00:00, 3.86MB/s]
Downloading: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 15.1k/15.1k [00:00<00:00, 354kB/s]
...
...
(tbbox) [code-server@suzakuwcx-server funasr]$ tbbox -c
/tmp/tmp4sfzc4ej
/tmp/tmp4sfzc4ej/vad_example.wav
/home/code-server/.cache
/home/code-server/.cache/YAPF
/home/code-server/.cache/YAPF/0.40.2
/home/code-server/.cache/YAPF/0.40.2/Grammar-py3.10.13.final.0.pickle
/home/code-server/.cache/YAPF/0.40.2/PatternGrammar-py3.10.13.final.0.pickle
/home/code-server/.cache/modelscope
/home/code-server/.cache/modelscope/ast_indexer
/home/code-server/.cache/modelscope/hub
/home/code-server/.cache/modelscope/hub/temp
/home/code-server/.cache/modelscope/hub/damo
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/.mdl
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/configuration.json
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/.msc
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/README.md
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/fig
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/fig/struct.png
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/vad.mvn
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/vad.pb
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/vad.yaml
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/example
/home/code-server/.cache/modelscope/hub/damo/speech_fsmn_vad_zh-cn-16k-common-pytorch/example/vad_example.wav
/home/code-server/.cache/huggingface
/home/code-server/.cache/huggingface/hub
/home/code-server/.cache/huggingface/hub/version.txt
/home/code-server/.modelscope
/home/code-server/.modelscope/credentials
/home/code-server/.modelscope/credentials/session
(tbbox) [code-server@suzakuwcx-server funasr]$ 
```
