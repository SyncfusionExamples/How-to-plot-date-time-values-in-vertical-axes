# How-to-plot-date-time-values-in-vertical-axes

This article explains how to plot date time values in vertical axis of Blazor chart.

**Plotting date time values in vertical axis**

To plot date-time value in y-axis, convert the date-time values to double while populating the items source for [Blazor chart](https://www.syncfusion.com/blazor-components/blazor-charts) and reverse the conversion(double to date-time) in the [OnAxisLabelRender](https://help.syncfusion.com/cr/blazor/Syncfusion.Blazor.Charts.AxisLabelRenderEventArgs.html) event.

By using Numeric axis with above conversion, you can plot date-time values in Y-axis.

The following code example illustrates this.

**C#**

```cshtml

@using Syncfusion.Blazor.Charts

<SfChart>
    <ChartPrimaryXAxis ValueType="Syncfusion.Blazor.Charts.ValueType.DateTime"></ChartPrimaryXAxis>
     <ChartEvents OnAxisLabelRender="@OnLabelRender"></ChartEvents>
   
    <ChartSeriesCollection>
        <ChartSeries DataSource="@WeatherReports" XName="XValue" YName="Y" Type="ChartSeriesType.Line">
        </ChartSeries>
    </ChartSeriesCollection>
</SfChart>

@code {

    DateTime start = new DateTime(1970, 1, 1);

    public class ChartData
    {

        public DateTime XValue { get; set; }
        public DateTime YValue { get; set; }
        public double Y
        {
            get{ return (YValue - new DateTime(1970, 1, 1)).TotalMilliseconds; }
        }
    }

    public List<ChartData> WeatherReports = new List<ChartData>
    {
        new ChartData { XValue = new DateTime(2010, 1, 1), YValue = new DateTime(2010, 1,  1) },
        new ChartData { XValue = new DateTime(2010, 2, 1), YValue = new DateTime(2010, 1,  2) },
        new ChartData { XValue = new DateTime(2010, 3, 1), YValue = new DateTime(2010, 1,  3) },
        new ChartData { XValue = new DateTime(2010, 4, 1), YValue = new DateTime(2010, 1,  4) },
        new ChartData { XValue = new DateTime(2010, 5, 1), YValue = new DateTime(2010, 1,  5) }
    };

    public void OnLabelRender(AxisLabelRenderEventArgs args)
    {
        if(args.Axis.Name == "PrimaryYAxis")
        {            
            double value = Convert.ToDouble(args.Text);
            //Converting corresponding double value to data time value.
            DateTime date = (new DateTime(1970, 1, 1).AddMilliseconds(value));
            args.Text = String.Format("{0:HH:mm}", date);
        }
    }

}

```

The following screenshot illustrate the output of the above code snippet.

**Output:**

![](/date-time-value-in-y-axis.png)

**Conclusion**

I hope you enjoyed learning how to plot date-time values in y-axis in Blazor Chart Component.

You can refer to our [Blazor Chart feature tour](https://www.syncfusion.com/blazor-components/blazor-charts) page to know about its other groundbreaking feature representations and [documentation](https://blazor.syncfusion.com/documentation/chart/getting-started), and how to quickly get started for configuration specifications. You can also explore our [Blazor Chart example](https://blazor.syncfusion.com/demos/chart/line?theme=bootstrap5) to understand how to create and manipulate data.

For current customers, you can check out our components from the [License and Downloads](https://www.syncfusion.com/sales/teamlicense) page. If you are new to Syncfusion, you can try our 30-day [free trial](https://www.syncfusion.com/downloads/blazor) to check out our other controls.

If you have any queries or require clarifications, please let us know in the comments section below. You can also contact us through our [support forums](https://www.syncfusion.com/forums), [support portal](https://support.syncfusion.com/create), or [feedback portal](https://www.syncfusion.com/feedback/blazor-components?control=charts). We are always happy to assist you!
