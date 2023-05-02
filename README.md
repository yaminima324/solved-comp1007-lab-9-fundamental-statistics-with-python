Download Link: https://assignmentchef.com/product/solved-comp1007-lab-9-fundamental-statistics-with-python
<br>
First, we summarize how to sort data in Python. Second, we learn how to use <strong>NumPy</strong> and

<strong>SciPy</strong> packages for basic statistics. Given a data set, we will:

<ul>

 <li>Find the mean, maximum, minimum, and standard deviation.</li>

 <li>Find the median and integer quartile range.</li>

 <li>Count the number of students in each score range.  Create charts to show the student distribution.</li>

</ul>




<h1>I.   Sorting Data</h1>

Case 1. If the data are stored in a list, we can use <strong>list.sort()</strong> function to sort the data.

L = [5, 2, 3, 1, 4] L.sort()

print(L) # [1, 2, 3, 4, 5]




Case 2. If the data are stored in a dictionary, we can first get the key‐values pairs through the <strong>dict.items()</strong> function, and then use the Python built‐in function <strong>sorted()</strong> to sort the key‐value pairs according to the key.

<table width="0">

 <tbody>

  <tr>

   <td width="521">d = {‘x’:3, ‘a’:89, ‘k’:5, ‘d’:10} L = sorted(d.items())print(L) # [(‘a’, 89), (‘d’, 10), (‘k’, 5), (‘x’, 3)]</td>

  </tr>

 </tbody>

</table>




Case 3. If the data are stored in a Numpy ndarray, we can use <strong>numpy.ndarray.sort()</strong> function to sort the ndarray in‐place.

import numpy as np

array = np.array([7, 5, 3, 2, 6, 1, 4]) array.sort()

print(array) # [1 2 3 4 5 6 7]




<h1>II.                 Counting Student Scores and Creating a Graph of Score Distributions with Median and Inter‐Quartile Range</h1>

<ol>

 <li>Import required library packages.</li>

</ol>




<table width="0">

 <tbody>

  <tr>

   <td width="521">import numpy as np from scipy import stats import pandas as pdfrom matplotlib import pyplot as plt</td>

  </tr>

 </tbody>

</table>




<ol start="2">

 <li>Download the data file <strong>csv</strong> from the course web page and save it in D drive.</li>

</ol>




<ol start="3">

 <li>Explore the <strong>csv</strong> file using Excel. We can see that the file has 3 columns – the index, student id, and scores. The index and ‘student id’ columns are not used for the statistics. We focus on the ‘scores’ column.</li>

</ol>




<ol start="4">

 <li>Load the file in Python. And, we store the values of the scores column in the <strong>NumPy’s</strong></li>

</ol>

df = pd.read_csv(‘quiz1_scores.csv’, index_col=’index’) scores = df[‘scores’].values

Remark: <strong>df</strong> is a <strong>DataFrame</strong>; <strong>df[‘scores’]</strong> is a <strong>Series</strong>, <strong>df[‘scores’].values</strong> is an <strong>ndarray</strong>.

<em> </em>

<ol start="5">

 <li>Finding the median.</li>

</ol>

Remark: <strong>Median</strong> is the value separating the higher half from the lower half of a data set.

median = np.median(scores)




<ol start="6">

 <li>Finding the q‐th percentile.</li>

</ol>

Remark: A <strong>percentile</strong> is a measure used in statistics indicating the value below which a given percentage of observations in a group of observations falls. For example, the 20th percentile is the value below which 20% of the observations may be found. Median is in fact the 50<sup>th</sup> percentile.

per75 = np.percentile(scores, 75) per25 = np.percentile(scores, 25)




<ol start="7">

 <li>Getting the <strong>Inter Quartile Range</strong> (IQR).</li>

</ol>

Remark: IQR is equal to the difference between 75th and 25th percentiles.

iqr = stats.iqr(scores)




<ol start="8">

 <li>Separate student scores into 10 groups evenly and count the number of scores in each group.</li>

