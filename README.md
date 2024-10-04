# MVF Protocol: Example Usage

## Overview

R script and a zipped file with example data to implement the Movement Verified Filtering (MVF) protocol. The MVF protocol is designed to distinguish genuine movement in animals using high-resolution GPS and motion sensor data. It combines velocity estimates from GPS data with Dynamic Body Acceleration (DBA) to identify and filter out erroneous or non-movement GPS fixes.

The script provided here was developed for an **African lion (Panthera leo)** dataset, where motion sensor data was collected using a **Daily Diary (DD)** device (10 Hz), and GPS data was collected at 1 Hz using a **Technosmart GiPSy-5** device. The MVF protocol aims to accurately classify traveling movement while filtering out inaccuracies, such as noise from resting behavior or low-quality GPS fixes. This approach is specifically tailored for **high-resolution GPS datasets** (e.g., 1 Hz), where frequent fixes can lead to significant positional errors if not properly filtered.

## Download the Example Dataset
Due to the large size of the dataset, you can download the example dataset used in this project from the following link:

[https://github.com/Richard6195/Movement-Verified-GPS-Filtering-Protocol/releases/tag/v1.0.0/Example.dataset.zip]

 ### For more information on the methodology and specific parameters used in the MVF protocol, please refer to the associated publication:

**"Decision rules for determining terrestrial movement and the consequences for filtering high-resolution global positioning system tracks: a case study using the African lion (Panthera leo)"** [https://royalsocietypublishing.org/doi/full/10.1098/rsif.2021.0692]

## Description

The **MVF protocol** script walks through the process of using GPS and motion sensor data to identify genuine traveling movements. The following major steps are covered:

- **Data Preparation**: Load and preprocess GPS and motion sensor data, ensuring timestamps are aligned and properly formatted for analysis.
- **Compute VeDBA**: Calculate **Vectorial Dynamic Body Acceleration (VeDBA)** to indicate movement intensity.
- **Compute GPS-derived Speed**: Calculate GPS speed using **Haversine distances** and filter out extreme outliers.
- **MVF Filtering**: Apply thresholds to **DBA**, GPS-derived speed, and positional consistency to determine valid movement periods (genuine traveling).
- **Time Thresholds**: Identify continuous movement segments meeting temporal criteria for classification as genuine movement.

The script is structured to be adaptable, allowing different thresholds for various parameters to be set according to the requirements of other species or datasets.

## Required Libraries

The following R packages are required to run the MVF script:

- **zoo**: For rolling mean calculations.
- **dplyr**: For data manipulation.
- **lubridate**: For timestamp handling and time operations.
- **ggforce**: For enhanced ggplot2 plotting capabilities.
- **tidyverse**: For general-purpose data wrangling and visualization.
- **ggplot2**: For generating plots.

## Setting the Working Directory

Before running the script, you need to ensure that your working directory is set correctly. After downloading and unzipping the repository, set the working directory to the folder containing the data and script files. This allows the script to access the necessary data files for motion sensor and GPS data.

### Instructions:
1. Unzip the repository into a folder on your computer (e.g., in your "Documents" or "Downloads" folder).
2. Open the R script in your R environment.
3. Modify the following line in the script to reflect the path where you unzipped the repository:

```r
setwd("/path/to/your/unzipped/repository")
```
## Steps Covered in the Script

### 1. Load and Subset Motion Sensor Data (included in a .zip file within this repository)
- Load motion sensor (DD) data from multiple `.txt` files and combine them into a single data frame.
- Create and format timestamp columns.
- Subset data to a specific time period.

### 2. Compute Static and Dynamic Acceleration
- Compute static acceleration by applying a smoothing window.
- Calculate **VeDBA** as an indicator of overall body acceleration intensity.

### 3. Load and Preprocess GPS Data
- Load GPS data and create timestamps.
- Subset GPS data to match the motion sensor time period.

### 4. Compute GPS-derived Speed
- Calculate distances using the **Haversine formula** and compute GPS speed by dividing distance by time intervals.

### 5. Merge Motion Sensor and GPS Data
- Merge GPS and motion sensor data, matching timestamps and filtering out unmatched points.
- Create interpolated GPS speed values for short gaps in GPS coverage.

### 6. Apply MVF Protocol Thresholds
- Apply thresholds (e.g., **VeDBA** and GPS speed) to identify potential movement periods.
- Merge small gaps between movement periods and classify those exceeding the time threshold as genuine movement.

### 7. Investigatory Plots
- Generate diagnostic plots to visualize filtered movement data and thresholds.

## Reference to Publication

The methodology for this script is detailed in the publication:

**"Decision rules for determining terrestrial movement and the consequences for filtering high-resolution global positioning system tracks: a case study using the African lion (Panthera leo)"**, published in the Journal of the Royal Society Interface. [https://royalsocietypublishing.org/doi/full/10.1098/rsif.2021.0692]

## Usage Notes

- This example uses data from an African lion, but thresholds and processes can be adjusted for different species or datasets.
- Ensure the working directory is set correctly before running the script.
- The MVF filtering method is particularly well-suited for high-resolution GPS datasets, such as those collected at 1 Hz, where frequent GPS fixes can introduce positional errors if not filtered.

## License

This project is licensed under the MIT License - see the `LICENSE` file for details.

## Contact

For questions or suggestions, feel free to contact me at [rgunner@ab.mpg].
