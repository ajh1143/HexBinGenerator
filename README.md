# HexBinGenerator
Generates a HexBin plot with Inferno color styling, simply define the source file, x and y attributes, gridsize, and extents

## Example Output
<img src="https://github.com/ajh1143/HexBinGenerator/blob/master/InfernoPlot.png" class="inline"/><br>

## Imports

```Python3
import pandas as pd
import matplotlib.pyplot as plt
```

## Build DataFrame, Chunk, Iterate, Concat!

```Python3
def get_data(file):
    """
    :param file: file location/name
    :return df: dataframe of file
    """
    df = pd.read_csv(file, iterator=True, chunksize=100)
    df1 = pd.concat(df, ignore_index=True)
    return df
```

## Build HexBin Plot, Customize As Needed!

```Python3
def hexBinning(df, x, y, ext):
    """
    :param df: dataframe with target data
    :param x: name of x feature
    :param y: name of y feature
    :param ext: [xmin, xmax, ymin, ymax] from a list for hexbinning, similar to setting axes
    :return: generates a plot
    """
    #Build Hexbin
    # Define your gridsize(x,y) for each plot and add to parameters in plt.hexbin()
    plt.hexbin(df[x], df[y], cmap='inferno', extent=((ext[0], ext[1], ext[2], ext[3])))
    # Title, Axes
    plt.title('Hex Plot')
    plt.xlabel(str(x))
    plt.ylabel(str(y))
    # Add color bar 
    plt.colorbar()
    # Display 
    plt.show()
```

## Run It

```Python3
if __name__ == '__main__':
    #pass file location/name
    file1 = input("File")
    df = get_data((file1))
    x_col = input("X Column Name") 
    y_col = input("Y Column Name")
    x_min = input("X Min")
    x_max = input("X Max")
    y_min = input("Y Min")
    y_max = input("X Max")
    axes = [x_min, x_max, y_min, y_max]
    hexBinning(df,x_col, y_col, axes)
```