</ol>




<ol>

 <li>Create labels for each group. We will use them as the <em>x</em> axis labels of the chart.</li>

</ol>

labels = [‘below 10′,

’10 to 19′,

’20 to 29′,

’30 to 39′,

’40 to 49′,

’50 to 59′,

’60 to 69′,

’70 to 79′,

’80 to 89′,

’90 or above’]




<ol>

 <li>There are 10 groups, but we need to create a sequence with total 11 numbers (0, 10, 20, …, 90, 100) that define the bin edges.</li>

</ol>

edges = np.linspace(0, 100, 11)

The <strong>linspace()</strong> function returns total 11 <strong>float</strong> numbers ‐ <em>0, 10, 20, 30, 40, 50, 60, 70, 80, 90</em>, and <em>100</em>.




You may also use the following statement to get the same values (but as integers).

edges = np.arange(0, 101, 10)




<ol>

 <li>Use <strong>NumPy’s histogram()</strong> function to tally scores into the appropriate interval and count the number of students in each interval.</li>

</ol>




Remark: A histogram is an accurate representation of the distribution of numerical data.  To construct a histogram, the first step is to “bin” (or “bucket”) the range of values, i.e., divide the entire range of values into a series of intervals, and then count how many values fall into each interval.




We have two methods to generate the histogram:

<ul>

 <li>specify the number of bins, then the range will be evenly divided into bins: hist, edges = np.histogram(scores, bins=10)</li>

</ul>




<ul>

 <li>specify the bin edges:</li>

</ul>

hist, edges = np.histogram(scores, bins=edges)

The <strong>histogram()</strong> function returns two ndarrays – <strong>hist</strong> stores the resulted data that is the count of each interval; <strong>bins</strong> stores the list of bin edges. Notice that the size of <strong>edges</strong> is one more than the size of <strong>hist</strong>.




The following is the counting result:

<table width="0">

 <tbody>

  <tr>

   <td width="134"><strong>Interval </strong></td>

   <td width="140"><strong>Count </strong></td>

  </tr>

  <tr>

   <td width="134">          below 10</td>

   <td width="140">3</td>

  </tr>

  <tr>

   <td width="134">10 to 19</td>

   <td width="140">2</td>

  </tr>

  <tr>

   <td width="134">20 to 29</td>

   <td width="140">15</td>

  </tr>

  <tr>

   <td width="134">30 to 39</td>

   <td width="140">26</td>

  </tr>

  <tr>

   <td width="134">40 to 49</td>

   <td width="140">51</td>

  </tr>

  <tr>

   <td width="134">50 to 59</td>

   <td width="140">42</td>

  </tr>

  <tr>

   <td width="134">60 to 69</td>

   <td width="140">39</td>

  </tr>

  <tr>

   <td width="134">70 to 79</td>

   <td width="140">23</td>

  </tr>

  <tr>

   <td width="134">80 to 89</td>

   <td width="140">11</td>

  </tr>

  <tr>

   <td width="134">90 or above</td>

   <td width="140">8</td>

  </tr>

 </tbody>

</table>




<ol start="9">

 <li>Print the histogram result.</li>

</ol>

print(‘Score Distribution’)

for i in range(len(hist)):

print(‘%s: t %d’ % (labels[i], hist[i]))




<ol start="10">

 <li>Plot a graph.

  <ol>

   <li>To plot a histogram with 10 bins, we need to find the center values for each bin:</li>

  </ol></li>

</ol>

bin_centers = 0.5 * (edges[1:] + edges[:‐1])

The statement above does the following thing:

<ul>

 <li><strong>edges[1:]</strong> is the subset of bins from 2<sup>nd</sup> element to last element.</li>

 <li><strong>edges[:‐1]</strong> is the subset of bins from 1<sup>st</sup> element to last second element.</li>

 <li>Add two <em>ndarrays</em></li>

 <li>Then, multiply the elements by 0.5.</li>

</ul>




