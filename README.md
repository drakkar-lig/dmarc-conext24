# Stress Testing the DMARC Reporting System: Compliance with Standards and Ways of Improvement. Replication code.

This repository contains the code used for generating the table 'Results of the Email Service Provider (ESP) 
measurements showing their adherence to specifications' in the article 
"Stress Testing the DMARC Reporting System: Compliance with Standards and Ways of Improvement"

The article will be published in the proceeding of the 20th International Conference on emerging Networking 
EXperiments and Technologies (CoNEXT'24).

The DOI and link to the article will be added here once the proceedings are published.

# The datasets

This repository does not contain the datasets. 

You can download the zip file 'dmarc-datasets-conext24.zip' from the data repository : https://entrepot.recherche.data.gouv.fr/dataset.xhtml?persistentId=doi:10.57745/IKYMKA and unzipped the archive into the cloned repository.

```bash
git clone https://github.com/drakkar-lig/dmarc-conext24
cd dmarc-conext24
wget --content-disposition 'https://entrepot.recherche.data.gouv.fr/api/access/datafile/:persistentId?persistentId=doi:10.57745/GXFEMF' 
unzip dmarc-datasets-conext24.zip
```
Elaborate datasets and experiment descriptions are provided in the README file in the data 

# Python environtement
The requirements.txt file lists all the necessary libraries to run the Jupyter notebooks using Python version 3.8.10

Run the following command to install the python environment

```
python3.8 -m venv venv
source venv/bin/activate
pip3 install -r requirements.txt
```
Note that the code is designed for a Unix-path environment.

# Table and Data Generation 

The table is generated in the last cell of the Jupyter Notebook 'GenerateData.ipynb'
You can either launch a jupyter-notebook server or run the following command :

```bash
jupytext --execute GenerateData.ipynb
```

The generated data and table can be found in the created folder 'results'. 
Although, the results can be found in the [data repository](https://entrepot.recherche.data.gouv.fr/file.xhtml?persistentId=doi:10.57745/I36UKN).


# Features evaluation

As an example for the ESP Fastmail, each DMARC features can be evaluated as follows : 

- F1 : Verify the presence of the DNS query : TXT _dmarc.fastmailcom.email-sender-1.example
- F2 : Verify the presence of the authentication information in the Authentication-Results email headers received in Fastmail's inbox. 
- F3 : Verify the presence of any aggregate reports towards fastmailcom.email-sender-1.example
- F4 : Verify the presence of any failure reports towards fastmailcom.email-sender-1.example
- F5 : Verify the presence of the DNS query : TXT fastmailcom.email-sender-4.example._report._dmarc.email-receiver-overwrite.example
- F6 : Verify the presence of any aggregate reports towards fastmailcom.email-sender-2.example in the control-domain.example inbox
- F7 : Verify the absence of any aggregate reports towards fastmailcom.email-sender-3.example in the email-recevier-invalid-edv.example inbox
- F8 : Verify that aggregate reports towards email-sender-4.example are sent to redirectionRUA@email-receiver-overwrite.example instead of rua@email-receiver-overwrite.example

All those evaluations are made in the Jupyter Notebook GeneratedData.ipynb. 