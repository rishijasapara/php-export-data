php-export-data by Eli Dickinson (http://github.com/elidickinson/php-export-data)
Released under the permissive MIT License: http://www.opensource.org/licenses/mit-license.php

A simple library for exporting tabular data to Excel-friendly XML, CSV, or TSV. It supports streaming exported data to a file or directly to the browser as a download so it is suitable for exporting large datasets (you won't run out of memory).

Excel XML code is based on Excel_XML by Oliver Schwarz (http://github.com/oliverschwarz/php-excel)

## What's New

1. You can create **Bold Rows** - helpful while creating the last row for total or creating a row that is to be highlighted
2. You can create **Header Rows** - these rows can be used to create column titles in blue background; you can also specify the numbers of cells to be merged to create a column header

## How to use it

    <?php

    // When executed in a browser, this script will prompt for download 
    // of 'test.xls' which can then be opened by Excel or OpenOffice.

    require 'php-export-data.class.php';

    // 'browser' tells the library to stream the data directly to the browser.
    // other options are 'file' or 'string'
    // 'test.xls' is the filename that the browser will use when attempting to 
    // save the download
    $exporter = new ExportDataExcel('browser', 'test.xls');

    $exporter->initialize(); // starts streaming data to web browser

	// this is the column title
	// addBlueBoldHeader(row data, merge column count);
	// merge column count is the total cells that will merged together
	// if you want to merge 4 columns, pass the count as 4
	$exporter->addBlueBoldHeader(array("Export Examples"), 3);
	
    // pass addRow() an array and it converts it to Excel XML format and sends 
    // it to the browser
    $exporter->addRow(array("This", "is", "a", "test")); 
    $exporter->addRow(array(1, 2, 3, "123-456-7890"));

    // doesn't care how many columns you give it
    $exporter->addRow(array("foo")); 

	// adding a bold row to highlight
	$exporter->addBoldRow(array("Total", "", "", "", "$100"));

	// writes the footer, flushes remaining data to browser.
    $exporter->finalize(); 

    exit(); // all done

    ?>


See the test/ directory for more examples.


Some other options for creating Excel files from PHP are listed here: http://stackoverflow.com/questions/3930975/alternative-for-php-excel/3931142#3931142