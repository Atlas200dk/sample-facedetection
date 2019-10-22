EN|[CN](README_cn.md)

# Face Detection<a name="EN-US_TOPIC_0167573017"></a>

Developers can deploy the application on the Atlas 200 DK to collect camera data in real time and predict facial information in the video.

## Prerequisites<a name="en-us_topic_0182554577_section137245294533"></a>

Before using an open source application, ensure that:

-   Mind Studio  has been installed.
-   The Atlas 200 DK developer board has been connected to  Mind Studio, the cross compiler has been installed, the SD card has been prepared, and basic information has been configured.

## Software Preparation<a name="en-us_topic_0182554577_section081240125311"></a>

Before running the application, obtain the source code package and configure the environment as follows.

1.  <a name="en-us_topic_0182554577_li953280133816"></a>Obtain the source code package.

    Download all the code in the sample-facedetection repository at  [https://github.com/Ascend/sample-facedetection](https://github.com/Ascend/sample-facedetection)  to any directory on Ubuntu Server where  Mind Studio  is located as the  Mind Studio  installation user, for example,  _/home/ascend/sample-facedetection/_.

2.  <a name="en-us_topic_0182554577_li1365682471610"></a>Obtain the source network model required by the application.

    Obtain the source network model and its weight file used in the application by referring to  [Table 1](#en-us_topic_0182554577_table144841813177), and save them to any directory on the Ubuntu server where  Mind Studio  is located (for example,  **$HOME/ascend/models/facedetection**).

    **Table  1**  Models used for face detection

    <a name="en-us_topic_0182554577_table144841813177"></a>
    <table><thead align="left"><tr id="en-us_topic_0182554577_row161061318181712"><th class="cellrowborder" valign="top" width="13.61%" id="mcps1.2.4.1.1"><p id="en-us_topic_0182554577_p1410671814173"><a name="en-us_topic_0182554577_p1410671814173"></a><a name="en-us_topic_0182554577_p1410671814173"></a>Model Name</p>
    </th>
    <th class="cellrowborder" valign="top" width="10.03%" id="mcps1.2.4.1.2"><p id="en-us_topic_0182554577_p1106118121716"><a name="en-us_topic_0182554577_p1106118121716"></a><a name="en-us_topic_0182554577_p1106118121716"></a>Model Description</p>
    </th>
    <th class="cellrowborder" valign="top" width="76.36%" id="mcps1.2.4.1.3"><p id="en-us_topic_0182554577_p14106218121710"><a name="en-us_topic_0182554577_p14106218121710"></a><a name="en-us_topic_0182554577_p14106218121710"></a>Model Download Path</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="en-us_topic_0182554577_row1710661814171"><td class="cellrowborder" valign="top" width="13.61%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554577_p13106121801715"><a name="en-us_topic_0182554577_p13106121801715"></a><a name="en-us_topic_0182554577_p13106121801715"></a>face_detection</p>
    </td>
    <td class="cellrowborder" valign="top" width="10.03%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554577_p167411934194719"><a name="en-us_topic_0182554577_p167411934194719"></a><a name="en-us_topic_0182554577_p167411934194719"></a>Network model for face detection.</p>
    <p id="en-us_topic_0182554577_p1337174414715"><a name="en-us_topic_0182554577_p1337174414715"></a><a name="en-us_topic_0182554577_p1337174414715"></a>It is a network model converted from ResNet10-SSD300 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.36%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554577_p110671813170"><a name="en-us_topic_0182554577_p110671813170"></a><a name="en-us_topic_0182554577_p110671813170"></a>Download the source network model file and its weight file by referring to<strong id="en-us_topic_0182554577_b10408165011127"><a name="en-us_topic_0182554577_b10408165011127"></a><a name="en-us_topic_0182554577_b10408165011127"></a> README.md</strong> in <a href="https://github.com/Ascend/models/tree/master/computer_vision/object_detect/face_detection" target="_blank" rel="noopener noreferrer">https://github.com/Ascend/models/tree/master/computer_vision/object_detect/face_detection</a>.</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  Convert the source network model to a Da Vinci model.
    1.  Choose  **Tool \> Convert Model**  from the main menu of  Mind Studio. The  **Convert Model**  page is displayed.
    2.  On the  **Convert Model**  page, set  **Model File**  and  **Weight File**  to the model file and weight file downloaded in  [2](#en-us_topic_0182554577_li1365682471610), respectively.

        See  [Figure 1](#en-us_topic_0182554577_fig1954118512311).

        -   Set  **Model Name**  to the model name in  [Table 1](#en-us_topic_0182554577_table144841813177):  **face\_detection**.
        -   Retain default values for other parameters.

        **Figure  1**  face\_detection model conversion configuration<a name="en-us_topic_0182554577_fig1954118512311"></a>  
        ![](doc/source/img/face_detection-model-conversion-configuration.jpg "face_detection-model-conversion-configuration")

    3.  Click  **OK**  to start model conversion.

        During the conversion, the following error will be reported.

        **Figure  2**  Model conversion error<a name="en-us_topic_0182554577_fig1632884495219"></a>  
        ![](doc/source/img/model-conversion-error.jpg "model-conversion-error")

        Select  **SSDDetectionOutput**  from the  **Suggestion**  drop-down list box at the  **DetectionOutput**  layer and click  **Retry**.

        After successful conversion, a .om model file is generated in the  **$HOME/tools/che/model-zoo/my-model/face\_detection** directory.

        See the following figure.

        **Figure  3**  Successful model conversion<a name="en-us_topic_0182554577_fig19292258105419"></a>  
        ![](doc/source/img/successful-model-conversion.jpg "successful-model-conversion")

4.  Upload the converted .om model file to the  **sample-facedetection/script**  directory in the source code path in  [1](#en-us_topic_0182554577_li953280133816).
5.  Log in to Ubuntu Server where  Mind Studio  is located as the  Mind Studio  installation user and set the environment variable  **DDK\_HOME**.

    **vim \~/.bashrc**

    Run the following commands to add the environment variables  **DDK\_HOME**  and  **LD\_LIBRARY\_PATH**  to the last line:

    **export DDK\_HOME=/home/XXX/tools/che/ddk/ddk**

    **export LD\_LIBRARY\_PATH=$DDK\_HOME/uihost/lib**

    >![](doc/source/img/icon-note.gif) **NOTE:**   
    >-   **XXX**  indicates the  Mind Studio  installation user, and  **/home/XXX/tools**  indicates the default installation path of the DDK.  
    >-   If the environment variables have been added, skip this step.  

    Enter  **:wq!**  to save and exit.

    Run the following command for the environment variable to take effect:

    **source \~/.bashrc**


## Deployment<a name="en-us_topic_0182554577_section7994174585917"></a>

1.  Access the root directory where the face detection application code is located as the  Mind Studio  installation user, for example,  _**/home/ascend/sample-facedetection**_.
2.  Run the deployment script to prepare the project environment, including compiling and deploying the ascenddk public library and configuring Presenter Server. The Presenter Server is used to receive the data sent by the application and display the result through the browser.

    **bash deploy.sh** _host\_ip_ _model\_mode_

    -   _host\_ip_: For the Atlas 200 DK developer board, this parameter indicates the IP address of the developer board.
    -   _model\_mode_  indicates the deployment mode of the model file. The default setting is  **internet**.
        -   **local**: If the Ubuntu system where  Mind Studio  is located is not connected to the network, use the local mode. In this case, download the dependent common code library to the  **sample-facedetection/script**  directory by referring to  [Downloading Dependent Code Library](#en-us_topic_0182554577_section4995103618210).
        -   **internet**: Indicates the online deployment mode. If the Ubuntu system where  Mind Studio  is located is connected to the network, use the Internet mode. In this case, download the dependent code library online.


    Example command:

    **bash deploy.sh 192.168.1.2 internet**

    When the message  **Please choose one to show the presenter in browser\(default: 127.0.0.1\):**  is displayed, enter the IP address used for accessing the Presenter Server service in the browser. Generally, the IP address is the IP address for accessing the  Mind Studio  service.

    Select the IP address used by the browser to access the Presenter Server service in  **Current environment valid ip list**, as shown in  [Figure 4](#en-us_topic_0182554577_fig184321447181017).

    **Figure  4**  Project deployment<a name="en-us_topic_0182554577_fig184321447181017"></a>  
    ![](doc/source/img/project-deployment.png "project-deployment")

3.  <a name="en-us_topic_0182554577_li499911453439"></a>Start Presenter Server.

    Run the following command to start the Presenter Server program of the face detection application in the background:

    **python3 presenterserver/presenter\_server.py --app face\_detection &**

    >![](doc/source/img/icon-note.gif) **NOTE:**   
    >**presenter\_server.py**  is located in the  **presenterserver**  in the current directory. You can run the  **python3 presenter\_server.py -h**  or  **python3 presenter\_server.py --help**  command in this directory to view the usage method of  **presenter\_server.py**.  

    [Figure 5](#en-us_topic_0182554577_fig69531305324)  shows that the presenter\_server service is started successfully.

    **Figure  5**  Starting the Presenter Server process<a name="en-us_topic_0182554577_fig69531305324"></a>  
    ![](doc/source/img/starting-the-presenter-server-process.png "starting-the-presenter-server-process")

    Use the URL shown in the preceding figure to log in to Presenter Server \(only the Chrome browser is supported\). The IP address is that entered in  [Figure 6](#en-us_topic_0182554577_fig64391558352)  and the default port number is  **7007**. The following figure indicates that Presenter Server is started successfully.

    **Figure  6**  Home page<a name="en-us_topic_0182554577_fig64391558352"></a>  
    ![](doc/source/img/home-page.png "home-page")

    The following figure shows the IP address used by the Presenter Server and  Mind Studio  to communicate with the Atlas 200 DK.

    **Figure  7**  Example IP Address<a name="en-us_topic_0182554577_fig1881532172010"></a>  
    ![](doc/source/img/example-ip-address.png "example-ip-address")

    Where:

    -   The IP address of the Atlas 200 DK developer board is 192.168.1.2 \(connected in USB mode\).
    -   The IP address used by the Presenter Server to communicate with the Atlas 200 DK is in the same network segment as the IP address of the Atlas 200 DK on the UI Host server. For example: 192.168.1.223.
    -   The following is an example of accessing the IP address of the Presenter Server using a browser: 10.10.0.1, because the Presenter Server and  Mind Studio  are deployed on the same server, the IP address is also the IP address for accessing the  Mind Studio  through the browser.


## Running<a name="en-us_topic_0182554577_section551710297235"></a>

1.  Run the face detection application.

    Run the following command in the  **sample-facedetection**  directory to start the face detection application:

    **bash run\_facedetectionapp.sh** _host\_ip_ _presenter\_view\_app\_name camera\_channel\_name_  &

    -   _host\_ip_: For the Atlas 200 DK developer board, this parameter indicates the IP address of the developer board.
    -   _presenter\_view\_app\_name_: Indicates  **View Name**  displayed on the Presenter Server page, which is user-defined. The value of this parameter must be unique on the Presenter Server page, which contains only case-senstive leters, digits, and underscores(_). The number of characters should be 3-20.
    -   _camera\_channel\_name_: Indicates the channel to which a camera belongs. The value can be  **Channel-1**  or  **Channel-2**. For details, see  **View the Channel to Which a Camera Belongs**  in  [Atlas 200 DK User Guide](https://ascend.huawei.com/documentation).

    Example command:

    **bash run\_facedetectionapp.sh 192.168.1.2 video Channel-1 &**

2.  Use the URL that is displayed when you start the Presenter Server service to log in to the Presenter Server website. For details, see  [3](#en-us_topic_0182554577_li499911453439).

    Wait for Presenter Agent to transmit data to the server. Click  **Refresh**. When there is data, the icon in the  **Status**  column for the corresponding channel changes to green, as shown in  [Figure 8](#en-us_topic_0182554577_fig113691556202312).

    **Figure  8**  Presenter Server page<a name="en-us_topic_0182554577_fig113691556202312"></a>  
    ![](doc/source/img/presenter-server-page.png "presenter-server-page")

    >![](doc/source/img/icon-note.gif) **NOTE:**   
    >-   The Presenter Server of the face detection application supports a maximum of 10 channels at the same time \(each  _presenter\_view\_app\_name_  parameter corresponds to a channel\).  
    >-   Due to hardware limitations, the maximum frame rate supported by each channel is 20fps, a lower frame rate is automatically used when the network bandwidth is low.  

3.  Click  **image**  or  **video**  in the  **View Name**  column and view the result. The confidence of the detected face is marked.

## Follow-up Operations<a name="en-us_topic_0182554577_section177619345260"></a>

-   **Stopping the Face Detection Application**

    The face detection application is running continually after being executed. To stop it, perform the following operation:

    Run the following command in the  _**/home/ascend/sample-facedetection**_  directory as the  Mind Studio  installation user:

    **bash stop\_facedetectionapp.sh** _host\_ip_

    _host\_ip_: For the Atlas 200 DK developer board, this parameter indicates the IP address of the developer board. For the Atlas 300 PCIe card, this parameter indicates the IP address of the PCIe card host.

    Example command:

    **bash stop\_facedetectionapp.sh 192.168.1.2**

-   **Stopping the Presenter Server Service**

    The Presenter Server service is always in the running state after being started. To stop the Presenter Server service of the face detection application, perform the following operations:

    Run the following command to check the process of the Presenter Server service corresponding to the face detection application as the  Mind Studio  installation user:

    **ps -ef | grep presenter | grep face\_detection**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-facedetection$ ps -ef | grep presenter | grep face_detection 
    ascend    7701  1615  0 14:21 pts/8    00:00:00 python3 presenterserver/presenter_server.py --app face_detection
    ```

    In the preceding information,  _7701_  indicates the process ID of the Presenter Server service corresponding to the face detection application.

    To stop the service, run the following command:

    **kill -9** _7701_


## Downloading Dependent Code Library<a name="en-us_topic_0182554577_section4995103618210"></a>

Download the dependent software libraries to the  **sample-facedetection/script**  directory.

**Table  2**  Download the dependent software library

<a name="en-us_topic_0182554577_table1935612447166"></a>
<table><thead align="left"><tr id="en-us_topic_0182554577_row1443920204334"><th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.1"><p id="en-us_topic_0182554577_p114391320203313"><a name="en-us_topic_0182554577_p114391320203313"></a><a name="en-us_topic_0182554577_p114391320203313"></a>Module Name</p>
</th>
<th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.2"><p id="en-us_topic_0182554577_p9439112010334"><a name="en-us_topic_0182554577_p9439112010334"></a><a name="en-us_topic_0182554577_p9439112010334"></a>Module Description</p>
</th>
<th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.3"><p id="en-us_topic_0182554577_p1443982013333"><a name="en-us_topic_0182554577_p1443982013333"></a><a name="en-us_topic_0182554577_p1443982013333"></a>Download Address</p>
</th>
</tr>
</thead>
<tbody><tr id="en-us_topic_0182554577_row843916205332"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554577_p143916201331"><a name="en-us_topic_0182554577_p143916201331"></a><a name="en-us_topic_0182554577_p143916201331"></a>EZDVPP</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554577_p543917207336"><a name="en-us_topic_0182554577_p543917207336"></a><a name="en-us_topic_0182554577_p543917207336"></a>Encapsulates the DVPP interface and provides image and video processing capabilities, such as color gamut conversion and image / video conversion</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554577_p7439122023313"><a name="en-us_topic_0182554577_p7439122023313"></a><a name="en-us_topic_0182554577_p7439122023313"></a><a href="https://github.com/Ascend/sdk-ezdvpp" target="_blank" rel="noopener noreferrer">https://github.com/Ascend/sdk-ezdvpp</a></p>
<p id="en-us_topic_0182554577_p14439520183315"><a name="en-us_topic_0182554577_p14439520183315"></a><a name="en-us_topic_0182554577_p14439520183315"></a>After the download, keep the folder name <span class="filepath" id="en-us_topic_0182554577_filepath1243922012337"><a name="en-us_topic_0182554577_filepath1243922012337"></a><a name="en-us_topic_0182554577_filepath1243922012337"></a><b>ezdvpp</b></span>.</p>
</td>
</tr>
<tr id="en-us_topic_0182554577_row2044012015330"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554577_p114391206337"><a name="en-us_topic_0182554577_p114391206337"></a><a name="en-us_topic_0182554577_p114391206337"></a>Presenter Agent</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554577_p54407202337"><a name="en-us_topic_0182554577_p54407202337"></a><a name="en-us_topic_0182554577_p54407202337"></a><span>API for interacting with the Presenter Server</span>.</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554577_p134402020123313"><a name="en-us_topic_0182554577_p134402020123313"></a><a name="en-us_topic_0182554577_p134402020123313"></a><a href="https://github.com/Ascend/sdk-presenter/tree/master" target="_blank" rel="noopener noreferrer">https://github.com/Ascend/sdk-presenter/tree/master</a></p>
<p id="en-us_topic_0182554577_p5440152033310"><a name="en-us_topic_0182554577_p5440152033310"></a><a name="en-us_topic_0182554577_p5440152033310"></a>Obtain the presenteragent folder in this path, after the download, keep the folder name <span class="filepath" id="en-us_topic_0182554577_filepath1440192033318"><a name="en-us_topic_0182554577_filepath1440192033318"></a><a name="en-us_topic_0182554577_filepath1440192033318"></a><b>presenteragent</b></span>.</p>
</td>
</tr>
<tr id="en-us_topic_0182554577_row1044016209336"><td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0182554577_p184401420133312"><a name="en-us_topic_0182554577_p184401420133312"></a><a name="en-us_topic_0182554577_p184401420133312"></a>tornado (5.1.0)</p>
<p id="en-us_topic_0182554577_p1744010205335"><a name="en-us_topic_0182554577_p1744010205335"></a><a name="en-us_topic_0182554577_p1744010205335"></a>protobuf (3.5.1)</p>
<p id="en-us_topic_0182554577_p114401820133318"><a name="en-us_topic_0182554577_p114401820133318"></a><a name="en-us_topic_0182554577_p114401820133318"></a>numpy (1.14.2)</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0182554577_p2440920163311"><a name="en-us_topic_0182554577_p2440920163311"></a><a name="en-us_topic_0182554577_p2440920163311"></a>Python libraries that Presenter Server depends on.</p>
</td>
<td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0182554577_p156393307316"><a name="en-us_topic_0182554577_p156393307316"></a><a name="en-us_topic_0182554577_p156393307316"></a>You can search for related packages on the Python official website <a href="https://pypi.org/" target="_blank" rel="noopener noreferrer">https://pypi.org/</a> for installation. If you run the pip3 install command to download the file online, you can run the following command to specify the version to be downloaded: <strong id="en-us_topic_0182554577_b84911294419"><a name="en-us_topic_0182554577_b84911294419"></a><a name="en-us_topic_0182554577_b84911294419"></a>pip3 install tornado==5.1.0 -i <em id="en-us_topic_0182554577_i1556317151418"><a name="en-us_topic_0182554577_i1556317151418"></a><a name="en-us_topic_0182554577_i1556317151418"></a>Installation source of the specified library</em> --trusted-host <em id="en-us_topic_0182554577_i9475221741"><a name="en-us_topic_0182554577_i9475221741"></a><a name="en-us_topic_0182554577_i9475221741"></a>Host name of the installation sourc</em>e</strong></p>
</td>
</tr>
</tbody>
</table>

