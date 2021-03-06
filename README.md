# gsheet-api
Easily and efficiently manage a Google Sheet.

## Install
```sh
pip install gsheet-api
```

## Notes
- Credentials required are the Google Service account json file
  - [Creating a Google Serivice Key](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)
- Sheet must be shared with edit access to the `client_email` found the the service account
- Credentials can be entered as a dictionary or a file path to a json file, both will work.

## Usage Example
**\*\*Required arguments are defined in the "Available Methods" section**
```python
from gsheet_api import GSheetAPI

gsheet = GSheetAPI(**)        # initialize the class
gsheet.sheet_to_df(**)        # import data from the sheet to a Pandas DataFrame

gsheet.change_gsheet(**)      # switch to a new Google Sheet to work off of
gsheet.get_cell(**)           # get the contents of a single cell

gsheet.change_tab(**)         # switch to a new tab in the current working Google Sheet
gsheet.set_cell(**)           # set the value of a single cell
gsheet.df_to_sheet(**)        # export a Pandas DataFrame to the current working sheet
gsheet.timestamp_to_cell(**)  # export a timestamp to a single cell in the sheet
```

## Available Methods
```
__init__(self, credentials, sheet_id, tab_name)
    Initializes the GSheetAPI and sets the current working sheet and current working tab
    :param dict|str credentials: Dictionary containing your Google Service Account json blob or a file
        path entered as a string
    :param str sheet_id: Sheet id found in the Google Sheet URL
    :param str tab_name: Name of the tab to use within the Google Sheet

change_gsheet(self, sheet_id, tab_name)
    Changes the current working sheet
    :param str sheet_id: Sheet id found in the Google Sheet URL
    :param str tab_name: Name of the tab to use within the Google Sheet

change_tab(self, tab_name)
    Changes the working tab name within the current sheet
    :param str tab_name: Name of the tab to use within the Google Sheet

df_to_sheet(self, df_input, row_start, col_start, clear_sheet=False, clear_range=None, allow_formulas=True, 
            include_index=False, resize=False, include_column_header=True)
    Exports a Pandas DataFrame to a Google Sheet
    :param pandas.DataFrame df_input: DataFrame to export
    :param int row_start: Integer value of the row (starting at 1)
    :param int col_start: Integer value of the column (starting at 1)
    :param bool clear_sheet: (default False) If the entire sheet should be cleared before dumping data
    :param bool clear_range: (default None) A range that should be cleared (eg. 'A1:B12')
    :param bool allow_formulas: (default True) Whether or not formulas should be executed or shown as a raw string
    :param bool include_index: (default False) Whether or not the DataFrame index should be shown in the sheet
    :param bool resize: (default False) If the sheet should resize when the data is too large to fit in the sheet
    :param bool include_column_header: (default True) If the data header should be dumped into the sheet

get_cell(self, cell)
    Gets the current value of a given cell in the sheet
    :param str cell: Cell reference (eg. 'A2')
    :return: The current contents of the cell

set_cell(self, cell, cell_content)
    Sets a cell to a given value
    :param str cell: Cell reference (eg. 'A2')
    :param str cell_content: Desired cell content

sheet_to_df(self, col_list, header, evaluate_formulas)
    Grabs data from a Google Sheet and returns it as a Pandas DataFrame
    :param list col_list: List of ints representing the column number to extract (eg. range(0, 4) for [0, 1, 2, 3])
    :param int header: Integer of the row to use as a column (0 indexed)
    :param bool evaluate_formulas: Whether or not the formulas should be computed before extracting the cell content
    :return pandas.DataFrame: The sheet contents as a DataFrame object

timestamp_to_cell(self, cell, fmt='%Y-%m-%d %H:%M %Z', tz='US/Central')
    Exports a timestamp to a single cell in the Google Sheet
    :param str cell:
    :param str fmt: (default "%Y-%m-%d %H:%M %Z")
    :param str tz: (default "US/Central")
```
