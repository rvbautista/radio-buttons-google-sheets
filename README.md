# radio-buttons-google-sheets
Adopted from Ben Collins website with some modifications

A tutorial was originally written by Ben Collins with the script included in the page:

https://www.benlcollins.com/apps-script/radio-buttons-in-google-sheets/

The script is for cases where there are four choices along the same row, and these choices are stored in Columns B to E. It needs to be modified a bit to accommodate different cases. They will be highlighted below.


### Original code by Ben Collins

Below is the original code by Ben Collins. Credit him by referring to his tutorial( https://www.benlcollins.com/apps-script/radio-buttons-in-google-sheets/ ) 

```
/**
 * onEdit to uncheck checkboxes as required
 */
function onEdit(e) {
   
  // get event object data: sheet name, row number and column number
  const sheet = e.range.getSheet();
  const row = e.range.rowStart;
  const col = e.range.columnStart;
   
  switch(col) {
 
    // case when column B is checked
    case 2:
      sheet.getRange("C" + row + ":E" + row).uncheck();
      break;
 
    // case when column C is checked
    case 3:
      sheet.getRangeList(["B" + row,"D" + row + ":E" + row]).uncheck();
      break;
 
    // case when column D is checked
    case 4:
      sheet.getRangeList(["B" + row + ":C" + row,"E" + row]).uncheck();
      break;
     
    // case when column E is checked
    case 5:
      sheet.getRange("B" + row + ":D" + row).uncheck();
      break;
 
    // cell is outside of columns B to D
    default:
      return;
 
  }
}

```

### Three choices, located in Columns B to D

This is a modification of the original code I made:

```

/**
 * onEdit to uncheck checkboxes as required
 */
function onEdit(e) {
   
  // get event object data: sheet name, row number and column number
  const sheet = e.range.getSheet();
  const row = e.range.rowStart;
  const col = e.range.columnStart;
   
  switch(col) {
 
    // case when column B is checked
    case 2:
      sheet.getRange("C" + row + ":D" + row).uncheck();
      break;
 
    // case when column C is checked
    case 3:
      sheet.getRangeList(["B" + row , "D" + row]).uncheck();
      break;
 
    // case when column D is checked
    case 4:
      sheet.getRangeList(["B" + row + ":C" + row]).uncheck();
      break;
     
    // cell is outside of columns B to D
    default:
      return;
 
  }
}

```

### Explanation of the Script for Further Modification

When a checkbox is ticked, the script detects where the checkbox is, and then clears all the other specified checkboxes along the same row as the one ticked. To modify the script for the case where the columns of checkboxes are not located at Columns B to E, you need to change the following part of the code:

```

    // case when column C is checked
    case 3:
      sheet.getRangeList(["B" + row,"D" + row + ":E" + row]).uncheck();
      break;

```

The input inside sheet.getRangeList specifies the cells with checkboxes to untick. For the example above, it clears the checkboxes at the cell under Column B, Column D, and Column E along the same row as the one ticked. Change it to the cells under other columns if the checkboxes are located at the other columns. For example, if you place the checkboxes to Columns F to H and you want the script to clear the checkbox under Column F and H if the checkbox under Column G is ticked, then the code should be modified as:

```

    // case when column G is checked
    case 3:
      sheet.getRangeList(["F" + row,"H" + row]).uncheck();
      break;

```

This will clear the checkbox under columns F and H. 
