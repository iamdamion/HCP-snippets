<!--Title of the snippet.-->
# Extract Timeseries to File Using Surface Parcels

## What is this snippet for?
<!-- What: <each thing should have a brief rundown of what it does. Maybe 2-4 sentences tops. 
example: Simple walkthrough and example code (python) to create a "template" surface pscalar, then to populate the Gordon 333 surpace parcels with arbirary values. 
(good for visualization of any metric or value you are computing using parcels.)
-->
Simple walkthrough and example code (python) to extract timeseries vectors, from a dense timeseries (dtseries) file, using a parcel set's dlabel file. 

## Why do we need this?
<!-- Why: Some brief background on the use case. This can be however long, but keep it short. 
example: For one project I was identifying parcels of interest. To show this across a group of subjects, I needed to essentially place a number on each parcel, which represented how many times that parcel was a parcel of interest across all subjects in my group. This example code allows you to place arbitrary values (for me this was the count of how many times the parcel was chosen) on any parcel, which you can then bring into workbench viewer and make a nice figure including a color map for your results, etc. 
-->
The most basic of needs for any analyses is a bit different using surface files. Here is an example in the most basic of scenarios. You have a dense timseries file created from the HCP pipeline (or any offshoot, such as from DCAN labs or using fmri-prep). Below is how you would:
1. Create a ptseries (parcellated timeseries) file. This is the average value of all vertices within each surface parcel, for all TRs (repetition time).
2. Extract the timeseries vectors from that ptseries file (to a .txt file use in any script), using the 333 cortical surface parcels in the Gordon 333 parcellation set. 

Note: This ptseries (parcellated timeseries file) file can be used with other workbench commands, etc. 

## Code example!
<!-- 
### How: Example code or workbench commands go here
-->
### Step I: Create a pstseries (parcellated timeseries file) from the dtseries
```python
# the dtseries file you want to extract
dt_path = <PATH TO>'/your_dense_timeseries_file.dtseries.nii'
# whatever parcel set you want to use
parc_path = <PATH TO>'/Gordon333_Parcels_LR.dlabel.nii' 
# output path to the ptseries you want to create - 
pt_path = <PATH TO>'/your_parcellated_timeseries_file.ptseries.nii'

pt_comm = ' '.join(['wb_command',
                    '-cifti-parcellate',
                    dt_path,
                    parc_path,
                    'COLUMN',
                    pt_path
                    ])
try:
    subprocess.call(pt_comm, shell=True)
except subprocess.CalledProcessError as err:
    print('ERROR:', err)
```

### Step II: Extract timeseries of average vertex values within each parcel to a .txt file. 

```python
# output path to the .txt - this will have one vector, per line. 
# NOTE: Each line is a parcel (in the order the dlabel file has them labeled).
# Each vector has one value for each TR of the scan.
tc_path = <PATH TO>'/your_timeseries_text_file.txt'

    tcext_comm = ' '.join(['wb_command',
                           '-cifti-convert',
                           '-to-text',
                           pt_path,
                           tc_path
                           ])
    try:
        subprocess.call(tcext_comm, shell=True)
    except subprocess.CalledProcessError as err:
        print('ERROR:', err)
```

### Example Outputs
<!--
- here put a pictuire of the example of what this will make or any files/examples that will help people better understand this tip/process/step
-->
