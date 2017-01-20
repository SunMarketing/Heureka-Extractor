# Hereuka.cz extractor
KBC Docker app for extracting data from Heureka (http://heureka.cz)

The Extractor gets list of campaign stats for previous day and saves the data to Storage API. Date of downloaded stats can be changed in configuration.


## Configuration

- **parameters**:
    - **username** - Username to Heureka
    - **password** - Password to Heureka
    - **bucket** - Name of bucket where the data will be saved
    - **since** *(optional)* - start date of downloaded stats (default is "-1 day")
    - **until** *(optional)* - end date of downloaded stats (default is "-1 day")
    - **eshopId** - Eshop Id in Heureka
    - **showSources** ```true/false```

## Output

Data are saved into table **incrementally**:

**stats** - contains marketing stats, columns are:
- **eshopId** 
- **date** 
- **visits**   
- **cpc** 
- **spend**
- **conversion_rates** 
- **orders** 
- **aov**
- **transaction_revenue**
- **pno**
- **source** `source is downloaded by setting optional parameter showSources to true`


> **NOTICE!**
> - Data can change for last 30 days
> - Data from previous day are available at morning


## Installation

If you want to run this app standalone:

1. Clone the repository: `git@bitbucket.org:matla/heureka-extractor.git ex-heureka`
2. Go to the directory: `cd ex-heureka`
3. Install composer: `curl -s http://getcomposer.org/installer | php`
4. Install packages: `php composer.phar install`
5. Create folder `data`
6. Create file `data/config.yml` with configuration, e.g.:

    ```
    parameters:
      username:
      password:
      eshopId:
      bucket: in.c-heureka
      showSources: true/false
    ```
7. Run: `php src/run.php --data=./data`
8. Data tables will be saved to directory `data/out/tables`
