# UKB RAP data extraction tutorial

- this is a quick tutorial building on work by the DNANexus Team on how to extract UKB phenotype data into a txt-like file created by Alexander Mörseburg (IMS-MRL) on 21/01/2022

- please note that this is just a rough guide and there is ABSOLUTELY NO WARRANTY


## 1. Launch Jupyterlab app
- Click "Tools" --> JupyterLab --> "New JupyterLab"

- enter name of your environment, configuration: **Spark Cluster** and set priority to **High**, for instance type you can experiment a bit, smth like *mem1_hdd1_v2_x16* and one or two nodes should be fine

- wait a few min for your environment to start

## 2. Extract data inside Jupyterlab

- please see the notebook **command_files/extract_phenotypes_female_specific_facs.ipynb** and the video from the tutorial on 21/01/2022 for more details

- a few key steps

### 2.a Load in your notebook

- open an untitled notebook and enter the following command


```{python dummychunk, echo = TRUE, eval = FALSE}
%%bash
dx download "/genetics_of_miscarriage/command_files/pheno_extraction/extract_phenotypes_miscarriage_genetics.ipynb"
```

### 2.b Read your phenotype in

- there are multiple ways of doing this, a way "native" to the script would be to create simple text files with the field numbers for UKB and one file per line, read into python for example as list (**mylist** in code below) and then do smth like (after functions under point 4 in notebook have been defined)

```{python dummychunk2, echo = TRUE, eval = FALSE}
print(fields_for_field_id(mylist)) # test fct
```

- I have provided a 35k row text file **original_data/ukb_fields_rap_field_names_20211203.txt**, please extract the column *field_names_pyspark* with your software of choice and feed it into the notebook after uploading the field_names files to the project, code can be found under point 3 in notebook, just replace **fem_spec_facs_ukb_field_names_pyspark.txt** with your own file

- the second option should work reasonably well for most data types, but in some cases for example for the hospital data all arrays are in a single column, this is not accounted for in my original data

## 3. Export your phenotypes

- modify the last line of the notebook (see below) accordingly

- when you have exported your data to your project you can either a) refine the phenotype data using another Juypter nb session or b) download the data to your local machine for processing (you can always re-upload the processed data to the RAP, though there is a tension here between pragmatism and having everything in one mostly closed system for potential audits etc.)

```{python dummychunk3, echo = TRUE, eval = FALSE}
%%bash
dx upload output.tsv --dest your_project/.../output.tsv
```
