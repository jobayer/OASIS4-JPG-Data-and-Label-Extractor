# OASIS4-JPG-Data-and-Label-Extractor
The Python script to extract JPG images and categorize them into different classes of dementia using the NIFTI data.

> This script was made for one of our personal projects, but I thought it might be worth sharing! Please feel free to modify it as you like.

### Background

The original [OASIS-4 dataset](https://sites.wustl.edu/oasisbrains/home/oasis-4/) consists of medical images in NIFTI format, which can be challenging to handle and preview. Additionally, extracting the associated labels or dementia classes from the images can be difficult. Therefore, I attempted to create a script to automate the process of extracting the image data in a standard format (e.g., JPEG) along with their corresponding labels in this Jupyter Notebook file.

### Folder Structure

Once you access the dataset from their website, you should have a folder structure similar to the one shown below.

- 0AS4_data_files
- OAS42000
    - OAS42000_MR_d3016
        - anat1
            - BIDS
                - sub-OAS42000_sess-d3016_FLAIR.json
            - NIFTI
                - sub-OAS42000_sess-d3016_FLAIR.nii.gz
        - anat2
        - ...
        - swi1
        - swi2
- OAS42001
- ...

### Precautionaries

During the extraction process, we have assumed some conditions following the sample code given in the dataset. Some of them are listed below.

- A NIFTI file usually contains multiple slices of images. However, for simplification, for each sequence (i.e., anat1, anat2, swi1), the script selects only one slice, the middle slice, with a round-off indexing using the `\\` operator.
- To label the data using Clinical Dementia Rating (CDR), we have utilized the `OASIS4_data_CDR.csv` file located in the `0AS4_data_files` directory. We labelled the images using the following relationship between the CDR number and the dementia level using the [CDR Scoring table](https://knightadrc.wustl.edu/professionals-clinicians/cdr-dementia-staging-instrument/cdr-scoring-table/).
- In some cases, there are multiple visits of a subject in the `OASIS4_data_CDR.csv` file. In this case, we chose the CDR record with the least difference between the `visit_days` column of the same subject and the relative day (for example, 3016) from the directory name `OAS42000_MR_d3016`, as shown in the example directory structure above.
- In the case of sequence selection, while looking for the sequences available in a directory, we excluded directories containing the terms `BIDS` and `Freesurfer`.  `BIDS` includes metadata of the MRI machines and other hardware and software properties, which are not of our interest. On the other hand, `Freesurfer` is brain imaging software [[1]](https://surfer.nmr.mgh.harvard.edu/), which is also not of interest.
- By default, we chose the `gray` colormap to save the images.

### Variables

The script is self-explanatory. If the dataset maintains the default folder structure, then it should be sufficient to change only the `ROOT_DIR` variable, which is the root directory of your dataset in NIFTI format, and the `CONVERTED_IMG_DIR` variable, which is the location where you want to save the images once they are converted into JPEG format. The other customizations are optional. Feel free to tweak it to your liking.

### Python Packages

To run the script, you will need the following Python packages installed in your Python environment, along with the dataset.

- nibabel
- pandas
- numpy
- matplotlib
- glob2
- tqdm

_For any queries, feel free to reach me at [jobayer@ieee.org](mailto:jobayer@ieee.org)._