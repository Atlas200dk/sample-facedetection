EN|[CN](Readme.md)

# Face Detection<a name="ZH-CN_TOPIC_0208834076"></a>

Developers can deploy the application on the Atlas 200 DK to collect camera data in real time and predict facial information in the video.

Application in the current branch is adapted to [DDK&RunTime](https://ascend.huawei.com/resources) with **1.31.0.0 and the above** version 

## Prerequisites<a name="zh-cn_topic_0203223294_section137245294533"></a>

Before using an open source application, ensure that:

-   **Mind Studio**  has been installed.
-   The Atlas 200 DK developer board has been connected to  **Mind Studio**, the cross compiler has been installed, the SD card has been prepared, and basic information has been configured.

## Deployment
1. Deployment: choose either faster-deployment or conventional deployment as shown below: 

   1.1 Faster-deployment, refer to https://gitee.com/Atlas200DK/faster-deploy 。
    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >-   This faster-deployment script can quickly deploy multiple cases, select face detection case for this project.
    >-   This faser-deployment automatically performs code download, model conversion and environment variable configuration. For details, choose conventional deployment method, as shown in 1.2.
    
   1.2 Conventional deployment, refer to : https://gitee.com/Atlas200DK/sample-README/tree/master/sample-facedetection 。
    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >-   This deployment method requires manually performing code download, model conversion and environment variable configuration. A better understand of the deployment process can be obtained from this method.
    
## Compile<a name="zh-cn_topic_0203223294_section7994174585917"></a>

1.  Open the corresponding project.

    Enter the “**MindStudio-ubuntu/bin**” directory after decompressing the installation package in the command line, for example, **$HOME/MindStudio-ubuntu/bin**. Run the following command to start **Mind Studio**:


    **./MindStudio.sh**

     After successfully starting **Mind Studio**, open **sample-facedetection** project，as shown in [Figure 6](#zh-cn_topic_0203223294_fig05481157171918).

    **Figure 6**  Open facedetection project<a name="zh-cn_topic_0203223294_fig05481157171918"></a>  
    

    ![](figures/打开工程项目-人脸检测.png)

2.  Configure related project information in the **src/param\_configure.conf**, as shown in [Figure 7](#zh-cn_topic_0203223294_fig0391184062214).

    **Figure 7**  Configuration file path<a name="zh-cn_topic_0203223294_fig0391184062214"></a>  
    

    ![](figures/face_detection_src.png)

    The configuration file is as follows:


    ```
    remote_host=
    data_source=
    presenter_view_app_name=
    ```
    
    Following parameter configuration needs to be added manually：

    -   remote\_host：indicates the IP address of Atlas 200 DK developer board.
    -   data\_source : Indicates the channel to which a camera belongs to. This parameter can be set to **Channel-1** or **Channel-2**. For details, see **"View the Channel to Which a Camera Belongs"** of[Atlas 200 DK User Guidance](https://ascend.huawei.com/documentation).
    -   presenter\_view\_app\_name : The user-defined View Name on the PresenterServer interface, this View Name needs to be unique  on the Presenter Server. It can only be a combination of uppercase and lowercase letters, numbers, and "\/", with a digit of at least 1.

    An example of configuration is as follows:

    ```
    remote_host=192.168.1.2
    data_source=Channel-1
    presenter_view_app_name=video
    ```

    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >-   All the three parameters must be filled in, otherwise build cannot be passed.
    >-   Note that the "" symbol is no need to be used when filling in parameters.

3.  Run the deployment script to adjust the configuration parameters, download and compile 3rd party libraries. Open the Terminal of **Mind Studio** tool, which is under the main code directory, run the following command to execute environment deployment in the backstage, as shown in [Figure 3](#zh-cn_topic_0182554577_fig19292258105419").
    
    **Figure 3**  Execute deployment script<a name="zh-cn_topic_0182554577_fig19292258105419"></a>  
    
    ![](figures/deploy_facedetection.png)
    
    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >-   Automatic download and compilation will perform if 3rd party libraries are not deployed for the first time of deployment. This process might take some time, please wait patiently. It will not download and compilation repeatedly when recompiling later, deployment is shown as above. 
    >-   Select the HOST IP connected to the developer board when deploying, which is usually the IP of virtual network card. If this IP belongs to the same segment as the developer board IP, it will be selected automatically and deployed. Otherwise, manual entering the IP connected to developer board is required for deployment.
    
4.  Begin to compile, open **Mind Studio** tool, click **Build \> Build \> Build-Configuration** in the toolbar, shown as [Figure 4](#zh-cn_topic_0203223294_fig1625447397), **build** and **run** folders will be generated under the directory.

    **Figure 4**  Compilation operation and generated files<a name="zh-cn_topic_0203223294_fig1625447397"></a>  
    

    ![](figures/face_detection_build.png)

    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >>When you compile the project for the first time, **Build \> Build** is gray and not clickable. Your need to click **Build \> Edit Build Configuration**, configure the compilation parameters and then compile.  
    >![](figures/build_configuration.png)  

5.  <a name="zh-cn_topic_0203223294_li499911453439"></a>Start Presenter Server.

     Open **Terminal** of **Mind Studio** tool, it is in the path where code saved in [Step 1] by default(#zh-cn_topic_0203223294_li953280133816), run the following command to start the **Presenter Server** main program of the **Face Detection**application, as shown in [Figure 5](#zh-cn_topic_0203223294_fig423515251067).

    **bash run\_present\_server.sh**

    **Figure 5**  Start PresenterServer<a name="zh-cn_topic_0203223294_fig423515251067"></a>  
    

    ![](figures/face_detection_presentserver1.png)

     -   When the message "Please choose one to show the presenter in browser (default: 127.0.0.1):" is displayed, enter the IP address used for accessing the **Presenter Server** service in the browser. Generally, the IP address is the IP address for accessing the **Mind Studio** service.

    As shown in [Figure 6](#zh-cn_topic_0203223294_fig999812514814), Select the IP address used by the browser to access the Presenter Server service in "Current environment valid ip list" and enter the path for storing video analysis data.

    **Figure 6**  Project deployment<a name="zh-cn_topic_0203223294_fig999812514814"></a>  
    

    ![](figures/face_detection_presentserver2.png)

    As shown in [Figure 7](#zh-cn_topic_0203223294_fig69531305324) it means **presenter\_server**  service starts successfully.

    **Figure 7**  Starting the Presenter Server process<a name="zh-cn_topic_0203223294_fig69531305324"></a>  
    

    ![](figures/face_detection_presentserver3.png)

    Use the URL shown in the preceding figure to log in to **Presenter Server** (only the Chrome browser is supported). The IP address is that entered in [Figure 8](#zh-cn_topic_0203223294_fig999812514814) and the default port number is 7007. The following figure indicates that **Presenter Server** is started successfully.

    **Figure 8**  Home page<a name="zh-cn_topic_0203223294_fig64391558352"></a>  
    ![](figures/主页显示.png "Home page")

    The following figure shows the IP address used by the **Presenter Server** and **Mind Studio** to communicate with the Atlas 200 DK.
    

    **Figure 9**  Example IP Address<a name="zh-cn_topic_0203223294_fig1881532172010"></a>  
    ![](figures/IP地址示例.png "Example IP Address")

    -   The IP address of the Atlas 200 DK developer board is 192.168.1.2 (connected in USB mode).
    -   The IP address used by the **Presenter Server** to communicate with the Atlas 200 DK is in the same network segment as the IP address of the Atlas 200 DK on the UI Host server. For example: 192.168.1.223.
    -   The following is an example of accessing the IP address of the **Presenter Server** using a browser: 10.10.0.1, because the Presenter Server and **Mind Studio** are deployed on the same server, the IP address is also the IP address for accessing the Mind Studio through the browser.

## Running<a name="zh-cn_topic_0203223294_section551710297235"></a>

1.  Run the Face Detection application.

    Find **Run** button in the toolbar of **Mind Studio** tool, click **Run \> Run 'sample-facedetection'**, as shown in [Figure 10](#zh-cn_topic_0203223294_fig93931954162719), the executable program has been executed on the developer board.
    
    **Figure 10**  Executed program<a name="zh-cn_topic_0203223294_fig93931954162719"></a>  
    

    ![](figures/face_detection_run.png)

2.  Log in to the **Presenter Server** website using the URL promoted when starting the **Presenter Server** service（only supports Chrome browser）, for details, please refer to [Step 4](#zh-cn_topic_0203223294_li499911453439).

    ait for Presenter Agent to transmit data to the server. Click  **Refresh**. When there is data, the icon in the  **Status**  column for the corresponding channel changes to green, as shown in  [Figure 11](#zh-cn_topic_0203223294_fig113691556202312).

    **Figure 11**  Presenter Server page<a name="zh-cn_topic_0203223294_fig113691556202312"></a>  
    ![](figures/Presenter-Server界面.png "Presenter Server page")

    >![](public_sys-resources/icon-note.gif) **NOTE：**   
    >-    The **Presenter Server** of the face detection application supports a maximum of 10 channels at the same time \(each  **_presenter\_view\_app\_name_**  parameter corresponds to a channel\).  
    >-   Due to hardware limitations, the maximum frame rate supported by each channel is 20fps, a lower frame rate is automatically used when the network bandwidth is low.  
3.  Click  **View Name**  column on the right, for example **video** shown as above, and view the result. The confidence of the detected face is marked. 

## Follow-up Operations<a name="zh-cn_topic_0203223294_section177619345260"></a>

-   **Stopping  Face Detection application**

    Face Detection is running continually after being executed. To stop it, perform the following operation:

    Click the stop button to stop Face Detection application as shown in [Figure 12](#zh-cn_topic_0203223294_fig14326454172518).

    **Figure 12**  Stopping Face Detection application<a name="zh-cn_topic_0203223294_fig14326454172518"></a>  
    
    ![](figures/face_detection_stopping.png)

    As shown in [Figure 13](#zh-cn_topic_0203223294_fig2182182518112), the application has been stopped.

    **Figure 13**  Face Detection application stops<a name="zh-cn_topic_0203223294_fig2182182518112"></a>  
    

    ![](figures/face_detection_stoped.png)

-   **Stopping the Presenter Server Service**

    The **Presenter Server** service is always in the running state after being started. To stop the **Presenter Server** service of the Face Detection application, perform the following operations: 

     Run the following command to check the process of the **Presenter Server** service corresponding to the Face Detection application as the **Mind Studio** installation user:

    **ps -ef | grep presenter | grep face\_detection**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-facedetection$ ps -ef | grep presenter | grep face_detection
    ascend    7701  1615  0 14:21 pts/8    00:00:00 python3 presenterserver/presenter_server.py --app face_detection
    ```

    Where  **_7701_**  indicates  the process ID of the **Presenter Server** service corresponding to **face\_detection**.
    
    To stop the service, run the following command:

    **kill -9** _7701_



