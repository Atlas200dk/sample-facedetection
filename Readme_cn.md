中文|[English](Readme.md)

# 人脸检测<a name="ZH-CN_TOPIC_0232337872"></a>

开�者�以将本application部署至Atlas 200DK上实现对摄�头数�的实时采集�并对视频中的人脸信�进行预测的功能。

当�分支中的应用适�**1.32.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="zh-cn_topic_0228461904_section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。
-   已完�Atlas 200 DK开�者�与Mind Studio的连接，交�编译器的安装，SD�的制作�基本信�的�置等。

## 部署<a name="zh-cn_topic_0228461904_section412811285117"></a>

�以选择如下快速部署或者常规方法部署，二选一��：

1.  快速部署，请�考：  [https://github.com/Atlas200dk/faster-deploy](https://github.com/Atlas200dk/faster-deploy)  。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   该快速部署脚本�以快速部署多个案例，请选择人脸检测案例部署��。  
    >-   该快速部署脚本自动完�了代�下载�模型转��环境���置等�程，如果需�了解详细的部署过程请选择常规部署方�。转：**[2. 常规部署](#zh-cn_topic_0228461904_li3208251440)**  

2.  <a name="zh-cn_topic_0228461904_li3208251440"></a>常规部署，请�考：  [https://github.com/Atlas200dk/sample-README/tree/master/sample-facedetection](https://github.com/Atlas200dk/sample-README/tree/master/sample-facedetection)  。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   该部署方�，需�手动完�代�下载�模型转��环境���置等过程。完��，会对其中的过程更加了解。  


## 编译<a name="zh-cn_topic_0228461904_section7994174585917"></a>

1.  打开对应的工程。

    以Mind Studio安装用户在命令行中进入安装包解压�的“MindStudio-ubuntu/bin�目录，如：$HOME/MindStudio-ubuntu/bin。执行如下命令�动Mind Studio。

    **./MindStudio.sh**

    �动�功�，打开**sample-facedetection**工程，如[图 打开facedetection工程](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig05481157171918)所示。

    **图 1**  打开facedetection工程<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig05481157171918"></a>  
    

    ![](figures/打开工程项目-人脸检测.png)

2.  在**src/param\_configure.conf**文件中�置相关工程信�。

    如[图 �置文件路径](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig0391184062214)所示。

    **图 2**  �置文件<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig0391184062214"></a>  
    

    ![](figures/face_detection_src.png)

    该�置文件默认�置内容如下：

    ```
    remote_host=192.168.1.2
    data_source=Channel-1
    presenter_view_app_name=video
    ```

    -   remote\_host：�置为Atlas 200 DK开�者�的IP地�。
    -   data\_source : �置摄�头所属Channel，�值为Channel-1或者Channel-2，查询摄�头所属Channel的方法请�考[Atlas 200 DK用户手册](https://ascend.huawei.com/doc/Atlas200DK/)中的“如何查看摄�头所属Channel�。
    -   presenter\_view\_app\_name : 用户自定义的在PresenterServer界�展示的View Name，此View Name需�在Presenter Server展示界�唯一，�能为大�写字��数字�“/�的组�，�数至少1�。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   三个�数必须全部填写，�则无法通过编译。  
    >-   注��数填写时�需�使用“�符�。  
    >-   当�已�按照�置示例�置默认值，请按照�置情况自行修改。  

3.  执行deploy脚本， 进行�置�数调整�第三方库下载编译 打开Mind Studio工具的Terminal，此时默认在代�主目录下，执行如下命令在��指执行deploy脚本，进行环境部署。如[图 执行deploy脚本](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig107831626101910)所示。

    **图 3**  执行deploy脚本<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig107831626101910"></a>  
    ![](figures/执行deploy脚本.png "执行deploy脚本")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   首次deploy时，没有部署第三方库时会自动下载并编译，耗时�能比较久，请�心等待。�续��新编译时，�会��下载编译，部署如上图所示。  
    >-   deploy时，需�选择与开��通信的主机侧ip，一般为虚拟网��置的ip。如果此ip和开��ip属于�网段，则会自动选择并部署。如果��网段，则需�手动输入与开��通信的主机侧ip�能完�deploy。  

4.  开始编译，打开Mindstudio工具，在工具�中点击**Build \> Build \> Build-Configuration**。如[图 编译�作�生�文件](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig1625447397)所示，会在目录下生�build和run文件夹。

    **图 4**  编译�作�生�文件<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig1625447397"></a>  
    

    ![](figures/face_detection_build.png)

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >首次编译工程时，**Build \> Build**为�色��点击状�。需�点击**Build \> Edit Build Configuration**，�置编译�数��进行编译。  

5.  �动Presenter Server。

    打开Mind Studio工具的Terminal，在应用代�存放路径下，执行如下命令在���动Face Detection应用的Presenter Server主程�。如[图 �动PresenterServer](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig423515251067)所示。

    **bash run\_present\_server.sh**

    **图 5**  �动PresenterServer<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig423515251067"></a>  
    

    ![](figures/face_detection_presentserver1.png)

    当�示“**Please choose one to show the presenter in browser\(default: 127.0.0.1\):**�时，请输入在�览器中访问Presenter Server�务所使用的IP地�（一般为访问Mind Studio的IP地�）。

    如[图 工程部署示�图](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig999812514814)所示，请在“**Current environment valid ip list**�中选择通过�览器访问Presenter Server�务使用的IP地�。

    **图 6**  工程部署示�图<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig999812514814"></a>  
    

    ![](figures/face_detection_presentserver2.png)

    如[图7](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig69531305324)所示，表示presenter\_server的�务�动�功。

    **图 7**  Presenter Server进程�动<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig69531305324"></a>  
    

    ![](figures/face_detection_presentserver3.png)

    使用上图�示的URL登录Presenter Server。IP地�为[图 工程部署示�图](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig999812514814)�作时输入的IP地�，端��默为7007，如下图所示，表示Presenter Server�动�功。

    **图 8**  主页显示<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig64391558352"></a>  
    ![](figures/主页显示.png "主页显示")

    Presenter Server�Mind Studio与Atlas 200 DK之间通信使用的IP地�示例如下图所示：

    **图 9**  IP地�示例<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig1881532172010"></a>  
    ![](figures/IP地�示例.png "IP地�示例")

    其中：

    -   Atlas 200 DK开�者�使用的IP地�为192.168.1.2（USB方�连接）。
    -   Presenter Server与Atlas 200 DK通信的IP地�为UI Host�务器中与Atlas 200 DK在�一网段的IP地�，例如：192.168.1.223。
    -   通过�览器访问Presenter Server的IP地�本示例为：10.10.0.1，由于Presenter Server与Mind Studio部署在�一�务器，此IP地�也为通过�览器访问Mind Studio的IP。


## �行<a name="zh-cn_topic_0228461904_section551710297235"></a>

1.  �行Face Detection程�。

    在Mind Studio工具的工具�中找到Run按钮，点击**Run \> Run 'sample-facedetection'**，如[图 程�已执行示�图](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig93931954162719)所示，�执行程�已�在开�者��行。

    **图 10**  程��行示例<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig93931954162719"></a>  
    

    ![](figures/face_detection_run.png)

2.  使用�动Presenter Server�务时�示的URL登录 Presenter Server 网站。

    等待Presenter Agent传输数�给�务端，�击“Refresh“刷新，当有数�时相应的Channel 的Status��绿色，如下图所示。

    **图 11**  Presenter Server界�<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig113691556202312"></a>  
    ![](figures/Presenter-Server界�.png "Presenter-Server界�")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   Face Detection的Presenter Server最多支�10路Channel�时显示，�个  _presenter\_view\_app\_name_  对应一路Channel。  
    >-   由于硬件的�制，�一路支�的最大帧率是20fps，��于网络带宽的影�，帧率会自动适�为较低的帧率进行展示。  

3.  �击�侧对应的View Name链接，比如上图的“video�，查看结果，对于检测到的人脸，会给出置信度的标注。

## �续处�<a name="zh-cn_topic_0228461904_section177619345260"></a>

-   **�止Face Detection应用**

    Face Detection应用执行�会处于�续�行状�，若��止Face Detection应用程�，�执行如下�作。

    �击[图 �止Face Detection应用](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig14326454172518)所示的�止按钮�止Face Detection应用程�。

    **图 12**  �止Face Detection应用<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig14326454172518"></a>  
    

    ![](figures/face_detection_stopping.png)

    如[图 Face Detection应用已�止](#zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig2182182518112)所示应用程�已�止�行

    **图 13**  Face Detection应用已�止<a name="zh-cn_topic_0228461904_zh-cn_topic_0203223294_fig2182182518112"></a>  
    

    ![](figures/face_detection_stoped.png)

-   **�止Presenter Server�务**

    Presenter Server�务�动�会一直处于�行状�，若想�止Face Detection应用对应的Presenter Server�务，�执行如下�作。

    以Mind Studio安装用户在Mind Studio所在�务器中的命令行中执行如下命令查看Face Detection应用对应的Presenter Server�务的进程。

    **ps -ef | grep presenter | grep face\_detection**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-facedetection$ ps -ef | grep presenter | grep face_detection
    ascend    7701  1615  0 14:21 pts/8    00:00:00 python3 presenterserver/presenter_server.py --app face_detection
    ```

    如上所示  _7701_  �为face\_detection应用对应的Presenter Server�务的进程ID。

    若想�止此�务，执行如下命令：

    **kill -9** _7701_