<table width="0">

 <tbody>

  <tr>

   <td width="71"><strong>edges[1:] </strong></td>

   <td rowspan="6" width="36">+</td>

   <td width="82"><strong>edges[:‐1]</strong></td>

   <td rowspan="6" width="36">à</td>

   <td width="71"><strong>temp</strong></td>

   <td rowspan="6" width="53">x 0.5à</td>

   <td width="87"><strong>bin_centers</strong></td>

  </tr>

  <tr>

   <td width="71">10</td>

   <td width="82">0</td>

   <td width="71">10</td>

   <td width="87">5</td>

  </tr>

  <tr>

   <td width="71">20</td>

   <td width="82">10</td>

   <td width="71">30</td>

   <td width="87">15</td>

  </tr>

  <tr>

   <td width="71">30</td>

   <td width="82">20</td>

   <td width="71">50</td>

   <td width="87">25</td>

  </tr>

  <tr>

   <td width="71">…</td>

   <td width="82">…</td>

   <td width="71">…</td>

   <td width="87">…</td>

  </tr>

  <tr>

   <td width="71">90</td>

   <td width="82">100</td>

   <td width="71">190</td>

   <td width="87">95</td>

  </tr>

 </tbody>

</table>




<ol>

 <li>Plot the graph using the bin_centers and histogram result data, and add meaningful labels on X axis. To see the step‐by‐step visual effect, you need to type the “<strong>%matplotlib qt</strong>” command in the IPython console first.</li>

</ol>




plt.plot(bin_centers, hist)

plt.xticks(bin_centers, labels, rotation=’vertical’)










You can also choose the bar style for the histogram: plt.bar(bin_centers, hist, width=10)

plt.xticks(bin_centers, labels, rotation=’vertical’)







<ol>

 <li>Add an indicator of Inter Quartile range – Q1, Q2, and Q3</li>

</ol>

q1 = median ‐ iqr/2

<table width="0">

 <tbody>

  <tr>

   <td width="475">q2 = median q3 = median + iqr/2 plt.axvline(x=q1, color=’lightgrey’, linestyle=’‐‐’) plt.axvline(x=q2, color=’red’, linestyle=’:’) plt.axvline(x=q3, color=’lightgrey’, linestyle=’‐‐’)</td>

  </tr>

 </tbody>

</table>




The <strong>axvline()</strong> function draws a vertical line in the graph. We can customize the line with the parameters:

<ul>

 <li><em>x</em> : the position on the x axis.</li>

 <li><em>color</em> : name of the color</li>

 <li><em>linestyle</em> : the line style – solid (‐), dashed (‐‐), dotted (:)</li>

</ul>




<ol>

 <li>Add graph title and text labels.</li>

</ol>

plt.title(‘Score Distribution 1’, fontsize = 24)




plt.text(q1, 5, ‘Q1=%.2f’% q1, fontsize = 16) plt.text(q2, 10, ‘Median=%.2f’% q2, fontsize = 16) plt.text(q3, 15, ‘Q3=%.2f’% q3, fontsize = 16)










<h1>III.               Creating a Graph with Mean, Standard Deviation, Reference Standard Normal Distribution Curve</h1>

In this section, we are going to create another graph using the same data set. The graph shows the mean, standard deviation, and a reference curve.




You may add the example code of this section after the previous one. At the end, you will see two graphs. The second graph is created by the code of this section. Otherwise, you need to repeat the steps from 1 to 8 of the previous section first.




<ol start="11">

 <li>Finding the mean, maximum, minimum, and standard deviation.</li>

</ol>

s_mean = scores.mean() s_max = scores.max() s_min = scores.min() s_std = scores.std()

The functions include <strong>mean()</strong>, <strong>max()</strong>, <strong>min()</strong> and <strong>std()</strong> are the built‐in functions of <em>ndarray</em>.




<ol start="12">

 <li>Compute the density data using the Probability Density Function.

  <ol>

   <li>Use the <strong>pdf()</strong> function to compute the reference data.</li>

  </ol></li>

</ol>

