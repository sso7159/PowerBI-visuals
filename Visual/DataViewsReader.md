#DataViews Reader
Learn how to extract targeted pieces of information from the DataView to build a logical data representation for your custom visual. 

##DataView
DataView is the structure that PowerBI provides to your visual and it contains the queried data to be visualized. DataView can be structured in different forms such as categorical and table DataView structures. PowerBI can also support the generation of multiple DataViews.

To get data into a usable format, you will create a 'visualTransform' function, which will access data in the DataView[] sent to your visual, and build a view model that your custom visual will use. 

This is where you will take advantage of the DataViewsReader!

```typescript
/**
 * Function that converts queried data into a view model that will be used by the visual
 * @param {VisualUpdateOptions} options - Contains references to size of container and the dataView which contains 
                                            all the data the visual had queried.
 * @param {IVisualHost} host            - Contains references to the host which contains services
 */
function visualTransform(options: VisualUpdateOptions, host: IVisualHost): ViewModel {
    /*Convert dataView to your viewModel*/
}
```

##DataView Usage With Different Structures

###Categorical Structures
The categorical structure is the most common DataView structure, and it is also the default structure set when you make a new PBI visual. For the first example, we'll look at how you would set up the 'visualTransform' for a fresh visual.

```typescript
function visualTransform(options: VisualUpdateOptions, host: IVisualHost): ViewModel {
    let ViewModel: ViewModel = { }  // This is the logical representation of how you want the data to be organized.
    
    let rootReader: IDataViewsReader = host.createIDataViewsReader(options.dataViews);
    let categoricalReader: IDataViewCategoricalReader = rootReader.getCategoricalReader();
    // Get all category and value columns
    let categoryColumn: ISafeCategoryColumn = categoricalReader.getCategoryColumn("category");
    let valueColumn: ISafeValueColumn = categoricalReader.getValueColumn("measure");

    for (let i = 0, len = categoryColumn.getValuesLength(); i < len; i++) {
        viewModel.push({
            // here you can get whatever information you want from each category or value column
            // categoryColumn.getDisplayName() ... categoryColumns.getValue(i) ... etc
            // also valueColumn.getValue(i)
        });
    }
}
```

###Table Structures
The table structure is the second most common DataView structure. It has columns which have metadata to correlate with the values in table rows. 

```typescript
function visualTransform(options: VisualUpdateOptions, host: IVisualHost): ViewModel {
    let ViewModel: ViewModel = { }  // This is the logical representation of how you want the data to be organized.
    
    let rootReader: IDataViewsReader = host.createIDataViewsReader(options.dataViews);
    let tableReader: IDataViewTableReader = rootReader.getTableReader();
    // Get all column metadata and value columns
    let metadataColumns: ISafeMetadataColumn[] = tableReader.getAllColumns();
    let tableRow: ISafeTableRow[] = tableReader.getAllTableRows();

    for (let i = 0, len = tableRow.getValuesLength(); i < len; i++) {
        viewModel.push({
            // here you can get whatever information you want from each metadata/table rows
        });
    }
}
```