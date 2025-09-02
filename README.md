# Terminal Management System - Usage Guide

## 📋 **Quick Setup Guide**

### **Step 1: Install Required Libraries**
```bash
pip install gspread pandas openpyxl xlsxwriter google-auth
```

### **Step 2: Configure Your Credentials**
Replace the following placeholders in the code:

```python
# REPLACE THESE VALUES WITH YOUR OWN:
service_account_info = {
    "project_id": "YOUR_PROJECT_ID",           # Your Google Cloud Project ID
    "private_key": "YOUR_PRIVATE_KEY",         # Your Service Account Private Key
    "client_email": "YOUR_CLIENT_EMAIL",       # Your Service Account Email
    # ... other fields
}

# REPLACE THESE SPREADSHEET IDs:
SOURCE_ID = "YOUR_MAIN_SPREADSHEET_ID"         # Main system spreadsheet
TERMINAL_ID = "YOUR_TERMINAL_SPREADSHEET_ID"   # Terminal data spreadsheet  
VPOS_ID = "YOUR_VPOS_SPREADSHEET_ID"          # VPOS data spreadsheet
```

### **Step 3: Grant Permissions**
Add your service account email to all Google Sheets as **Editor**:
- Main spreadsheet
- Terminal spreadsheet
- VPOS spreadsheet

---

## 🔧 **Configurable Settings**

### **1. Bank Configuration**
```python
# Modify these lists to add/remove banks:
BANKS = ['HALKBANK', 'ANADOLUBANK', 'VAKIFBANK', 'DENIZBANK', 'AKBANK']
VPOS_BANKS = ['ISBANK', 'QNB', 'TFKB', 'DENIZBANK', 'VAKIFBANK', 'AKBANK', 'HALKBANK']
```

### **2. File Size Settings**
```python
# Change rows per Excel file:
CHUNK_SIZE = 100000  # Current: 100K rows per file
# Options: 50000 (50K), 150000 (150K), 200000 (200K)
```

### **3. Output File Naming**
```python
# Modify file naming pattern:
excel_file_name = f"terminal_management_system{file_number:02d}_{timestamp}.xlsx"
# Change to: f"custom_report_{file_number:02d}_{timestamp}.xlsx"
```

### **4. Column Headers**
```python
# Customize Excel column names:
column_headers = [
    'Mali No', 'Org ID', 'Bank Name', 'Bank Status',
    # Add/modify column names as needed
]
```

---

## 🎯 **Usage Examples**

### **Basic Usage:**
```python
# Run quick test (1000 rows)
quick_test()

# Generate full report
create_excel_report()
```

### **Advanced Usage:**
```python
# Custom chunk size
CHUNK_SIZE = 50000  # 50K rows per file
create_excel_report()

# Different timestamp format
timestamp = datetime.now().strftime("%Y_%m_%d")
```

---

## 📊 **Data Processing Rules**

### **1. Sales Status Conversion:**
- `evet` (yes) → `Passive`
- `hayir` (no) → `Active`

### **2. Bank Status Conversion:**
- `var` → `Completed`
- `red` → `Rejected`
- `banka bekleniyor` → `Awaiting Response`
- `yok` or empty → `Not Sent`

### **3. Terminal Type Classification:**
- Main DB records → `PHYSICAL POS`
- VPOS DB records → `CEPTEPOS`

### **4. Request Type Logic:**
- Has cancellation data → `Deletion`
- No cancellation data → `Installation`

---

## 🔄 **Customization Options**

### **1. Add New Status Categories:**
```python
def convert_bank_status(value):
    # Add new status mappings:
    if 'new_status' in value_str:
        return 'New Category'
    # ... existing code
```

### **2. Modify Color Schemes:**
```python
# Change Excel conditional formatting colors:
worksheet.conditional_format(f'D2:D{row_count + 1}', {
    'type': 'text', 'criteria': 'containing', 'value': 'Completed',
    'format': workbook.add_format({'bg_color': '#YOUR_COLOR'})  # Change color
})
```

### **3. Add New Data Sources:**
```python
# Add new spreadsheet:
NEW_SPREADSHEET_ID = "YOUR_NEW_SHEET_ID"
new_workbook = gs_client.open_by_key(NEW_SPREADSHEET_ID)

# Add to parallel processing:
executor.submit(fetch_sheet_data, new_workbook, "Sheet_Name"): "NEW_DATA"
```

### **4. Filter Data:**
```python
# Add data filtering before processing:
if mali_no.startswith('FILTER_PREFIX'):
    # Process only specific mali numbers
    continue
```

---

## 📁 **Output File Structure**

### **File Naming Convention:**
```
terminal_management_system01_20241202_1430.xlsx
terminal_management_system02_20241202_1430.xlsx
...
```

### **Excel Sheet Structure:**
- **Sheet Name:** Terminal Management
- **Columns:** 20 columns (Mali No to Bank TID)
- **Formatting:** Headers, colors, conditional formatting
- **Features:** Frozen panes, auto-width columns

---

## ⚠️ **Important Notes**

### **1. Service Account Setup:**
1. Go to [Google Cloud Console](https://console.cloud.google.com/apis/credentials)
2. Create Service Account
3. Download JSON key
4. Replace credentials in code
5. Enable Google Sheets API and Google Drive API

### **2. Permissions:**
- Add service account email to ALL Google Sheets as **Editor**
- Ensure sheets are accessible by the service account

### **3. Error Handling:**
- Check internet connection for Google Sheets access
- Verify spreadsheet IDs are correct
- Ensure sufficient disk space for output files

### **4. Performance:**
- Processing time depends on data size
- Large datasets may take 15-30 minutes
- Monitor memory usage for very large files

---

## 🚀 **Quick Start Commands**

```python
# 1. Test the system
quick_test()

# 2. Generate full report  
create_excel_report()

# 3. Check output files
import os
files = [f for f in os.listdir('.') if f.startswith('terminal_management')]
print(f"Generated {len(files)} files")
```

This system provides a complete terminal management reporting solution with full customization capabilities for enterprise use.
