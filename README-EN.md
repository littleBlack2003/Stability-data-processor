# StabLab Processor User Guide

## 1. Introduction

StabLab Processor is a data analysis and visualization software specifically designed for organic and perovskite solar cell stability testing. It can quickly parse multi-channel test logs, generate visualization curves for Fill Factor (FF), Open-Circuit Voltage (Voc), Short-Circuit Current (Isc), Maximum Power (Pmax), and Cumulative Energy Yield, and supports flexible multi-channel data grouping and one-click export.

## 2. Key Features

- **Multi-Dimensional Data Visualization**: Seamlessly switch between curves for FF, Voc, Isc, Pmax, and Cumulative Energy Yield.
- **Flexible Data Grouping**: Import configuration files to batch group and uniformly color test channels for comparison.
- **Intelligent Data Processing**: Built-in calculus algorithms automatically calculate the cumulative energy yield (mWh) of devices based on power and timestamps.
- **Data Export**: Export processed and cleaned data from the current view to standard CSV format, convenient for importing into professional plotting software such as Origin.
- **Offline Operation**: Can be packaged as a local desktop application to meet the security requirements of laboratory environments without internet access.

## 3. Data Format Specifications

### 3.1 Test Data Files (Log Files)

The software supports importing standard CSV or TXT format test logs.

- **File Naming Requirement**: The filename must contain a channel identifier in the format `C` + number (e.g., `data_C001.txt`, `sample_C012.csv`). The software will automatically extract `C001` or `C012` as the channel name for that curve.
- **File Content Requirement**: Data must be comma-separated and must include the following headers (case-sensitive, including units in parentheses):
  - `Time`: Timestamp (e.g., `2023-10-01 12:00:00`)
  - `Isc(mA)`: Short-circuit current
  - `Voc(V)`: Open-circuit voltage
  - `Pmax(mW)`: Maximum power
  - `FF(%)`: Fill factor

**Test Data File Example (`data_C001.csv`):**

```csv
Time,Isc(mA),Voc(V),Pmax(mW),FF(%)
2023-10-01 10:00:00,20.5,1.05,17.2,80.0
2023-10-01 10:05:00,20.4,1.04,17.0,79.8
2023-10-01 10:10:00,20.6,1.05,17.3,80.1
```

### 3.2 Grouping Configuration File (Cluster Config)

If you need to group multiple channels for comparison (e.g., comparing degradation of different encapsulation materials), you can import a grouping configuration file.

- **File Format**: CSV format (`.csv`)
- **Header Requirements**:
  - `Group`: Group name (e.g., Control Group, Experimental Group A).
  - `Color`: Display color for the group in the chart. Supports HEX color codes (e.g., `#FF5733`) or standard English color names (e.g., `blue`, `red`).
  - `Channels`: Channel numbers included in the group. Supports comma separation and hyphen ranges (e.g., `"1-5, 8, 10-12"` represents channels 1,2,3,4,5,8,10,11,12). **Note**: If commas are included, the entire field must be enclosed in double quotes.

**Grouping Configuration File Example (`groups.csv`):**

```csv
Group,Color,Channels
Control Group,#FF5733,"1-3, 7"
Experimental Group A,#33FF57,"4-6"
Experimental Group B,blue,"8, 10-12"
```
## 4. Operation Steps

1. **Import Data**: In the left sidebar, click the "Upload Files" area and select one or more test data files that conform to the format (e.g., `C001.txt`, `C002.txt`).
2. **Switch Views**: Click on different parameter tabs (FF, Voc, Isc, Pmax, Cumulative Energy Yield) above the chart. The chart will update in real-time, and the axis ranges will adjust automatically.
3. **Configure Grouping**: Click the "Import Grouping Configuration" button at the bottom of the left sidebar, upload the prepared `groups.csv` file. The chart lines will be automatically recolored and grouped according to the configuration, and the legend will be updated accordingly.
4. **Export Data**: Click the "Export CSV" button in the upper right corner to save the processed data from the current view (including calculated cumulative energy yield, etc.) to your local computer.

## 5. Changelog

### V1.1

- **Multi-channel Aligned Data Export**: Added the "Data Analysis Export" module in the sidebar. Supports exporting the currently selected parameters (e.g., FF, Voc, Isc, Pmax) as a standard CSV file.
- **Automatic Time Alignment**: The system automatically extracts and aligns the time union of all loaded channels.
- **Wide Format Export**: The exported CSV has the time axis as the first column, followed by each channel as a separate column (e.g., C001, C002...). Missing values are left blank automatically.

### V1.3

- Fixed the issue of slow software response and added the integral cumulative energy yield function.

## 6. Maintainer Information

Contact: xiaohei.wu@whu.edu.cn
