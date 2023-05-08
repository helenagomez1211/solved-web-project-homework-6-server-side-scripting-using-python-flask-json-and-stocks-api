Download Link: https://assignmentchef.com/product/solved-web-project-homework-6-server-side-scripting-using-python-flask-json-and-stocks-api
<br>
<h1>1. Objectives</h1>

<ul>

 <li>Get experience with Python programming language and Flask framework.</li>

 <li>Get experience creating web pages using HTML, CSS, JavaScript, DOM, JSON format and XMLHttpRequest object.</li>

 <li>Get experience with Tiingo Stocks API and <u>org</u>’s News API ● Getting hands-on experience in GCP, AWS or Azure.</li>

</ul>

<h2>1.1 Cloud Exercise</h2>

<ul>

 <li>The backend of this homework must be implemented in the cloud on GCP, AWS or Azure using Python.</li>

 <li>See homework 5 for installation of either one of these platforms. You only have to select one platform to implement your backend.</li>

 <li>See the hints in section 3; a lot of reference material is provided to you.</li>

 <li>For Python and Flask kick-start, please refer to the Lecture slides on the class website.</li>

 <li>You must refer to the grading guidelines, the video, the specs and Piazza. Styling will be graded and the point’s breakup is mentioned in the grading guidelines.</li>

 <li>The link for the video is – <u>https://youtu.be/1vOis6BxYq4</u></li>

</ul>

<h1>2. Description</h1>

In this exercise, you are asked to create a webpage that allows you to search for stock information using the <em><u>Tiingo</u> Stock API</em>, and the results will be displayed in both tabular format and charts format using <u>HighCharts</u>. You will also provide news articles for the selected stock using the News API.

<h2>2.1. Description of the Search Form</h2>

The user first opens a web page as shown below in <strong>Figure 1</strong>, the initial search page, where he/she can enter a stock ticker symbol. Providing a value for the “Stock Ticker Symbol” field is mandatory.




<h3>Figure 1: Initial search page</h3>

The search form has two buttons:

<ol>

 <li><strong>Search button: </strong></li>

</ol>

Once the user has provided valid data (a stock ticker is required), and clicked on the <strong>Search</strong> button, your front-end JavaScript script will make a request to your web server providing it with the form data that was entered (the ticker symbol). You must use GET to transfer the form data to your web server (do not use POST, as you would be unable to provide a sample link to your cloud services). A Python script using Flask will retrieve the data and send it to the Tiingo Stocks API. You need to use the <em>Flask</em> Python framework to make all the API calls.




<strong>Using XMLHttpRequest or any other JavaScript calls for anything other than calling your own “cloud” backend will lead to a 4-point penalty</strong>.  <strong><u>Do not call the Tiingo Stocks API</u> <u>directly from JavaScript.</u> </strong>

Define routing endpoints and make your API call from the Python backend. The recommended tutorial for <em>Flask</em> and more importantly, routing, can be found at the following link: <u>https://flask.palletsprojects.com/en/1.1.x/</u>




If the user clicks on the <strong>Search</strong> button without providing a value in the field, an alert should pop up “Please fill out this field” (an example is shown in <strong>Figure 2</strong>).




<h3>Figure 2: An Example of Empty Input alert</h3>

<ol start="2">

 <li><strong>Clear button: </strong></li>

</ol>

This button must clear the result area (below the search area) and the text field (stock ticker symbol).

<h2>2.2 Displaying Results</h2>

In this section, we outline how to use the form data to construct the calls to the RESTful web services of the <em>Tiingo APIs</em>, <em>News API</em> and display the results in the web page. There are basically<strong> four</strong> components to display in a “tabs” from on the web page: <strong>Company Outlook</strong>, <strong>Stock Summary</strong>, <strong>Charts</strong> and <strong>Latest News</strong>.

A sample result is shown in <strong>Figure 3</strong>.




<strong>Figure 3: A Sample Search Result for Apple Inc (AAPL) </strong>

<h3>2.2.1 Displaying Company Outlook Tab</h3>

We use the <strong><em>Tiingo “Meta Endpoint” API</em></strong>. Please refer to <u>https://api.tiingo.com/documentation/end-of-day</u>  for more details on the API.

<h4>API Sample: <em><u>https://api.tiingo.com/tiingo/daily/keyword?token=API_KEY</u></em></h4>

