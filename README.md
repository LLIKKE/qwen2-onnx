### 说明
- 本项目实现导出qwen2的onnx格式，并实现直接使用onnx格式进行推理。
- 该项目来自于[https://github.com/Tlntin/qwen-ascend-llm](https://github.com/Tlntin/qwen-ascend-llm)，仅保留onnx格式转换与推理部分。
- 感谢作者[https://github.com/Tlntin](https://github.com/Tlntin)开源代码支持入门学习。
### 使用方法


1. 下载qwen1.5/qwen2的模型，选择chat模型或者instruct模型，将其放到项目根目录，仅支持huggingface下载的模型，网络不好的可以用镜像站：https://hf-mirror.com/Qwen


2. 安装相应版本代码库
  ```bash
  pip install -r ./requirements.txt
  ```


3. `export/test_pytorch_run.py` 以运行pytorch版本qwen2。


3. 导出onnx，默认kv-cache长度为1024，可以根据自己的内存、显存来设置更大参数。
  ```bash
  python3 export/export_onnx.py \
    --hf_model_dir="./Qwen2-1.5B-Instruct" \
    --onnx_model_path="./output/onnx/qwen2_1.5b_chat.onnx" \
    --kv_cache_length=1024
  ```

3. `export/test_onnx_run.py`以运行onnx模型，检查输出。


4. 运行onnx，返回项目根目录，运行cli_chat.py，测试一下onnx对话是否正常（注意：由于是cpu运行，所以速度较慢，请耐心等待）。
  ```bash
  python3 ./cli_chat.py \
    --session_type=onnx \
    --hf_model_dir="./download/Qwen2-1.5B-Instruct" \
    --onnx_model_path="./output/onnx/qwen2_1.5b_chat.onnx"
  ```


