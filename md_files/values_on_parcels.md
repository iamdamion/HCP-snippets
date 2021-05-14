<!--Title of the snippet.-->
# Populate surface parcels with arbitrary values

## What is this snippet for?
<!-- What: <each thing should have a brief rundown of what it does. Maybe 2-4 sentences tops. 
example: Simple walkthrough and example code (python) to create a "template" surface pscalar, then to populate the Gordon 333 surpace parcels with arbirary values. 
(good for visualization of any metric or value you are computing using parcels.)
-->
Simple walkthrough and example code (python) to create a "template" surface pscalar, then to populate the Gordon 333 surpace parcels with arbirary values. 
(good for visualization of any metric or value you are computing using parcels.)

## Why do we need this?
<!-- Why: Some brief background on the use case. This can be however long, but keep it short. 
example: For one project I was identifying parcels of interest. To show this across a group of subjects, I needed to essentially place a number on each parcel, which represented how many times that parcel was a parcel of interest across all subjects in my group. This example code allows you to place arbitrary values (for me this was the count of how many times the parcel was chosen) on any parcel, which you can then bring into workbench viewer and make a nice figure including a color map for your results, etc. 
-->
For one project I was identifying parcels of interest. To show this across a group of subjects, I needed to essentially place a number on each parcel, which represented how many times that parcel was a parcel of interest across all subjects in my group. This example code allows you to place arbitrary values (for me this was the count of how many times the parcel was chosen) on any parcel, which you can then bring into workbench viewer and make a nice figure including a color map for your results, etc. 


## Code example!
<!-- 
### How: Example code or workbench commands go here
-->
### Step I: Make TEMPLATE pscalar from original dlabel (this only needs to be done once really)
```python

# any dscalar in the correct surface you want to use
hcp1200_dscalar_source = <PATH TO>'/S1200.sulc_MSMAll.32k_fs_LR.dscalar.nii' 
# whatever parcel set you want to use
gordon_dlabel = <PATH TO>'/Gordon333_Parcels_LR.dlabel.nii' 
# The template you want to put values onto going forward
out_pscalar_TEMPLATE = <PATH TO>'/Gordon333_TEMPLATE.pscalar.nii' 

# the wb_command
wb_comm = ' '.join(['wb_command',
                    '-cifti-parcellate',
                    hcp1200_dscalar_source,
                    gordon_dlabel,
                    'COLUMN',
                    out_pscalar_TEMPLATE
                   ])
subprocess.call(wb_comm, shell=True)
```

### Step II: Make and save whatever values. 
- 333 vector (each line of text file is each parcel 1-333. careful of python 0 indexing)
- Save out as text file, one value per line.

```python
value_vect_out = <PATH TO>'/TEST_values.txt'
# making manual text file just for testing here
the_vect = np.zeros(333, dtype=np.int).tolist()
the_vect[0] = 1
the_vect[161] = 162
the_vect[116] = 117
the_vect[278] = 279
with open(value_vect_out, 'w') as f:
    for item in the_vect:
        f.write(str(item) + '\n')
```

### Step III: Write that vector of value to a pscalar file for wb view!!

```python
output_pscalar = <PATH TO>'/YOUR_OUTPUT_G333.pscalar.nii'
wb_comm = ' '.join(['wb_command',
                    '-cifti-convert',
                    '-from-text',
                    value_vect_out,
                    out_pscalar_TEMPLATE,
                    output_pscalar                    
                   ])
subprocess.call(wb_comm, shell=True)
```

### Example Outputs
<!--
- here put a pictuire of the example of what this will make or any files/examples that will help people better understand this tip/process/step
-->
