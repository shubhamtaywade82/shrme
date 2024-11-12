212# Introduction
This app is a tool for calculation inventory need and allocating accross multiple locations & warehouses.

# Key Features

# Version List
### 2.55
    - Updated Azure App Secret
    - Fixed required fields issue in RMA transfer uploads
    - Updated SMTP to use Sendgrid
    - Updated Store to Store Transfer Store List Excel File
### 2.50
    - API Error Handling (500 errors issue) - Pop Up Messages instead of spinning
    - Resolve error issue when running Allocation Search for the first time
    - First size doubling up in Min-Max page
    - Added Checks for required fields for all file upload types (Transfers, Manual Alloc, RMA)
    - Modified instructions for all Uploads
### 2.40
    - Change Inventory Calculation Metrics GET to POST
    - Query Performace optimization for Inventory Calculation Metrics
### 2.30
    - Expansion & Collapse to the Store & Size level in the Allocation Table
    - Sort table by Adj Alloc Desc
### 2.20
    - Summary Page for Meghan
    - Resolve puma bug for Query Token MAX LENGTH
### 2.15
    - Fix WTD Sales calculation that was showing double
    - Fix Min-Max display which was showing 0 for several items
### 2.10
    - UK Cost added for integration with FC
### 2.00
    - Update store_fc_codes.xlsx file in the images folder
    - Update TABULAR_USERNAME & TABULAR_PASSWORD in the env file
    - Added MARYLEBONE to submit_allocation.jsx
    - Modified SuperAdmins section in the manual_allocation.jsx
    - Updated transfer_functions.js to add MARYLEBONE
### 1.99
    - Add Readme
    - Change Environment Variables to reference config

### 1.97d
    - remove bad logs

### 1.97c
    - Update build and readd min max functionality. 
    - Add validation for RA uploads
    - Add specific logging/titles for archive.

### 1.97b
    - Add distinction to file titles for archive Manual Allocations vs Uploads
    - Add distinction to log for archive for Manual Allocations vs Uploads

### 1.97a
    - Update has map functionality
    - update tabulator


### 1.95h
    - add min-max upload by store functionality.


### 1.95g
    - Remove issue with min values not being properly applied

### 1.95f
    - Remove line causing bug in calculation sales metrics for ecomm allocation.

### 1.95c
    -  Update transfer_archive to include test_transfer transfers
    -  add store name validation to upload

### 1.95b
    - update sleep timer again for sftp transfer logic.
    - Add explicit connection close to sftp transfer.

### 1.95
    - comment out ability to update single store at a time for min/max
    - Update sleep timer for sftp transfer logic.
    - Add test logic for sftp transfer

<!-- #### 1.95 
    - Update tabulator.
    - Update hash map functionality
    - Add ability to update single store at a time for min max -->

#### 1.94 
    - update SFTP credentials

#### 1.93b 
    - fix issue with extra javascript action being called causing allocation issue.
#### 1.93
    - update check to see if same file has been uploaded in same day

#### 1.92e
    - update sftp creds

#### 1.92d
    - update alerts for webhooks_backups

#### 1.92c 
    - Adjust schedule for chron

#### 1.92b
    - Fix manual allocation error

#### 1.92
    - Add critical mailers to webhook monitoring

#### 1.91
    - add toggle in allocation upload to set replen shipping

#### 1.90
    - add error modal on long transfer

#### 1.89b

 - update issues with date validation
 - update schedule logging and correct table name error for cron jobs

#### 1.89

- Update cron task to include distinction for channel type when checking order events

#### 1.88

- Fix min-max upload issue that was preventing correct files from being uploaded.

#### 1.87c 

- fix issue with dates being too picky on upload.

#### 1.87b

- fix issue with column header for warehouse for manual allocation in incorrect place

#### 1.87

- Add ability to re-export ecomm orders
- Add error handling for min max upload
- move WOS next to min/max

#### 1.86

- Add date check to upload for Transfer

#### 1.85

- finish min-max
- add better error handling for sftp.
- add better error logging for sftp and min max
- add extra variable removal. for table page.

#### 1.84

