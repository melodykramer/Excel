![UNC Libraries logo](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image1.png?raw=true)
# Working with Data in Excel

### **[Download Companion Excel Sheet](https://github.com/UNC-Libraries-data/Excel/raw/master/Excel_Workshop.xlsx)**

*[ ] indicate sheet names in the companion Excel workbook*


## Table of Contents:
* [Getting Started](#getting-started)
* [Functions](#functions)
* [Common Problems](#common-problems)
	+ [Delimiters](#splitting-on-delimiters)
	+ [Filling Blanks](#filling-blanks)
* [VLOOKUP](#vlookup)
* [Pivot Tables](#introduction-to-pivottables)


## [Getting Started]

### Shortcuts


| To... | Windows | Mac |
|-------|---------|-----|
| Find and replace | CTRL+F | &#8984;+F |
| Move to the edge of the data region | CTRL+Arrow key | &#8984;+Arrow key |
| Select to the edge of the data region | CTRL+SHIFT+Arrow key| &#8984;+SHIFT+Arrow key |
| Select entire column | CTRL+SPACEBAR | CTRL+SPACEBAR |
| Select entire row | SHIFT+SPACEBAR | SHIFT+SPACEBAR |
| Enter value into all selected cells* | CTRL+ENTER | ^+RETURN |

*Highlight empty cells; type the value you want to enter in all of them; press the shortcut keys.

### Best Practices and [Tidy Data](http://vita.had.co.nz/papers/tidy-data.pdf)
* Each row is as an "observation" at a consistent level (e.g. no totals mixed in)
* Each column as a "variable" or "field".
	+ Don't store more than one piece of information in a cell.
* Avoid color or other formatting alone to encode data.
* Only one table per sheet.
* Blank cells indicate missing values, zeroes indicate **observed zeroes**.
* Comments or notes should be integrated as a separate column or stored separately.

Try saving your data as a .csv (common separate values) file. This saves just the active sheet sheet *without formatting*.

## [Functions]
### Using Functions in Excel
* `=SUM()`
* `=AVERAGE()`
* `=MEDIAN()`
* Etc.

![Example of using SUM function in Excel](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image2.png?raw=true)

### Working with Text
* `=LEFT()` Extracts a specified number of characters from a variable, counting from the left
	+ `=RIGHT()` same as above, but counting from the right
* `=TRIM()` Removes all whitespace aside from single spaces between words
* `=CONCATENATE()` combines multiple strings into a single string

### Pasting
* **Paste Special**: Making Functions Permanent
	* Right-click: Copy
	* Right-click: Paste Special > Values
* **Paste[Transpose]**
	* Right-click: Copy
	* Right-click: Paste Special > Transpose

## Common Problems:
### [Splitting] on Delimiters
The "Text to Columns" tool (Data Tab>) lets you split a cell into multiple cells based on width or a special character (delimiter).

![Text to columns example in Excel](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image3.png?raw=true)

### Filling [Blanks]
When dealing with human-readable text, we often have categories listed once with the implication that all lines before the next category fall into this group. For example, in the Blanks sheet we might assume that Bertie Rudolph is a Freshman. While this is human readable, the relationship won't be clear to the computer!
* (PC) Home Tab, Editing > Find & Select > Go to Special > Blanks > OK
* (Mac) Edit Menu > Find > Go To...> Special... > Blanks > OK
* Type =, then hit the up directional arrow. Hit CTRL+Enter (PC) or &#8984;+Enter (Mac)
![Filling blanks example in Excel](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image4&5.PNG?raw=true)

### Cell References

In each of our formulas so far, we've referred to cells like this:

`=A1`

to indicate the first row of column A.  When we copy or drag this reference one cell to the right it becomes B1, or if we drag it one cell down, it automatically becomes A2.

Sometimes we don't want our references to change as we drag our formulas.  [Absolute references](https://support.office.com/en-us/article/switch-between-relative-absolute-aand-mixed-references-dfec08cd-ae65-4f56-839e-5f0d8d0baca9) provide unchanging references by placing a $ before the column letter and row number:

`=$A$1`

The reference above will stay the same no matter where we move it.

## [VLOOKUP]
The VLOOKUP function provides a way to merge or join additional data into a dataset, using a common code or value.

![VLOOKUP example in Excel](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image8.png?raw=true)


**`=VLOOKUP(A3,$F$3:$G$9,2,FALSE)`**

|Parameter|Value|Description|
|---------|-----|-----------|
|lookup_value|A3|_Value in our main table_ that we're looking to match in the other table|
|table_array|$F$3:$G$9|The _other table_ we need information from (lock references with $)|
|col_index_num|2|The _column from the other table_ we're looking for|
|[range_lookup]|FALSE|Whether you want approximate matches [TRUE] or exact matches [FALSE]|

VLOOKUP can refer to a value in a different sheet or even different workbook on your computer.  If you click into a cell on the other table while filling out your VLOOKUP formula, it will automatically supply the reference necessary to link to the other sheet or workbook.

**Exercise: [Ex_Main],[Ex_Lookup]**

## Introduction to PivotTables

### [Pivot_Tables_IPEDS.xlsx](https://github.com/UNC-Libraries-data/Excel/raw/master/Pivot_Tables_IPEDS.xlsx)

PivotTables create cross-tabulations displaying values split out across categories displayed as row and/or column headings.  Make sure you have only **one** cell or the entire table selected to ensure Excel auto-detects your data correctly.

**Windows:** Insert Tab>PivotTable

**Mac:** Go to Data Tab>PivotTable>Create Manual PivotTable...

**Adding data:** Click and drag to areas at the bottom of "PivotTable Fields". Remove by dragging back to list.

**Columns and Rows:** The _categories_ on the edges of the PivotTable
* Multiple categories on a  single axis will be nested

**Values:** The _numbers_ shown in the cells of the PivotTable (each cell summarizes one variable for the group defined by the combination of its column and row categories.)

![PivotTable example in Excel](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image9.png?raw=true)

In most cases, there will be **many** rows in your dataset represented by one cell in your PivotTable, so we need to summarize or aggregate the data. In the example above, there are many public or private universities in each state.

### Aggregation of Values
* Click on a field in the Values area and choose "Value Field Settings" to change the default aggregation
![Example of changing default aggregation in Excel](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image10.png?raw=true)
* "Summarize Values By" determines the mathematical function used to summarize the cells
	* Frequencies are available via the Count function. Note: this **will not count missing values.**
	* _Exercise_: Compare Frequency of "Control of Institution" using Count on "Control of Institution" and a Count on "Applicants Total".
		1. Drag "Control of Institutions" to Rows.
		2. Drag "Control of Institutions" to Values, and make sure it is summarized by "Count of"
		3. Drag "Applicants Total" to Values, and make sure it is summarized by "Count of"
* "Show Values As" allows more complex calculations based on other cells (e.g. percent of total)
* **Mac:** Click the "i" icon on the Value. "Show Values As" is located under the "Options>>" tab.

### Sorting and Filtering Columns and Rows
* Use the arrows at the right of "Row Labels" and "Column Labels"
![Example of how to sort in Excel](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image11.png?raw=true)
* "More Sort Options" provides advanced sorting by Values (_Mac: Not Available_)
	* Advanced filtering available in "Label Filters" and "Value Filters"

### Filters
* Dragging a field to the Filters area will create a drop-down filter at the top of the sheet.

## PivotTable Exercises
1. What are the "Enrolled Totals" in public and private schools (see "Control of Institutions")?
2. Which "Geographic Region" has the highest average "ACT Composite 75th Percentile Score"? How many regions have average scores below the national (Grand Total) average?
3. Which category of "Degree of Urbanization" contains the most public ("Control of Institution") universities?
	1. What percent of the "Applications Total" go to each of the top two "Degrees of Urbanization"? (Hint: Use the Show Values As tab in Values Field Settings)

## Next Steps:
### Other Useful Tools:
* Pivot Charts: Pivot Tables with added visualizations.
* Power Query (Windows-only): Loading and filtering large datasets
	* Data Tab > Get & Transform
* Data Validation: Control data entry to prevent errors
	* Data Tab > Data Validation
* Macros: Record and re-use processes, or write your own code

### Getting Help:
* [Lynda.com](http://software.sites.unc.edu/lynda/) provides training videos (free to UNC affiliates) on a wide variety of Excel functions
* [Data Carpentry - Spreadsheets](http://datacarpentry.org/spreadsheets-socialsci/)
* [Matt Jansen](http://guides.lib.unc.edu/mattjansen) ([guides.unc.edu/mattjansen](http://guides.lib.unc.edu/mattjansen)) of the Davis Library Research Hub is available for one-on-one consultations.

### Data Sources:
* [World Development Indicators](https://data.worldbank.org/products/wdi) (Excel_Workshop.xlsx)
* [IPEDS](https://nces.ed.gov/ipeds/use-the-data) (Pivot_Tables_IPEDS.xlsx), accessed [here](https://public.tableau.com/en-us/s/resources).

## SOLUTIONS
_Disclaimer: For many of these questions, there are multiple ways to get to the correct values. These are merely one way you could get the desired results._

### [Completed Companion Excel Workbook](https://github.com/UNC-Libraries-data/Excel/raw/master/Excel_Workshop_Completed.xlsx)

Companion Excel Workbook with all exercises completed with formulas and pasted values.

### Pivot Tables Exercises
1. What are the "Enrolled Totals" in public and private schools (see "Control of Institution")?
![Solution to PivotTable exercise](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image12.png?raw=true)
* Drag "Control of Institutions" to Row Labels to layout the table
* Drag "Enrolled Total" to Values
* Click "Enrolled Total" in Values and select Value Field Settings...
	* Change Summarize Values to _Sum_ instead of the default _Count_

2. Which "Geographic Region" has the highest average "ACT Composite 75th Percentile Score"? How many regions have average scores below the national (Grand Total) average?
![Solution to PivotTable exercise](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image13.png?raw=true)
* Drag "Geographic Region" to Row Labels
* Drag "ACT Composite 75th Percentile Score" to Values
* Click "ACT Composite 75th Percentile Score" to Values and select Value Field Settings...
	* Change Summarize Values by to _Average_.
* Sort the table by clicking the arrow icon in the corner of _Row Labels_ on the table itself (see arrow)
	* Click More Sort Options, then select Descending (Z to A) and set to "Average of ACT Composite 75th Percentile Score"

![Example of sorting a PivotTable](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image14.png?raw=true)

3. Which category of "Degree of Urbanization" contains the most public ("Control of Institution") universities?
![Solution to PivotTable exercise](https://github.com/UNC-Libraries-data/Excel/blob/master/media/image15.png?raw=true)
* Drag "Degree of Urbanization" to Row Labels. Drag "ID number" to Values.
* Click "ID Number" in Values, then Value Field Settings > Summarize Values by to set aggregation to _Count_.
	* Note: ANY variable that doesn't have missing values will work here. The _Count_ aggregation is essentially counting the number of filled cells in the given categories.  So some values will have slightly different counts due to empty cells.
* Drag "Control of Institution" to Report Filter. Use the Filter appearing at the top of the screen to select "Public".
* Use the Row Labels arrow, then More Sort Options to sort by "Count of ID Number"
	1. What percent of the "Applications Total" go to each fo the top two "Degrees of Urbanization"? (Hint: Use the Show Values As tab in Value Field Settings)
![Solution to PivotTable exercise 3](https://raw.githubusercontent.com/UNC-Libraries-data/Excel/master/media/image16.png)
	* Assume that we keep the Public filter active. Leave the earlier work in place.
	* Drag "Applicants Total" to Values and place it under "Count of ID number".
	* Click "Applicants Total" and select Value Field Settings
		* Under Summarize Values by, choose _sum_
		* Under Show Values As, choose _% of Column Total_