The process to create your API key is explained in section 3. When constructing the python request required obtaining the Company Details, you need to provide two values in the URL:

<ol>

 <li>The first value, the <strong>keyword</strong>, is the <strong>stock ticker</strong> the user entered in the form.</li>

 <li>The second value, the <strong>token</strong> is your <strong>API_KEY </strong>that you create as described in section 3. For example, to get information about AAPL, the stock ticker or Apple, you would call the API as: <u>https://api.tiingo.com/tiingo/daily/aapl?token=0108ecd7f84bf97f8f11998a4e4561bx51da92c8</u></li>

</ol>

The <strong>response</strong> of this Python request is a <strong>JSON-formatted object</strong>. <strong>Figure 4</strong> shows a sample response from the request. You need to parse this JSON object and extract some fields as required. The mapping of the JSON response to the tabular data to be displayed on the screen is shown in <strong>Table 1</strong>.

<strong> </strong>




<h4>Figure 4: Sample JSON response from Tiingo API’s metadata endpoint</h4>

<strong> </strong>




<table width="606">

 <tbody>

  <tr>

   <td width="216"><strong>Tabular Data</strong></td>

   <td width="390"><strong>Data from Tiingo Metadata API response JSON</strong></td>

  </tr>

  <tr>

   <td width="216">Company Name</td>

   <td width="390">The value of key <em>“name”</em></td>

  </tr>

  <tr>

   <td width="216">Stock Ticker Symbol</td>

   <td width="390">The value of key <em>“ticker”</em></td>

  </tr>

  <tr>

   <td width="216">Stock Exchange Code</td>

   <td width="390">The value of key <em>“exchangeCode”</em></td>

  </tr>

  <tr>

   <td width="216">Company Start Date</td>

   <td width="390">The value of key <em>“startDate”</em></td>

  </tr>

  <tr>

   <td width="216">Description</td>

   <td width="390">The value of key <em>“description”. </em>The description needs to be truncated with an ellipsis (“triple dots”) so as to only span the first <strong>FIVE</strong> lines.</td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<h4>Table 1: Mapping JSON data and company outlook display</h4>

<strong> </strong>

After extracting the data, the data should be displayed in a tabular format. A sample output is shown in <strong>Figure 5</strong>.

<strong> </strong>

<strong>Figure 5: Example of Company Outlook Tab </strong>

<strong> </strong>

<h3>2.2.2 Displaying Stock Summary Tab</h3>

We use the <strong><em>Tiingo “Current Top-of-Book &amp; Last Price” API </em></strong>to fetch the stock information for the ticker. Please refer to <u>https://api.tiingo.com/documentation/iex</u> for more details on the API.

<h4>API Sample: <em><u>https://api.tiingo.com/iex/keyword?token=API_KEY</u></em><em>  </em></h4>

When constructing the python request required obtaining the Company Details, you need to provide two values in the URL:

<ol>

 <li>The first value, the <strong>keyword</strong>, is the <strong>stock ticker</strong> the user entered in the form.</li>

 <li>The second value, the <strong>token</strong> is your <strong>API_KEY </strong>that you create as described in section 3.</li>

</ol>

For example, to get information about AAPL, the stock ticker or Apple, you would call the API as:

<u>https://api.tiingo.com/iex/aapl?token=0108ecd7f84bf97f8f11998a4e4545ea51da92c8</u>

The <strong>response</strong> of this Python request is a <strong>JSON-formatted object</strong>. <strong>Figure 6</strong> shows a sample response from the request. You need to parse this JSON object and extract some fields as required. The mapping of the JSON response to the tabular data to be displayed on the screen is shown in <strong>Table 2</strong>.










<h4>Figure 6: Sample JSON response from Tiingo API’s Current Top-of-Book &amp; Last Price endpoint</h4>




