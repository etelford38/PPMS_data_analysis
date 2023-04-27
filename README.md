# PPMS_data_analysis
Python code for loading, analyzing, and saving data generated by a PPMS instrument.
Written by Evan Telford (ejt2133@columbia.edu) and Christie Koay (csk2172@columbia.edu)


Running the program:

You will need to install a series of Python packages and a compiler (Spyder) to run the code.
1.	Install Python. 

Mac: https://www.python.org/downloads/macos/

Windows: https://www.python.org/downloads/windows/

2.	Install Anaconda (a Python environment manager which makes installing software more easily).

Mac: https://docs.anaconda.com/anaconda/install/mac-os/

Windows: https://docs.anaconda.com/anaconda/install/windows/#

3.	Create your own environment to install the relevant packages. 

Open the Python terminal. On Mac, this is simply opening the terminal. On Windows, this is opening the “Anaconda Prompt”. Type: “conda create --name <insert desired environment name>”. This creates a new environment with your desired name. The name is arbitrary. Type: “conda activate <name of your environment>”. This activates your environment. The name should be the same as the one you used in Step 3b. Any lines of code run after this will be run in your chosen environment. If you want to deactivate the environment and return to the default environment (called “root”), simply type “conda deactivate”. 

For more details on creating environments:
(https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

4.	Install Spyder. 
	
Spyder is an integrated development environment (IDE) program where you can write, compile, and run python code. Type: “conda install spyder”. Check your installation by running Spyder. Do this by typing “Spyder” into the terminal. It should open Spyder.
  
5.	Install a series of additional Python packages required to run the software.

	Pandas (https://anaconda.org/anaconda/pandas).
	Numpy (https://anaconda.org/anaconda/numpy).
	Scipy (https://anaconda.org/anaconda/scipy).
	Matplotlib (https://anaconda.org/conda-forge/matplotlib).
	Pyqt5 (https://anaconda.org/anaconda/pyqt)
  
6.	Load the python script that launches the data analysis GUI.

Run Spyder by typing “spyder” in the terminal within your desired environment. Within Spyder, open the data analysis program named “QD_data_analysis_v2.py”. Click the run button (shaped like a “play” button). The GUI should automatically launch.

Note: if you run into issues in installing any of the above packages, try updating anaconda. 
1.	In the “root” environment, type “conda update conda”.
2.	Type “conda update --all”.
3.	Activate your environment.
4.	Type “conda update --all”.
5.	Try reinstalling the package.

List of GUI functions:
	
1.	Load PPMS Data: 
Load Data: Opens Finder to select data file.

2.	Available data:
x-axis and y-axis: Drop down menus containing titles of all the data columns. You can select which data you want to plot on the x and y axes.

3.	Plot or Print Data:
a.	Print Data: This will display the data that you have selected in the drop down menu under x-axis and y-axis in “Available Data” in the Spyder console.
b.	Plot Data: Plots selected data from “Available Data” on graph.

4.	Clear Graph: 
Clear: Clears ALL traces from the plot.

5.	Create New Data Columns: This tool enables you to do calculations/conversions with data from the existing data columns. Use the drop down menus “Variable (x)” and “Variable 2 (y)” to select x and/or y variable(s). You can then define an equation for your calculation in “Analysis Code” using Python syntax and define a new name for the new data column under “New Variable Name.” Hitting “Create Column” will create a new data column that reflects your calculation. This new column should be visible in the x-axis and y-axis drop down menus under “Available Data”.

Note: To call pandas, numpy, or scipy packages use “pan”, “np”, or “sc”, respectively.

6.	Fitting Plot Data:
a.	Lower Limit / Upper Limit: Define the x-axes bounds that you want to fit. If you leave these blank, it will default to the min/max of your x-axis data for the lower/upper limit, respectively.
b.	Polynomial Fit Order: The polynomial order you want to fit your data to. If you leave this blank, it will default to 1.
c.	Fit Data: Replots the data onto the graph and plots the fit as a dashed line. Coefficients for the polynomial fit are displayed in the legend.

7.	Modify Data:
a.	Smooth Data Binning Window: Applies a Savitzky-Golay filter to your data. This smooths data by fitting a polynomial to small subsets of data points, which can help with noisy data sets. However, you will lose some resolution. 
b.  Binning window: The number of points in each subset over which you want to fit. This must be an odd number greater than 1.
c.	Smooth Data: This will apply the filter. Checking the “Save?” box will save the smoothed data as a new data column.
	
8.	Hall Analysis: 
a.	Symmetrize: typically used for magnetoresistance data where y = magnetoresistance and x = magnetic field. It performs the following calculation:
 y_symm  =  (f(+x) + f(-x))/2 		
b.	Anti-symmetrize: typically used for Hall measurements where y = Hall resistance and x = magnetic field. It performs the following calculation:
 y_antisymm  =  (f(+x) - f(-x))/2

9.	Save Data: 
Save Data: Opens a file dialog to save the modified dataset (including newly generated columns) as a text file (.txt) with the user defined name.
Note: To save the plot as an image file, use the save button on the toolbar above the graph.

10.	Additional functions:
a.	Making plots with multiple traces or creating new plots: The folder icon adds traces to the same plot, or create a new plot.
b.	Rename Tabs: Double clicking the tab title will open a new window that will allow you to enter a new name for the tab.
  
Data-file constraints:
	
A brief description of the subfunction which loads the data is as follows:
1.	Opens the selected file.
2.	Searches the file for a “[Data]” keyword.
3.	Reads the file start from the line after the one containing “[Data]”. Reading is done assuming comma-demilimited text.
4.	The first line after the one containing “[Data]” is set to be the header.
5.	The remaining lines are saved as a data frame.

The python program can therefore load any data file that is formatted in the following way:
●	Line X: [Data]
●	Line X+1: Comma-delimited names of data columns.
●	Line X+2 → end of file: Comma-delimited data in string format.

Note: Any lines before Line X do not matter. Can contain any information in any format. The python code will automatically skip them.
Second Note: files generated by MultiVu are saved in the appropriate format. If your file is in a different format, you’ll need to convert it using a third-party program.
