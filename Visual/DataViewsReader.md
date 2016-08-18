#DataViews Reader
Learn how to extract targeted pieces of information from the DataView, to build a logical data representation for your custom visual.

##DataView
DataView is the structure that PowerBI provides to your visual and it contains the queried data to be visualized. DataView can be structured in different forms such as categorical and table DataView structures. PowerBI can also support the generation of multiple DataViews.

To get data into a usable format, you will create a 'visualTransform' function, which will access data in the DataView[] sent to your visual, and build a view model that your custom visual will use. 

```typescript
/**
 * Function that converts queried data into a view model that will be used by the visual
 *
 * @function
 * @param {VisualUpdateOptions} options - Contains references to the size of the container
 *                                        and the dataView which contains all the data
 *                                        the visual had queried.
 * @param {IVisualHost} host            - Contains references to the host which contains services
 */
function visualTransform(options: VisualUpdateOptions, host: IVisualHost): BarChartViewModel {
    /*Convert dataView to your viewModel*/
}
```

##DataView Structures

###Categorical
The categorical structure is the most common DataView structure. 