<table width="654">

 <tbody>

  <tr>

   <td width="192"><strong>Tabular Data</strong></td>

   <td width="462"><strong>Data from Tiingo Current Top-of-Book &amp; Last Price </strong><strong>API response JSON</strong></td>

  </tr>

  <tr>

   <td width="192">Stock Ticker Symbol</td>

   <td width="462">The value of key <em>“ticker”</em></td>

  </tr>

  <tr>

   <td width="192">Trading Day</td>

   <td width="462">The value of the key <em>“timestamp”. Truncate the value to just display the date.</em></td>

  </tr>

  <tr>

   <td width="192">Previous Closing Price</td>

   <td width="462">The value of key <em>“prevClose”</em></td>

  </tr>

  <tr>

   <td width="192">Opening Price</td>

   <td width="462">The value of key <em>“open”</em></td>

  </tr>

  <tr>

   <td width="192">High Price</td>

   <td width="462">The value of key <em>“high”</em></td>

  </tr>

  <tr>

   <td width="192">Low Price</td>

   <td width="462">The value of key <em>“low”</em></td>

  </tr>

  <tr>

   <td width="192">Last Price</td>

   <td width="462">The value of key <em>“last”</em></td>

  </tr>

  <tr>

   <td width="192">Change</td>

   <td width="462">Difference between the value of key <em>“last” </em>and<em> “prevClose”.  </em>Also display the upward arrow or downward arrow depending on whether the difference value is positive or negative. Reference to the image links in Section 3.<strong> Change = (last – prevClose) </strong></td>

  </tr>

  <tr>

   <td width="192">Change Percent</td>

   <td width="462">The Change Percent between the value of key <em>“last” and “prevClose”.</em>Also display the upward arrow or downward arrow depending on whether the difference value is positive or negative. Reference to the image in Section 3. <strong>Change Percent = (Change / prevClose) * 100 </strong>Please refer to below link for formula:<u>https://www.skillsyouneed.com/num/percent-change.html</u></td>

  </tr>

  <tr>

   <td width="192">Number of Shares Traded</td>

   <td width="462">The value of key <em>“volume”</em></td>

  </tr>

 </tbody>

</table>

<h4>Table 2: Mapping JSON data and stock summary display</h4>

<strong> </strong>

After extracting the data, the data should be displayed in a tabular format. A sample output is shown in <strong>Figure 7</strong>.




<strong>Figure 7: Example of Stock Summary Information Tab </strong>

<strong> </strong>

<h3>2.2.3 Displaying Stock Price/Volume Chart Tab</h3>

You should extract the content of Time Series Data from the returned JSON object to construct a chart which is responsible for displaying (close) price/volume. The chart is provided by <strong>HighCharts. </strong>Find more information about HighCharts at: <u>https://www.highcharts.com/demo</u>

The historical data for the ticker can be obtained from <strong><em>Tiingo’s “Historical Intraday Prices Endpoint” API</em></strong>.

Please refer to <u>https://api.tiingo.com/documentation/iex</u> for more details on the API.

API Sample:

<h4><em><u>https://api.tiingo.com/iex/keyword/prices?startDate=prior_date&amp;resampleFreq=12hour&amp;columns=o pen,high,low,close,volume&amp;token=API_KEY</u></em><em>  </em></h4>

When constructing the python request required obtaining the Company Details, you need to provide 5 values:

<ol>

 <li>The first value, the <strong>keyword</strong>, is the <strong>stock ticker</strong> the user entered in the form.</li>

 <li>The second value, the <strong>token</strong> is your <strong>API_KEY </strong>that you create as described in section 3.</li>

 <li>The third value is the <strong>startDate</strong>, a prior date which should be 6 months prior to the current date. You can use Python DateUtils’s “relativedelta” to calculate the date. Please refer to <u>https://dateutil.readthedocs.io/en/stable/relativedelta.html</u> for more details.</li>

 <li>The fourth value, <strong>columns</strong>, indicates what you want returned: open, high, low and close prices and volume.</li>

 <li>The fifth value, <strong>resampleFreq</strong>, indicates in hours the resampling frequency. See the Tiingo documentation for allowed values.</li>

</ol>

For example, to get information about AAPL Historical Intraday Prices, you would call the API as: <u>https://api.tiingo.com/iex/aapl/prices?startDate=2020-03-</u>

<u>04&amp;resampleFreq=12hour&amp;columns=open,high,low,close,volume&amp;token=0108ecd7f84bf97f8f1199</u>

<u>8a4e4561ea51da92c8</u>




The <strong>response</strong> of this Python request is a <strong>JSON-formatted object</strong>. <strong>Figure 8 </strong>shows a sample response from the request. You need to parse this JSON object and extract some fields as required.