pdf = stats.norm.pdf(range(100), s_mean, scale = s_std)

We provide a range (0 to 99, 100 elements), the peak (s_mean) and scale (standard deviation).




<ol>

 <li>Scale the resulted data up so as to match the histogram data scale.</li>

</ol>

Pdf = pdf / pdf.max() * hist.max()




<ol start="13">

 <li>Plot the graph using the bins and histogram result data. Then, change the x‐axis labels.</li>

</ol>




plt.plot(bin_centers, hist)

plt.xticks(bin_centers, labels, rotation=’vertical’)




<ol start="14">

 <li>Plot the density data as a reference curve.</li>

</ol>




plt.plot(Pdf, ‘‐‐’)













<ol start="15">

 <li>Add indicators for the mean and standard deviation.</li>

</ol>




<ol>

 <li>Add line and label for mean:</li>

</ol>

plt.axvline(x=mean, color=’green’) plt.text(mean, 10, <strong>‘$mu = %.2f$’ </strong>% mean)

The string <strong>‘$mu = %.2f$’</strong> is a formatted string for printing the string with special symbols. The <strong>mu</strong> in the string will be replaced by the <strong><em>μ</em> </strong>symbol but the string must be enclosed in quotation marks and dollar signs (<strong>‘$  $’</strong>).




<ol>

 <li>Add lines and labels for standard deviation:</li>

</ol>

for i in range(‐2,3):

if (i != 0):

x = mean + std * i

plt.axvline(x=x, color=’lightgrey’, linestyle=’:’)

plt.text(x, 0, ‘$ %d sigma$’ % i)










<ol start="16">

 <li>Draw the legend.</li>

</ol>

plt.legend([‘Score Counts’,’Reference’])

There are total 7 lines in the graph including the score counts (result of the histogram), reference (the result of pdf), mean, and the lines about the standard division. But, we don’t show all of them in the legend.




In the statement above, we pass a list with two strings that mean we want to show the first two lines with the labels stored in the list.




<h1>Exercise</h1>

Imagine that we have a survey data file retrieved from an online survey system. The columns contained in the survey data includes the responded date, customer IDs, salary range, age, number of children, gender and the choices of question 1 to 6. However, we only focus on the salary range.




Now, you need to create a graph to show the salary distribution with the median, IQR, and reference curve.




You need to:

<ul>

 <li>Separate the data in the 18 groups.</li>

</ul>




<ul>

 <li>Create a sequence (bins) with 19 numbers.</li>

</ul>




<ul>

 <li>The interval is 5,000</li>

</ul>




<ul>

 <li>Consider the follows labels for creating the histogram and plot the graph:</li>

</ul>




<table width="0">

 <tbody>

  <tr>

   <td width="119">Label</td>

   <td width="402">Description</td>

  </tr>

  <tr>

   <td width="119">Below 15K</td>

   <td width="402">The salary is less than $15,000</td>

  </tr>

  <tr>

   <td width="119">15K &lt;= $ &lt; 20K</td>

   <td width="402">The salary is larger than or equal to $20,000 but less than $15,000.</td>

  </tr>

  <tr>

   <td width="119">20K &lt;= $ &lt; 25K</td>

   <td width="402">The salary is larger than or equal to $25,000 but less than $20,000.</td>

  </tr>

  <tr>

   <td width="119">…</td>

   <td width="402">…</td>

  </tr>

  <tr>

   <td width="119">$95K or above</td>

   <td width="402">The salary is larger than or equal to $95,000</td>

  </tr>

 </tbody>

</table>




Assume that the minimum amount is $10,000, and the maximum amount is $100,000.




<ul>

 <li>Create a histogram using <strong>NumPy’s histogram()</strong> function with the salary data and bins.</li>

</ul>




<ul>

 <li>Compute density data using <strong>SciPy’s pdf()</strong></li>

</ul>




<ul>

 <li>Plot the graph using <strong>Matplotlib</strong>.</li>

</ul>
















The sample output of the graph: