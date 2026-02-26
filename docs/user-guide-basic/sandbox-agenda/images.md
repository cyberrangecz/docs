## Images Overview

Provides a list of available images that can be installed on virtual machines. Each row contains the following values of image parameters:

* **Name**: The unique name of the image.
* **Default User**: User used to login to the virtual machine via GUI or connect via SSH.
* **Updated At**: Last time image was updated.
* **Gui Access**: Signals if graphical user interface is installed for the image.
* **Size**: The size of the image, in gigabytes.

!!! note
    Don't get confused by the **Gb** in the name of column **Size**. The value is in gigabytes, not gigabits.

Click extend button :material-chevron-down:{: .icon .grey} to show **detailed information** about the image:

* **OS Distro**: Common name of operating system distribution.
* **OS Type**: Linux or windows.
* **Disk Format**: The format of the underlying disk image specifies how the disk stores information.
* **Container Format**: Indicates whether the image also contains metadata about the virtual machine (bare = no metadata).
* **Min Disk**: Minimum amount of disk memory to boot image, in gigabytes.
* **Min RAM**: Minimum amount of main memory to boot image, in megabytes.
* **Visibility**: Public, private, community, shared.
* **Created At**: Time of the creation.
* **Tags**: Used to filter images.
* **Version**: Specifies the version of the image.

Checkbox **Only CRCZP images** allows filtering of images that are created by the CyberRangeCZ Platform team.

Checkbox **Only GUI access** allows filtering of images that have graphical user interface installed for the image.

![overview-images](/img/user-guide-basic/sandbox-agenda/images/overview-images.png){: .shadow .center .radius-image }