<h4>Figure 8: Sample JSON response from Tiingo API’s Historical Intraday Prices Endpoint</h4>

<strong> </strong>

<strong> </strong>

The data obtained from the API can then be mapped to the <strong>HighCharts</strong> dataset using the mapping below.




<table width="630">

 <tbody>

  <tr>

   <td width="216"><strong>Chart Data</strong></td>

   <td width="414"><strong>Data from Tiingo Historical Intraday Prices API response </strong><strong>JSON</strong></td>

  </tr>

  <tr>

   <td width="216">Date</td>

   <td width="414">The value of key <em>“name”</em></td>

  </tr>

  <tr>

   <td width="216">Stock Price</td>

   <td width="414">The value of key <em>“close”</em></td>

  </tr>

  <tr>

   <td width="216">Volume</td>

   <td width="414">The value of key <em>“volume”</em></td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<h4>Table 3: Mapping JSON data and HighCharts data</h4>

<strong> </strong>

For mapping the Stock price data to data for HighCharts, create an array of data points (x1, y1)  where x1 will be the date(in UTC format) and y1 will be the corresponding close stock price for that day. This array will then act as an input dataset for your HighCharts. Please refer to links in <strong>Section 3</strong> for more details.




Similarly create another array of points (x2, y2) where x2 will be the date (also in UTC format) and y1 will be the volume for that day. This array will be the second input for your HighCharts. Since you will be plotting Stock Price vs Date and Volume vs Date you will have two different datasets and two yaxis and a single x-axis.

<strong> </strong>

Initially, the chart shows the historical stock price (in blue line with filling the area below, two digits after decimal) and volume (in grey bar) for the <strong>past six months</strong> by an interval of<strong> one day</strong>. <strong>Figure 9</strong> shows an example of the Stock Price/Volume chart.







<h4>Figure 9: An Example of Chart showing Stock Price/Volume for 6 months</h4>

The title of the chart for showing price/volume is “<strong>Stock Price &lt;Ticker&gt; (YYYY-MM-DD)</strong>”, where “YYYY-MM-DD” is today’s date. The subtitle of the chart should be “Source: Tiingo” and should hyperlink to the Tiingo website: <u>https://api.tiingo.com/.</u> The title of the Y-axis is “<strong>Stock Price</strong>” when showing the stock price and the other Y-axis is “<strong>Volume</strong>”.




The X-axis changes on the basis of the zoom level 6 months, 3 months, 1 month, 15 days, and 7 days. Please refer to <strong>Section 3</strong> for references on how to change the chart data on the basis of the zoom level<strong>. Figure 10</strong> shows an example of the Stock Price/Volume chart for 15 days zoom level.







<strong>Figure 10: An Example of Chart showing Stock Price/Volume for 15 days</strong>

<strong> </strong>

<h3>2.2.4 Displaying Stock News Tab</h3>

To display news for the company, we should use the stock ticker symbol from the form data to construct a Python request to the <strong><em>News API</em></strong> and display the results in your page. Please refer to <u>https://newsapi.org/docs</u> for more details.

<h4>API Sample: <em><u>https://newsapi.org/v2/everything?apiKey=API_KEY&amp;q=keyword</u></em><em>  </em></h4>

When constructing the python request required obtaining the News articles, you need to provide two values:

<ol>

 <li>The first value is your <strong>apiKey</strong>, which you created as described in section 3.</li>

 <li>The second value, <strong>q</strong>, is the stock ticker the user entered in the form.</li>

</ol>

The <strong>response</strong> of this Python request is a <strong>JSON-formatted object</strong>. <strong>Figure 11 </strong>shows a sample response from the request. You need to parse this JSON object and extract some fields as required. Only the articles that have <em>title, url, urlToImage </em>and<em> publishedAt</em> keys present with a non-empty value should be displayed. If any attribute is missing, empty or blank, do not display it in the results. Display the <strong>first five</strong> articles from the response which have all the keys and values present as mentioned.




<h4>Figure 11: Sample JSON response from News API’s Endpoint</h4>

<strong> </strong>

The mapping between the information populated in the results and the JSON object is shown in <strong>Table 4</strong>.




