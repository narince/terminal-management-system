# Data Management System - Complete Usage Guide

## 📋 **System Overview**

This system is designed to consolidate and process data from multiple Google Sheets sources into comprehensive Excel reports. It handles large datasets efficiently and provides detailed analysis with customizable formatting.

### **Key Features:**
- **Multi-source data integration** from Google Sheets
- **Large dataset processing** (millions of records)
- **Automated Excel generation** with professional formatting
- **Parallel data retrieval** for optimal performance
- **Customizable data mappings** and transformations
- **Local file storage** eliminating download issues

## 🔧 **Required Configuration**

### **1. Service Account Setup**
```python
# REQUIRED: Replace these values with your Google Cloud credentials
service_account_info = {
    "project_id": "YOUR_PROJECT_ID",           # Your Google Cloud Project ID
    "private_key": "YOUR_PRIVATE_KEY",         # Your Service Account Private Key
    "client_email": "YOUR_SERVICE_ACCOUNT",    # Your Service Account Email
    # ... other credentials
}
```

### **2. Data Source Configuration**
```python
# REQUIRED: Replace with your Google Sheets IDs
GOOGLESHEET1_ID = "YOUR_MAIN_SPREADSHEET_ID"      # Primary data source
GOOGLESHEET2_ID = "YOUR_SECONDARY_SPREADSHEET_ID" # Secondary data source  
GOOGLESHEET3_ID = "YOUR_THIRD_SPREADSHEET_ID"     # Third data source

# REQUIRED: Replace with your actual sheet tab names
"MainData"        # Replace with your main data sheet name
"Submissions"     # Replace with your submissions sheet name
"Cancellations"   # Replace with your cancellations sheet name
```

### **3. Data Mapping Configuration**
```python
# OPTIONAL: Customize data source names
DATA_SOURCES = ['DATA1', 'DATA2', 'DATA3', 'DATA4', 'DATA5']
SECONDARY_SOURCES = ['SOURCE1', 'SOURCE2', 'SOURCE3', ...]

# REQUIRED: Adjust column mappings to match your data structure
DATA_SUBMISSION_SCHEMA = {
    'DATA1': {'key': 0, 'cols': [1, 2, 3, 4]},  # Adjust column indices
    # ... configure for each data source
}
```

## 🎯 **What This System Does**

### **1. Data Integration**
- **Connects to multiple Google Sheets** simultaneously
- **Retrieves data in parallel** for faster processing
- **Handles different data structures** from various sources
- **Combines related records** across multiple sheets

### **2. Data Processing**
- **Normalizes data formats** across different sources
- **Converts status values** to standardized terminology
- **Merges related records** based on unique identifiers
- **Applies business rules** for data classification

### **3. Excel Generation**
- **Creates multiple Excel files** (100K rows each)
- **Applies professional formatting** with colors and styles
- **Includes conditional formatting** for visual data analysis
- **Provides comprehensive data analysis** with statistics

### **4. Business Logic Processing**
- **Request Type Classification:** Installation vs Deletion
- **Status Processing:** Maps various status values to standard categories
- **Date/Time Handling:** Combines and formats date/time data
- **Cross-reference Validation:** Verifies data consistency across sources

## 📊 **Customizable Elements**

### **1. Data Sources**
```python
# Modify according to your organization's data sources
DATA_SOURCES = ['DEPT_A', 'DEPT_B', 'SYSTEM_X', 'PLATFORM_Y']
```

### **2. Status Mappings**
```python
# Customize status conversion logic
def convert_data_status(value):
    if 'approved' in value_str:
        return 'Completed'
    elif 'denied' in value_str:
        return 'Rejected'
    # Add your specific status mappings
```

### **3. Column Structure**
```python
# Adjust column headers for your Excel output
column_headers = [
    'Unique_ID', 'Department', 'System_Name', 'Current_Status',
    'Created_Date', 'Updated_Date', 'Notes', 'Priority',
    # Customize according to your requirements
]
```

### **4. File Output**
```python
# Customize file naming and size
CHUNK_SIZE = 75000  # Rows per file
excel_file_name = f"monthly_report_{file_number:02d}_{timestamp}.xlsx"
```

## 🚀 **Usage Instructions**

### **Basic Usage:**
```python
# Test the system with sample data
quick_test()

# Generate complete reports from your data
create_excel_report()
```

### **Advanced Configuration:**
1. **Modify data source names** to match your organization
2. **Adjust column mappings** to fit your spreadsheet structure  
3. **Customize status conversions** for your business logic
4. **Set appropriate file sizes** based on your requirements

### **Prerequisites:**
1. **Google Cloud Project** with Sheets API enabled
2. **Service Account** with appropriate permissions
3. **Google Sheets access** for the service account
4. **Python environment** with required libraries

This system provides a robust foundation for enterprise data management and reporting, with full customization capabilities to adapt to any organizational structure or data format.