# Face detection <a name="EN-CN_TOPIC_0208834076"> </a>

Developers can deploy this application to the Atlas 200DK to implement real-time collection of camera data and prediction of face information in videos.

The applications in the current branch are adapted to [DDK & RunTime] (https://ascend.huawei.com/resources) of ** 1.31.0.0 and above.

## Prerequisites <a name="zh-cn_topic_0203223294_section137245294533"> </a>

Before deploying this sample, you need to prepare the following environments:

-Mind Studio has been installed.
-The connection between Atlas 200 DK developer board and Mind Studio, installation of cross compiler, production of SD card and configuration of basic information have been completed.

## Software preparation <a name="zh-cn_topic_0203223294_section081240125311"> </a>

Before running this Sample, you need to obtain the source package according to this chapter, configure the relevant environment and prepare the model file.

1. <a name="zh-cn_topic_0203223294_li953280133816"> </a> Get the source package.

    Put [https://gitee.com/Atlas200DK/sample-facedetection/tree/1.3x.0.0/](https://gitee.com/Atlas200DK/sample-facedetection/tree/1.3x.0.0/) in the warehouse The code is downloaded by the Mind Studio installation user to any directory on the Ubuntu server where Mind Studio is located. For example, the code storage path is: $ HOME / AscendProjects / sample-facedetection.

2. <a name="zh-cn_topic_0203223294_li1365682471610"> </a> Get the original network model needed in this application.

    Refer to [Table 1] (# zh-cn_topic_0203223294_table144841813177) to obtain the original network model used in this application and its corresponding weight file, and store it in any directory on the Ubuntu server where Mind Studio is located. These two files must be stored in the same directory Under a directory. For example: $ HOME / models / facedetection.

    ** Table 1 ** Models used in Face Detection

    <a name="zh-cn_topic_0203223294_table144841813177"> </a>
    <table> <thead align = "left"> <tr id = "zh-cn_topic_0203223294_row161061318181712"> <th class = "cellrowborder" valign = "top" width = "13.61%" id = "mcps1.2.4.1.1"> < p id = "zh-cn_topic_0203223294_p1410671814173"> <a name="zh-cn_topic_0203223294_p1410671814173"> </a> <a name="zh-cn_topic_0203223294_p1410671814173"> </a> model name </ p>
    </ th>
    <th class = "cellrowborder" valign = "top" width = "10.03%" id = "mcps1.2.4.1.2"> <p id = "zh-cn_topic_0203223294_p1106118121716"> <a name="zh-cn_topic_0203223294_p1106118121716"> </ p a> <a name="zh-cn_topic_0203223294_p1106118121716"> </a> Model description </ p>
    </ th>
    <th class = "cellrowborder" valign = "top" width = "76.36%" id = "mcps1.2.4.1.3"> <p id = "zh-cn_topic_0203223294_p14106218121710"> <a name="zh-cn_topic_0203223294_p14106218121710"> </ p a> <a name="zh-cn_topic_0203223294_p14106218121710"> </a> Model download path </ p>
    </ th>
    </ tr>
    </ thead>
    <tbody> <tr id = "zh-cn_topic_0203223294_row1710661814171"> <td class = "cellrowborder" valign = "top" width = "13.61%" headers = "mcps1.2.4.1.1"> <p id = "zh-cn_topic_0203223294294_p13106121801715" > <a name="zh-cn_topic_0203223294_p13106121801715"> </a> <a name="zh-cn_topic_0203223294_p13106121801715"> </a> face_detection </ p>
    </ td>
    <td class = "cellrowborder" valign = "top" width = "10.03%" headers = "mcps1.2.4.1.2"> <p id = "zh-cn_topic_0203223294_p13106171831710"> <a name="zh-cn_topic_0203223294_p13106171831710"> </ p a> <a name="zh-cn_topic_0203223294_p13106171831710"> </a> Face detection network model. </ p>
    <p id = "zh-cn_topic_0203223294_p18106718131714"> <a name="zh-cn_topic_0203223294_p18106718131714"> </a> <a name="zh-cn_topic_0203223294_p18106718131714"> </a> This model is based on Caffe's Resnet10-SSD300 model conversion Network model. </ p>
    </ td>
    <td class = "cellrowborder" valign = "top" width = "76.36%" headers = "mcps1.2.4.1.3"> <p id = "zh-cn_topic_0203223294_p110671813170"> <a name="zh-cn_topic_0203223294_p110671813170"> </ a a> <a name="zh-cn_topic_0203223294_p110671813170"> </a> Please refer to <a href = "https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/face_detection" target = "_ blank" rel = "noopener noreferrer"> https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/face_detection </a> directory to download the original network model file and its corresponding weight file. </ p>
    </ td>
    </ tr>
    </ tbody>
    </ table>

3. Log in to the Ubuntu server where Mind Studio is installed as the Mind Studio installation user, determine the DDK version number currently used, and set the environment variables DDK \ _HOME, tools \ _version, NPU \ _DEVICE \ _LIB, and LD \ _LIBRARY \ _PATH.
    1. <a name="zh-cn_topic_0203223294_li61417158198"> </a> Query the DDK version number currently used.

        It can be queried through the Mind Studio tool or obtained through the DDK software package.

        -Query using Mind Studio tools.

            In the Mind Studio project interface, select "File \> Settings \> System Settings \> Ascend DDK" in turn, and the interface as shown in [Figure DDK version number query] (en-us_topic_0203223294.md # fig94023140222) is displayed.

            ** Figure 1 ** DDK version number query <a name="zh-cn_topic_0203223294_fig17553193319118"> </a>
            ! [] (figures / DDK version number query.png "DDK version number query")

            The ** DDK Version ** shown is the current DDK version number, such as ** 1.31.T15.B150 **.

        -Query via DDK software package.

            Get the DDK version number by the package name of the installed DDK.

            The package name format of the DDK package is: ** Ascend \ _DDK-\ {software version \}-\ {interface version \}-x86 \ _64.ubuntu16.04.tar.gz **

            ** software version ** is the software version number of the DDK.

            E.g:

            The package name of the DDK package is Ascend \ _DDK-1.31.T15.B150-1.1.1-x86 \ _64.ubuntu16.04.tar.gz, then the version of this DDK is 1.31.T15.B150.

    2. Set the environment variables.

        ** vim \ ~ / .bashrc **

        Run the following command to add the environment variables DDK \ _HOME and LD \ _LIBRARY \ _PATH in the last line.

        ** export tools \ _version = _1.31.X.X _ **

        ** export DDK \ _HOME = \\ $ HOME / .mindstudio / huawei / ddk / \\ $ tools \ _version / ddk **

        ** export NPU \ _DEVICE \ _LIB = $ DDK \ _HOME /../ RC / host-aarch64 \ _Ubuntu16.04.3 / lib **

        ** export LD \ _LIBRARY \ _PATH = $ DDK \ _HOME / lib / x86 \ _64-linux-gcc5.4 **

        >! [] (public_sys-resources / icon-note.gif) ** Description: **
        >-** _ 1.31.X.X _ ** is the DDK version number found in [1] (# zh-cn_topic_0203223294_li61417158198), which needs to be filled in according to the query result, such as ** 1.31.T15.B150 **
        >-If this environment variable has been added, this step can be skipped.

        Enter: wq! To save and exit.

        Run the following command to make the environment variables take effect.

        ** source \ ~ / .bashrc **

4. Convert the original network model into a model suitable for the Shengteng AI processor. There are two ways to convert the model: Mind Studio tool conversion and command line conversion.
    -Model conversion with Mind Studio tools.
        1. Select ** Tools \> Model Convert ** from the top menu bar of the Mind Studio operation interface to enter the model conversion interface.
        2. In the pop-up ** Model ** ** Conversion ** interface, perform the model conversion configuration, as shown in [Figure face \ _detection model conversion configuration] (en-us_topic_0203223294.md # fig58411932131319).

            ** Figure 2 ** face \ _detection model conversion configuration <a name="zh-cn_topic_0203223294_fig206931026131712"> </a>
            

            ! [] (figures / models_facedetection1.png)

            -For the Model File, select the model file downloaded in [Step 2] (# zh-cn_topic_0203223294_li1365682471610). At this time, the weight file will be automatically matched and filled in the Weight File.
            -Fill in the Model Name as the model name in [Table 1] (# zh-cn_topic_0203223294_table144841813177): ** face \ _detection **.

        3. Click ** Next ** to enter the Nodes configuration interface.

            ** Figure 3 ** Nodes configuration example <a name="zh-cn_topic_0203223294_fig3754173017185"> </a>
            

            ! [] (figures / model_facedetection2.png)

        4. Click ** Next ** to enter the Quantization configuration interface.

            Turn off the Quantization Configuration button and do not turn on quantization.

        5. Click ** Next ** to enter the AIPP configuration interface. Need to modify ** Input Image Size \ [W \] \ [H \] ** to 384,304 respectively, here need to do 128 \ * 16 alignment. ** Model Image Format ** needs to be modified to BGR888 \ _U8. Others use default values. As shown in [Figure AIPP Configuration] (# zh-cn_topic_0203223294_fig1682055223010)

            ** Figure 4 ** AIPP configuration <a name="zh-cn_topic_0203223294_fig1682055223010"> </a>
            ! [] (figures / AIPP configuration.png "AIPP configuration")

        6. Click ** Finish ** to start the model conversion.

            When converting, the error message shown in [Figure Model Conversion Error] (en-us_topic_0203223294.md # fig3694182619173) will appear.

            ** Figure 5 ** Model conversion error <a name="zh-cn_topic_0203223294_fig2865313121718"> </a>
            

            ! [] (figures / model_facedetection_coversionfailed.png)

            Select ** SSDDetectionOutput ** in Suggestion ** of ** DetectionOutput ** layer and click ** Retry **.

            After the model conversion is successful, the offline model storage address with the extension .om is: $ HOME / modelzoo / face \ _detection / device.

            >! [] (public_sys-resources / icon-note.gif) ** Description: **
            > For the specific meaning and parameter description of each step in Mindstudio model conversion, please refer to [https://ascend.huawei.com/doc/mindstudio/2.1.0\(beta\)/en/zh-cn\_topic\_0188462651.html ] (https://ascend.huawei.com/doc/mindstudio/2.1.0 (beta) /en/zh-cn_topic_0188462651.html)


    -Command line mode conversion model
        1. Install the user in Mind Studio into the folder where the original model is stored.

            ** cd $ HOME / models / facedetection **

        2. Use the omg tool to execute the following commands for model conversion.

            `` `
            $ {DDK_HOME} / uihost / bin / omg --output = "./ face_detection" --model = "./ face_detection.prototxt" --framework = 0 --ddk_version = $ {tools_version} --weight = "./ face_detection.caffemodel "--input_shape =` head -1 $ HOME / AscendProjects / sample-facedetection / MyModel / shape_face_detection` --insert_op_conf = $ HOME / AscendProjects / sample-facedetection / MyModel / aipp_face_detection.cfg --op_name_map = $ HOME / AscendProjects / sample-facedetection / MyModel / reassign_operators
            `` `

            >! [] (public_sys-resources / icon-note.gif) ** Description: **
            >-input \ _shape, insert \ _op \ _conf, op \ _name \ _map required files are all in the "sample-facedetection / MyModel" directory under the path where the source code is located, please configure these file paths according to the path where your actual source code is located .
            >-The specific meaning of each parameter can be understood in the following document [https://ascend.huawei.com/doc/Atlas200DK/1.3.0.0/en/zh-cn\_topic\_0165968579.html](https:// ascend.huawei.com/doc/Atlas200DK/1.3.0.0/en/zh-cn_topic_0165968579.html).


5. Upload the converted model file (.om file) to the "** sample-facedetection / script **" directory under the path where the source code is located in [Step 1] (# zh-cn_topic_0203223294_li953280133816).

## Compile <a name="zh-cn_topic_0203223294_section7994174585917"> </a>

1. Open the corresponding project.

    As a Mind Studio installation user, enter the "MindStudio-ubuntu / bin" directory after the installation package is decompressed on the command line, such as: $ HOME / MindStudio-ubuntu / bin. Run the following command to start Mind Studio.

    **. / MindStudio.sh **

    After successful startup, open the ** sample-facedetection ** project, as shown in [Figure Open facedetection project] (# zh-cn_topic_0203223294_fig05481157171918).

    ** Figure 6 ** Open facedetection project <a name="zh-cn_topic_0203223294_fig05481157171918"> </a>
    

    ! [] (figures / Open Project-Face Detection.png)

2. Configure related project information in ** src / param \ _configure.conf ** file.

    As shown in [Figure Configuration File Path] (# zh-cn_topic_0203223294_fig0391184062214).

    ** Figure 7 ** Configuration file <a name="zh-cn_topic_0203223294_fig0391184062214"> </a>
    

    ! [] (figures / face_detection_src.png)

    The configuration file is as follows:

    `` `
    remote_host =
    data_source =
    presenter_view_app_name =
    `` `

    -remote \ _host: configured as the IP address of the Atlas 200 DK developer board.
    -data \ _source: Configure the channel to which the camera belongs. The value is Channel-1 or Channel-2. For the method of querying the channel to which the camera belongs, refer to the [Atlas 200 DK User Guide] (https://ascend.huawei.com/documentation) "How to check which channel the camera belongs to".
    -presenter \ _view \ _app \ _name: User-defined View Name displayed on the PresenterServer interface. This View Name needs to be unique on the Presenter Server display interface. It can only be a combination of uppercase and lowercase letters, numbers, and "/". 1 person.

    Configuration example:

    `` `
    remote_host = 192.168.1.2
    data_source = Channel-1
    presenter_view_app_name = video
    `` `

    >! [] (public_sys-resources / icon-note.gif) ** Description: **
    >-All three parameters must be filled in, otherwise the compilation will fail.
    >-Note that you do not need to use the "" symbol when filling in parameters.

3. Start compilation, open Mindstudio tool, click ** Build \> Build \> Build-Configuration ** in the toolbar. As shown in [Figure Compile Operation and Generate File] (# zh-cn_topic_0203223294_fig1625447397), the build and run folders are generated in the directory.

    ** Figure 8 ** Compile operation and generate file <a name="zh-cn_topic_0203223294_fig1625447397"> </a>
    

    ! [] (figures / face_detection_build.png)

    >! [] (public_sys-resources / icon-note.gif) ** Description: **
    > When compiling the project for the first time, ** Build \> Build ** is gray and not clickable. Need to click ** Build \> Edit Build Configuration **, configure the compilation parameters and then compile.
    >! [] (figures / build_configuration.png)

4. <a name="zh-cn_topic_0203223294_li499911453439"> </a> Start Presenter Server.

    Open the Terminal of the Mind Studio tool. At this time, by default, in the code storage path in [Step 1] (# zh-cn_topic_0203223294_li953280133816), execute the following command to start the Presenter Server main program of the Face Detection application in the background. As shown in [Figure Start PresenterServer] (# zh-cn_topic_0203223294_fig423515251067).

    ** bash run \ _present \ _server.sh **

    ** Figure 9 ** Start PresenterServer <a name="zh-cn_topic_0203223294_fig423515251067"> </a>
    

    ! [] (figures / face_detection_presentserver1.png)

    When prompted "** Please choose one to show the presenter in browser \ (default: 127.0.0.1 \): **", please enter the IP address used to access the Presenter Server service in the browser (usually to access Mind Studio IP address).

    As shown in [Figure Engineering Deployment Schematic] (# zh-cn_topic_0203223294_fig999812514814), please select the IP address used by the browser to access the Presenter Server service in "** Current environment valid ip list **".

    ** Figure 10 ** Schematic diagram of project deployment <a name="zh-cn_topic_0203223294_fig999812514814"> </a>
    

    ! [] (figures / face_detection_presentserver2.png)

    As shown in [Figure 11] (# zh-cn_topic_0203223294_fig69531305324), it means that the service of presenter \ _server started successfully.

    ** Figure 11 ** Presenter Server process starts <a name="zh-cn_topic_0203223294_fig69531305324"> </a>
    

    ! [] (figures / face_detection_presentserver3.png)

    Use the URL shown in the figure above to log in to Presenter Server. Only Chrome browser is supported. The IP address is [Figure Schematic diagram of project deployment] (# zh-cn_topic_0203223294_fig999812514814) The IP address entered during the operation, and the port number is 7007 by default, as shown in the figure below, which indicates that the Presenter Server was successfully started.

    ** Figure 12 ** Homepage display <a name="zh-cn_topic_0203223294_fig64391558352"> </a>
    ! [] (figures / homepage display.png "homepage display")

    An example of the IP address used for communication between Presenter Server, Mind Studio and Atlas 200 DK is shown below:

    ** Figure 13 ** Example of IP address <a name="zh-cn_topic_0203223294_fig1881532172010"> </a>
    ! [] (figures / IP address example.png "IP address example")

    among them:

    -The IP address used by the Atlas 200 DK developer board is 192.168.1.2 (USB connection).
    -The IP address of the Presenter Server and the Atlas 200 DK is the IP address of the UI Host server on the same network segment as the Atlas 200 DK, for example: 192.168.1.223.
    -IP address for accessing Presenter Server through a browser This example is: 10.10.0.1. Since Presenter Server is deployed on the same server as Mind Studio, this IP address is also the IP for accessing Mind Studio through a browser.


## Run <a name="zh-cn_topic_0203223294_section551710297235"> </a>

1. Run the Face Detection program.

    Find the Run button in the toolbar of the Mind Studio tool, click ** Run \> Run 'sample-facedetection' **, as shown in [Figure program has been executed] (# zh-cn_topic_0203223294_fig93931954162719), the executable program is already under development Board running.

    ** Figure 14 ** Example of program operation <a name="zh-cn_topic_0203223294_fig93931954162719"> </a>
    

    ! [] (figures / face_detection_run.png)

2. Log in to the Presenter Server website using the URL that is prompted when starting the Presenter Server service. For details, refer to [Starting Presenter Server] (# zh-cn_topic_0203223294_li499911453439).

    Wait for the Presenter Agent to transmit data to the server, and click "Refresh" to refresh. When there is data, the status of the corresponding Channel turns green, as shown in [Figure 15] (# zh-cn_topic_0203223294_fig113691556202312).

    ** Figure 15 ** Presenter Server interface <a name="zh-cn_topic_0203223294_fig113691556202312"> </a>
    ! [] (figures / Presenter-Server interface.png "Presenter-Server interface")

    >! [] (public_sys-resources / icon-note.gif) ** Description: **
    >-Face Detection's Presenter Server supports up to 10 channels to display at the same time, each _presenter \ _view \ _app \ _name_ corresponds to one channel.
    >-Due to hardware limitations, the maximum frame rate supported by each channel is 20fps. Due to the influence of network bandwidth, the frame rate will be automatically adapted to a lower frame rate for display.

3. Click the corresponding View Name link on the right, such as "video" in the figure above, to view the results. For detected faces, a confidence level annotation will be given.

## Follow-up <a name="zh-cn_topic_0203223294_section177619345260"> </a>

-** Stop Face Detection app **

    The Face Detection application will run continuously after execution. To stop the Face Detection application, perform the following operations.

    Click the stop button shown in [Figure Stop Face Detection Application] (# zh-cn_topic_0203223294_fig14326454172518) to stop the Face Detection application.

    ** Figure 16 ** Stop Face Detection application <a name="zh-cn_topic_0203223294_fig14326454172518"> </a>
    

    ! [] (figures / face_detection_stopping.png)

    As shown in [Figure Face Detection application has stopped] (# zh-cn_topic_0203223294_fig2182182518112) the application has stopped running

    ** Figure 17 ** Face Detection application has stopped <a name="zh-cn_topic_0203223294_fig2182182518112"> </a>
    

    ! [] (figures / face_detection_stoped.png)

-** Stop Presenter Server service **

    The Presenter Server service is always running after it is started. If you want to stop the Presenter Server service corresponding to the Face Detection application, you can perform the following operations.

    As a Mind Studio installer, run the following command on the command line on the server where Mind Studio is installed to view the progress of the Presenter Server service corresponding to the Face Detection application.

    ** ps -ef | grep presenter | grep face \ _detection **

    `` `
    ascend @ ascend-HP-ProDesk-600-G4-PCI-MT: ~ / sample-facedetection $ ps -ef | grep presenter | grep face_detection
    ascend 7701 1615 0 14:21 pts / 8 00:00:00 python3 presenterserver / presenter_server.py --app face_detection
    `` `

    As shown above, _7701_ is the process ID of the Presenter Server service corresponding to the face \ _detection application.

    To stop this service, execute the following command:

    ** kill -9 ** _7701_
