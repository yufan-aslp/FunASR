## Using paraformer with ONNXRuntime

<p align="left">
    <a href=""><img src="https://img.shields.io/badge/Python->=3.7,<=3.10-aff.svg"></a>
    <a href=""><img src="https://img.shields.io/badge/OS-Linux%2C%20Win%2C%20Mac-pink.svg"></a>
</p>

### Introduction
- Model comes from [speech_paraformer](https://www.modelscope.cn/models/damo/speech_paraformer-large_asr_nat-zh-cn-16k-common-vocab8404-pytorch/summary).


### Steps:
1. Download the whole directory
```shell
git clone https://github.com/alibaba/FunASR.git && cd FunASR
cd funasr/runtime/python/onnxruntime/paraformer/rapid_paraformer
```
2. Install the related packages.
   ```bash
   pip install -r requirements.txt
   ```
3. Export the model.
    - Export your model([docs](https://github.com/alibaba-damo-academy/FunASR/tree/main/funasr/export))

4. Run the demo.
   - Model_dir: the model path, which contains `model.onnx`, `config.yaml`, `am.mvn`.
   - Input: wav formt file, support formats: `str, np.ndarray, List[str]`
   - Output: `List[str]`: recognition result.
   - Example:
        ```python
        from paraformer_onnx import Paraformer

        model_dir = "/nfs/zhifu.gzf/export/damo/speech_paraformer-large_asr_nat-zh-cn-16k-common-vocab8404-pytorch"
        model = Paraformer(model_dir, batch_size=1)

        wav_path = ['/nfs/zhifu.gzf/export/damo/speech_paraformer-large_asr_nat-zh-cn-16k-common-vocab8404-pytorch/example/asr_example.wav']

        result = model(wav_path)
        print(result)
        ```

## Speed

Environment：Intel(R) Xeon(R) Platinum 8163 CPU @ 2.50GHz
Test [wav](https://isv-data.oss-cn-hangzhou.aliyuncs.com/ics/MaaS/ASR/test_audio/asr_example_zh.wav)

| Backend |   RTF  |
|:-------:|:------:|
| Pytorch |  0.110 |
|  Onnx   | 0.038  |


## Acknowledge
1. We acknowledge [SWHL](https://github.com/RapidAI/RapidASR) for contributing the onnxruntime(python api).