<table width="631">

 <tbody>

  <tr>

   <td width="181"><strong>Card Data</strong></td>

   <td width="450"><strong>Data from News API JSON response</strong></td>

  </tr>

  <tr>

   <td width="181">Image</td>

   <td width="450">The value of key <em>“urlToImage”</em></td>

  </tr>

  <tr>

   <td width="181">Title</td>

   <td width="450">The value of key <em>“title”</em></td>

  </tr>

  <tr>

   <td width="181">Date</td>

   <td width="450">The value of key <em>“publishedAt”</em></td>

  </tr>

  <tr>

   <td width="181">Link to Original Post</td>

   <td width="450">The value of key <em>“url”</em></td>

  </tr>

 </tbody>

</table>

<h4>Table 4: Mapping between result card and JSON object</h4>

After extracting the data, it should be displayed as shown in <strong>Figure 12</strong>.  The <strong>“See Original Post” </strong>hyperlink opens the original post in a new tab in the browser.

<strong> </strong>

<strong>Figure 12: Example of Latest News </strong>

<h3>2.2.5 Displaying Error Message</h3>

If the Tiingo API service returns an Invalid Call error message, the page should display “<em>Error : No record has been found, please enter a valid symbol.</em>” <strong>Figure 13</strong> shows an example when searching for non-existent stock symbol “<em>xyz</em>”.




<strong>Figure 13: Search Result when there is no matching result </strong>

<h2>2.3 Saving Previous Inputs</h2>

In addition to displaying the results, the page should maintain the entered value while displaying the current result. For example, if a user searches for “<em>AAPL</em>”, the user should see what was provided in the search form when displaying the results. Specifically, when clicking on the <strong>Search</strong> button, the page should display the result retrieved from the <em>Tiingo API</em> service and keep the value provided in the search form.

<strong> </strong>

<strong> </strong>

<strong> </strong>

<h1>3. Hints</h1>

<h2>3.1 Tiingo API Documentation</h2>

To apply for an API key on Tiingo and read the API documentation, please go to:  <u>https://api.tiingo.com/</u>.

Click on the <strong>Sign-up</strong> button. Enter your<strong> Username</strong>, your @usc.edu <strong>E-mail</strong> address, select and confirm a <strong>Password</strong>, and click on <strong>Sign-up</strong>. Verify your account and go to  <u>https://api.tiingo.com/account/api/token</u>  to get your API_KEY.

<h2>3.2 Image References</h2>

Regarding the marker icon rendered beside the values of <em>Change</em>, <em>Change Percent</em>, a red-down arrow icon is displayed if the value is negative while a green-up arrow icon is displayed if the value is positive. The icons can be found at:

<u>https://csci571.com/hw/hw6/images/GreenArrowUp.jpg</u>  <u>https://csci571.com/hw/hw6/images/RedArrowDown.jpg</u>

<h2>3.3 Deploy Python file to the cloud (GAE/AWS/Azure)</h2>




You should use the domain name of the GAE/AWS/Azure service you created in HW #5 to make the request. For example, if your GAE/AWS/Azure server domain is called <strong>example.appspot.com</strong> or <strong>example.elasticbeanstalk.com</strong> or <strong>example.azurewebsites.net</strong>, the following links will be generated:




GAE – http://example.appspot.com/index.html

AWS – http://example.elasticbeanstalk.com/index.html

Azure – http://example.azurewebsites.net/index.html




The <em>example</em> subdomain in the above URLs will be replaced by your choice of subdomain from the cloud service. You may also use a different page than index.html.

<h2>3.4 How to get News API Key</h2>

To apply for an API Key for newsapi.org, go to <u>https://newsapi.org/docs</u>.




Click on the “<strong>Get</strong> <strong>API key</strong>” button. You should fill out the form as shown in <strong>Figure 14</strong>. Click <strong>Submit</strong>.

The API Key (News API key) will be displayed. Copy this key as you will use it in all the <em>News API</em> calls.




<h2>Figure 14: Google News Register for API Key Form</h2>




<h3>3.5 References for HighCharts</h3>

<strong> </strong>

<ol>

 <li><u>https://api.highcharts.com/highstock/</u></li>

 <li><u>https://www.highcharts.com/demo/stock/intraday-area</u></li>

 <li><u>https://www.highcharts.com/demo/stock/compare</u></li>

</ol>


