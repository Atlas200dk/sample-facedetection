# Face detection <a name="EN-CN_TOPIC_0208834076"> </a>

Developers can deploy this application to the Atlas 200DK to implement real-time collection of camera data and prediction of face information in videos.

The application in the current branch is adapted to [DDK & RunTime] (https://ascend.huawei.com/resources) of ** 1.31.0.0 and above **.

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
    <p id = "zh-cn_topic_0203223294_p18106718131714"> <a name="zh-cn_topic_0203223294_p18106718131714"> </a> <a name="zh-cn_topic_0203223294_p18106718131714"> </a> This model is based on the Caffe Resnet10-SSD300 model conversion Network model. </ p>
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

            The package name of the DDK package is Ascend \ _DDK-1.31.T15.B150-1.1.1-x86 \ _64.ubuntu16.04.tar.gz, then the version number of this DDK is 1.31.T15.B150.

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

4. Convert the original network model to a model suitable for the Ascension AI processor. The model is converted to Mind Studio.
