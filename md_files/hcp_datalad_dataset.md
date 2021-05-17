
<!--Title of the snippet.-->
# Get HCP Data with Datalad

## What is this snippet for?
<!-- What: <each thing should have a brief rundown of what it does. Maybe 2-4 sentences tops. 
example: Simple walkthrough and example code (python) to create a "template" surface pscalar, then to populate the Gordon 333 surpace parcels with arbirary values. 
(good for visualization of any metric or value you are computing using parcels.)
-->
The HCP Open Access dataset is a collection of more than a thousand subjects' multimodal neuroimaging data. Obtaining the data through [https://db.humanconnectome.org/](https://db.humanconnectome.org/) requires thorough navigation and querying of the web interface, followed by a painfully long download process for large collections. 

[Datalad](http://handbook.datalad.org/en/latest/) is an open-source data management tool that simplifies the data download process. The HCP dataset hosted on Amazon S3 buckets have been converted to a datalad dataset and remotely hosted on GitHub at: [https://github.com/datalad-datasets/human-connectome-project-openaccess](https://github.com/datalad-datasets/human-connectome-project-openaccess). 


## Why do we need this?
<!-- Why: Some brief background on the use case. This can be however long, but keep it short. 
example: For one project I was identifying parcels of interest. To show this across a group of subjects, I needed to essentially place a number on each parcel, which represented how many times that parcel was a parcel of interest across all subjects in my group. This example code allows you to place arbitrary values (for me this was the count of how many times the parcel was chosen) on any parcel, which you can then bring into workbench viewer and make a nice figure including a color map for your results, etc. 
-->
Instead of downloading huge images for a large collection of subjects, you can clone this GitHub remote and use datalad to obtain the entire dataset as light-weight symbolic links pointing to the dataset's origin (Amazon S3 Bucket). So instead of downloading TBs of data in one go, you simply download a few MBs of symbolic links, and you can explore the dataset on your computer as if you've already have all the data. And once you've found the specific files you'd like to obtain, you can get the full file with `datalad get`.

## Code example!
See GitHub repo for instructions on how to obtain a `datalad` dataset: [https://github.com/datalad-datasets/human-connectome-project-openaccess](https://github.com/datalad-datasets/human-connectome-project-openaccess)

To summarize:

 - Install `datalad` with either `pip` or `conda` (See handbook below if you've never done this)

 - Obtain your [ConnectomeDB](https://db.humanconnectome.org) account and enable the Amazon S3 bucket access for your Amazon account so you can obtain your own access secret key and key ID.

 - Clone the dataset with `datalad clone https://github.com/datalad-datasets/human-connectome-project-openaccess.git`

 - Each subject folder and their corresponding data folders are called "subdatasets", you can obtain specific files with `datalad get <path/to/file>` or `datalad get <path/to/subdataset>`.

 - If this is the first time you access a Amazon S3 bucket, you will be prompted to enter your access key ID and secret key obtained in the earlier step. 

For people unfamiliar with `datalad`, check out their wonderful handbook: [http://handbook.datalad.org/en/latest/](http://handbook.datalad.org/en/latest/)

### Example Outputs
<!--
- here put a pictuire of the example of what this will make or any files/examples that will help people better understand this tip/process/step
-->

See [https://github.com/datalad-datasets/human-connectome-project-openaccess](https://github.com/datalad-datasets/human-connectome-project-openaccess) for all files available through the GitHub remote host.