- Add refresh to navigation to improve memory.F
- remove extra let statements to improve memory.
- Add min max upload functionality
- fix click outside bug for
- comment out min/max upload selection prior to improvements

#### 1.83

- add compression to json_blobs to improve performance for saved results

#### 1.82d

- fix issue with dates for manual allocation upload

#### 1.82b

- fix order number issue and column order

#### 1.81c

- fix sftp issue

#### 1.81b

- add export functionality for csv
- slightly modify webhook schedule

#### 1.81

- Add error logs and error handling for SFTP.
- Allow a user to see all current working plans.
- Add additional errors to exclusion for errors log alert.
- Remove erroneous extra sftps from broken line items

#### 1.80b

- Add logic to update RTV customer number for Dray.

#### 1.80

- add webhoook backups controller and models
- fix expired authorization cert
- update deduplication logic for webhook events.

#### 1.79c

- fix webhokos_tests controller

#### 1.79b

- update loggers for webhooks
- update loggers for errors
- fix date for archived logs

#### 1.79

- correctly add sleep
- update path error for cron/webpacker issue
- set up logs to archive daily
- change emails to 1 for each category

#### 1.78h

- add sleep and attempt to deal with issue with path

#### 1.78

- update bulk selection to filter based off of UK location
- update exports to include warehouse column and
- add ssh login
- add logging
- add scheduled emails and error checks
- add cron & ssh to docker image

#### 1.77b

- update ecomm transfers to download

#### 1.77

- add secondary webhooks controller
- fix sku selection bug
- remove max-override pop-up

#### 1.76

- fix webhooks controller
- fix apply_min
- fix max overried min_applied status logic
- fix store level update logic

#### 1.75

- fix issue with bulk numbers and references in upload allocations not being long enough.
- allow user to override min max
- fix submitting allocation bug
- fix show product style on lower style levels.

#### 1.74b

- fix webhook bug

#### 1.74

- fix bug with bulk ata/wh ata being incorrect if bulk ATA is 0
- ensure seven character string literal for bulk reference number

#### 1.73f

- enable SFTP for STS
- limit RTV size to 100

#### 1.73d

- correct rma template error
- set default file download to txt only.

#### 1.73c

- update to STS transfers to fix bug with upload
- addition of RTV, STS and Allocation StoreList files
- Reduction to 0 of - RTVs and STSes

#### 1.73b

- fix bulk sort issue
- add bulk sort loader
- fix issue where historical allocation wasn't loaded.

#### 1.73

- Add shipping method setting to store settings page.
- Add Bulk info to submitted allocation review page.

#### 1.72e

- update shipping for STS and RTV

#### 1.72d*2

- fix webhook issue for return item events.

#### 1.72c

- update RMA to no longer split files into 100

#### 1.72b

- update file titles for transfers and allocations.

#### 1.72

- Update ecomm transfers for allocations

#### 1.71

- Fix warehouse selection issue for Draycott.
- Add split functionality for RTV files (split into files of 100 or less).
- Add spacing to download to allow for more than 10 files.

#### 1.70

- Update transfer timestamps & transfer titles for RMA, STS and Uploads.
- Turn on SFTP for allocations through table. Split files on allocation through table.
- Add Draycott information to allocations.
- Fix color code on allocation export.
- Add column header check on transfer uploads.

#### 1.69

- Refactor of upload process to improve performance and add support for massive files/
- addition of failsafe for dev tools on production.
- removal of automatic edit of ecom min*maxes on apply all button on min*max page.

#### 1.68c

- fix store calculation bug introduced from #### 1.68b

#### 1.68b

- fix ecomm calculations leading to incorrect ideal
- fix proportionate storeweight calculation bug introduced as a result of changed primary keys.

#### 1.68

- Add warehouse warehouse selection logic for UK. This includes selection of UK stores overriding seletion of US stores.
- Change Version button to About pop*up.

#### 1.67

- STS, RTV and Manual allocations have been updated to properly handle large files (300 rows +) for creation and transfer over SFTP
- UK Company Name  and FullCircle Code have been added to store creation page.
- SFTP has been enabled for transfer orders created through the allocation interface, and ECOMMERCE allocation files have been disabled over SFTP.
