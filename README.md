<div align="center">
  <img width="100%" height="100%" src="docs/images/Vitis-AI.png">
</div>

<br />
Xilinx&reg; Vitis&trade;AI는 에지 장치와 Alveo 카드를 포함한 Xilinx 하드웨어 플랫폼에서 사용하는 AI 인퍼런스를 위한 개발 스택입니다.

최적화된 IP, 도구, 라이브러리, 모델 및 예제 디자인으로 구성됩니다.
고효율과 사용 편의성을 염두에두고 설계되어 Xilinx FPGA 및 ACAP에서 AI 가속의 잠재력을 최대한 발휘합니다.
<br />
<br />

<div align="center">
  <img width="45%" height="45%" src="docs/images/Vitis-AI-arch.png">
</div>

<br />
Vitis AI is composed of the following key components:

* **AI 모델 Zoo**  - Xilinx 장치에 배포할 준비가 된 사전 최적화 모델 세트입니다.
* **AI 옵티마이저** - 모델을 최대 90%까지 정리할 수있는 선택적 모델 최적화 프로그램입니다. 상업용 라이센스와 별도로 사용할 수 있습니다.
* **AI 퀀타이저** - 모델 양자화, 보정 및 미세 조정을 지원하는 강력한 퀀타이저입니다.
* **AI 컴파일러** - 양자화 된 모델을 고효율 명령 세트 및 데이터 흐름으로 컴파일합니다.
* **AI 프로파일러** - AI 추론 구현의 효율성 및 활용도에 대한 심층 분석을 수행합니다.
* **AI 라이브러리** - 엣지에서 클라우드까지 AI 애플리케이션을 위한 높은 수준의 최적화된 C++ API를 제공합니다.
* **DPU** - 효율적이고 확장 가능한 IP 코어는 다양한 애플리케이션의 요구 사항을 충족하도록 사용자 정의할 수 있습니다.
  * 사용 가능한 다양한 DPU에 대한 자세한 내용은 [DPU Naming](docs/learn/dpu_naming.md)을 참조하십시오.


