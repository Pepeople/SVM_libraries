# SVM_libraries
Running libsvm and Asynchronous parallel greedy coordinate descent (AGCD) 
We are following this procedure:

• Transform data to the format of an SVM package (if using datasets from libsvm site, skip this step.

• scale the data.

• Use the RBF kernel.

• Use cross-validation to find the best parameter C and γ.

• Use the best parameter C and γ to train the whole training set and record time it takes.

• Test and record accuracy.

The libsvm and AGCD both requires unix environment. For our experiment, we used cygwin on windows 10.

Instructions for libsvm:

1-	open cygwin and change directory to where your files of interest are.  Example: cd "C:/Users/F/Desktop/libsvm"

2-	simply run `make` 

3-	Running ./svm-train without any input data show you all different options related to training.

4-  For scaling traininng data, use following to scale from -1 to 1: ./svm-scale -l -1 -u 1 -s range1 svmguide1 > svmguide1.scale

The svm-scale tool, which performs feature scaling on the data. -l -1: This sets the lower limit for scaling to -1. -u 1: This sets the upper limit for scaling to 1. -s range1: This specifies the filename where the scaling parameters will be stored. The scaling parameters include the minimum and maximum values for each feature, which are needed to scale new data(test data). svmguide1: This is the filename of the input data file that will be scaled. svmguide1.scale: This redirects the output of the svm-scale command to a new file named svmguide1.scale. The scaled data will be stored in this file.

5-  For scaling tesing data, use following format: ./svm-scale -r range1 svmguide1.t > svmguide1.t.scale

6- For cross validation, change to the tools directory in libsvm file and include scaled datasets. This directory will include grid.py.

Run the following: python grid.py svmguide1.scale. Since RBF is selected by default, this will find optimal values for C and gamma. For more information about parameter selection using grid.by, check README in the same directory.

7-After grid.py, return to libsvm directory and run svm-train using optimal hyperparameters values: ./svm-train -c 2 -g 2 svmguide1.scale. For splice dataset: -c 8 -g 0.03125.

8-for predictions: ./svm-predict svmguide1.t.scale svmguide1.scale.model svmguide1.t.predict

Instructions for AGCD:

1- It uses the scaled datasets from libsvm and the optimal hyper-parameters values from grid.by.

2- The following runs the traininng and prediction at the same line using 20 cores: export OMP_NUM_THREADS=20; ./svm-train -c 2 -g 2 svmguide1 svmguide1.t