**더 알아보기:** [Vitis AI Overview](https://www.xilinx.com/products/design-tools/vitis/vitis-ai.html)  


## [새로운 기능 보기](docs//learn/release_notes.md)
- [릴리즈 노트](docs//learn/release_notes.md)

## 시작

Vitis AI 도구 및 리소스로 컨테이너를 설치하기 위해 두 가지 옵션을 사용할 수 있습니다.

 - Docker Hub에 있는 사전 빌드된 컨테이너: [xilinx/vitis-ai](https://hub.docker.com/r/xilinx/vitis-ai/tags)
 - Docker 레시피를 사용하여 로컬에서 컨테이너 빌드: [Docker Recipes](setup/docker)


### 설치
 - 아직 Docker가 없는 경우에는 [Docker를 설치해주세요](docs/install_docker/README.md)

 - [리눅스 사용자가 Docker를 사용할 수 있게 해 주세요](https://docs.docker.com/install/linux/linux-postinstall/)

 - Vitis-AI 저장소를 복제하여 예제, 참조 코드 및 스크립트를 얻으세요
    ```bash
    git clone --recurse-submodules https://github.com/Xilinx/Vitis-AI  

    cd Vitis-AI
    ```

#### 사전 빌드된 Docker 이미지 사용

아래 명령을 사용해 최신 Vitis AI 이미지를 다운로드하십시오.
이 컨테이너는 CPU에서 작동합니다.  
```
docker pull xilinx/vitis-ai-cpu:latest  
```

Docker를 실행하려면 다음 명령을 사용하십시오:
```
./docker_run.sh xilinx/vitis-ai-cpu:latest
```
#### 레시피에서 Docker 빌드

There are two types of docker recipes provided - CPU recipe and GPU recipe. If you have a compatible nVidia graphics card with CUDA support, you could use GPU recipe; otherwise you could use CPU recipe.
제공되는 도커 레시피에는 CPU 레시피와 GPU 레시피의 두 가지 유형이 있습니다.
CUDA를 지원하는 호환되는 NVIDIA 그래픽 카드를 가지고 있는 경우 GPU 레시피를 사용할 수 있습니다. 그렇지 않으면 CPU 레시피를 사용하면 됩니다.

**CPU Docker**

아래 명령을 사용하여 CPU 도커를 빌드하십시오.:
```
cd setup/docker
./docker_build_cpu.sh
```
CPU 도커를 실행하려면 다음 명령을 사용하십시오:
```
./docker_run.sh xilinx/vitis-ai-cpu:latest
```
**GPU Docker**

GPU Docker 빌드:
```
cd setup/docker
./docker_build_gpu.sh
```
GPU Docker 실행:
```
./docker_run.sh xilinx/vitis-ai-gpu:latest
```
Please use the file **./docker_run.sh** as a reference for the docker launching scripts, you could make necessary modification to it according to your needs.
More Detail can be found here: [Run Docker Container](docs/install_docker/load_run_docker.md)

**X11 Support for Running Vitis AI Docker with Alveo**

If you are running Vitis AI docker with Alveo card and want to use X11 support for graphics (for example, some demo applications in VART and Vitis-AI-Library for Alveo need to display images or video), please add following line into the *docker_run_params* variable definition in *docker_run.sh* script:

~~~
-e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/.Xauthority:/tmp/.Xauthority \
~~~

And after the docker starts up, run following command lines:

~~~
cp /tmp/.Xauthority ~/
sudo chown vitis-ai-user:vitis-ai-group ~/.Xauthority
~~~

Please note before running this script, please make sure either you have local X11 server running if you are using Windows based ssh terminal to connect to remote server, or you have run **xhost +** command at a command terminal if you are using Linux with Desktop. Also if you are using ssh to connect to the remote server, remember to enable *X11 Forwarding* option either with Windows ssh tools setting or with *-X* options in ssh command line.



 ### Get Started with Examples
  - [VART](demo/VART/README.md)
  - [Vitis AI Library](demo/Vitis-AI-Library/README.md)
  - [Examples](examples/README.md)
  - [Vitis AI DNNDK samples](demo/DNNDK)


## Programming with Vitis AI

Vitis AI offers a unified set of high-level C++/Python programming APIs to run AI applications across edge-to-cloud platforms, including DPU for Alveo, and DPU for Zynq Ultrascale+ MPSoC and Zynq-7000. It brings the benefits to easily port AI applications from cloud to edge and vice versa. 8 samples in [VART Samples](demo/VART) are available to help you get familiar with the unfied programming APIs.


| ID | Example Name          | Models              | Framework  | Notes                                                                     |
|----|-----------------------|---------------------|------------|---------------------------------------------------------------------------|
| 1  | resnet50              | ResNet50            | Caffe      | Image classification with VART C\+\+ APIs\.                   |
| 2  | resnet50\_mt\_py      | ResNet50            | TensorFlow | Multi\-threading image classification with VART Python APIs\. |
| 3  | inception\_v1\_mt\_py | Inception\-v1       | TensorFlow | Multi\-threading image classification with VART Python APIs\. |
| 4  | pose\_detection       | SSD, Pose detection | Caffe      | Pose detection with VART C\+\+ APIs\.                         |
| 5  | video\_analysis       | SSD                 | Caffe      | Traffic detection with VART C\+\+ APIs\.                      |
| 6  | adas\_detection       | YOLO\-v3            | Caffe      | ADAS detection with VART C\+\+ APIs\.                         |
| 7  | segmentation          | FPN                 | Caffe      | Semantic segmentation with VART C\+\+ APIs\.                  |
| 8  | squeezenet\_pytorch   | Squeezenet          | Pytorch    | Image classification with VART C\+\+ APIs\.                   |

For more information, please refer to [Vitis AI User Guide](https://www.xilinx.com/html_docs/vitis_ai/1_3/zmw1606771874842.html)


## References
- [Vitis AI Overview](https://www.xilinx.com/products/design-tools/vitis/vitis-ai.html)
- [Vitis AI User Guide](https://www.xilinx.com/html_docs/vitis_ai/1_3/zmw1606771874842.html)
- [Vitis AI Model Zoo with Performance & Accuracy Data](models/AI-Model-Zoo)
- [Vitis AI Tutorials](https://github.com/Xilinx/Vitis-In-Depth-Tutorial/tree/master/Machine_Learning)
- [Developer Articles](https://developer.xilinx.com/en/get-started/ai.html)

## [System Requirements](docs/system_requirements.md)

## Questions and Support
- [FAQ](docs/faq.md)
- [Vitis AI Forum](https://forums.xilinx.com/t5/AI-and-Vitis-AI/bd-p/AI)
- [Third Party Source](docs/Thirdpartysource.md)

[models]: docs/models.md
[Amazon AWS EC2 F1]: https://aws.amazon.com/marketplace/pp/B077FM2JNS
[Xilinx Virtex UltraScale+ FPGA VCU1525 Acceleration Development Kit]: https://www.xilinx.com/products/boards-and-kits/vcu1525-a.html
[AWS F1 Application Execution on Xilinx Virtex UltraScale Devices]: https://github.com/aws/aws-fpga/blob/master/SDAccel/README.md
[Release Notes]: docs/release-notes/1.x.md
[UG1023]: https://www.xilinx.com/support/documentation/sw_manuals/xilinx2017_4/ug1023-sdaccel-user-guide.pdf
[FAQ]: docs/faq.md
[ML Suite Overview]: docs/ml-suite-overview.md
[Webinar on Xilinx FPGA Accelerated Inference]: https://event.on24.com/wcc/r/1625401/2D3B69878E21E0A3DA63B4CDB5531C23?partnerref=Mlsuite
[Vitis AI Forum]: https://forums.xilinx.com/t5/AI-and-Vitis-AI/bd-p/AI
[ML Suite Lounge]: https://www.xilinx.com/products/boards-and-kits/alveo/applications/xilinx-machine-learning-suite.html
[Models]: https://www.xilinx.com/products/boards-and-kits/alveo/applications/xilinx-machine-learning-suite.html#gettingStartedCloud
[whitepaper here]: https://www.xilinx.com/support/documentation/white_papers/wp504-accel-dnns.pdf

   ```
