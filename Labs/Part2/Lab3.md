# Lab 3: Watson Studio Assembling a Dashboard
In this lab we will cover several data visualization capabilities provided by **IBM Watson Studio**:

* The **IBM Watson Studio Dashboards** service, with a UI-driven capability to build and publish dashboards largely inspired by **IBM Cognos Analytics** capabilities.

## Watson Studio Cognos Dashboard Embedded
**IBM Watson Studio** has a built-in capability to build interactive, publishable dashboard.

### Setting up a dashboard
1. Back to your project's Assets list, select the `[(+) Add to project]` button ![](Lab2-Visualization/20190717_b56ce3a3.png)
1. Select the `Dashboard` button ![](Lab2-Visualization/20190717_c23e6094.png) to create a new dashboard
1. Enter a name, e.g. `NYC Bike Rentals`
1. We will need to create a dashboard service instance, select the `Associate a Cognos Dashboard Embedded service instance` link ![](Lab2-Visualization/markdown-img-paste-20180513232835944.png)
1. Choose the 'Lite' configuration, and confirm default org and space
1. Click the `Reload` link and select the instance, then the `Save` button: ![](Lab2-Visualization/markdown-img-paste-2018051422030148.png)
1. In the `Select a template`, use `Tabbed` and `Freeform`: ![](Lab2-Visualization/markdown-img-paste-20180513233249777.png), then `[OK]` button.

### Adding data to a dashboard
We will now use the data produced by Data Refinery for the NYC bike share dataset.
1. Switch to the `Select` tab and expand `Selected sources` ![](Lab2-Visualization/markdown-img-paste-20180513233447821.png)
1. Select the `201701-citibike-tripdata_cleansed.csv` file: ![](Lab2-Visualization/markdown-img-paste-2018051323355497.png)
1. The dashboarding has the ability to propose a graph type based on the data. We will start by displaying the `Trip Duration` by `Age`:
    1. Drag&Drop the `Trip_Duration` from the data panel on the left to the dashboard canvas on the right; ![](Lab2-Visualization/markdown-img-paste-2018051323454084.png) The `Trip_Duration` total aggregated sum is displayed as a big number:  
     ![](Lab2-Visualization/markdown-img-paste-20180513234653132.png)
    1. Drop the `Age` field onto the `Trip_Duration` widget: ![](Lab2-Visualization/markdown-img-paste-20180513234943347.png)
    1. **IBM Watson Studio** changes the graph to a more suitable representation, in this case a bar graph: ![](Lab2-Visualization/20180925_ae2fad33.png)
    1. Unfortunately, our data has not been cleansed enough and we have erroneous values for `Age`. Right-click on the `Age` label to display the menu, and select the filter icon ![](Lab2-Visualization/markdown-img-paste-20180513235455667.png)
    1. In the filter definition box, select all values which do not make sense (no value, values above 100): ![](Lab2-Visualization/markdown-img-paste-20180513235711748.png)
    1. then click the `Invert` button and OK. We get a better-looking graph where we can see the trip duration distribution by age ![](Lab2-Visualization/markdown-img-paste-20180513235826902.png).
1. Now add a new Freeform tab ![](Lab2-Visualization/markdown-img-paste-20180514000047873.png) and we will create a map display of the stations by count of rentals:
    1. Select the two `Start_Station_Latitude` and `Start_Station_Longitude` fields and drop them on the canvas: ![](Lab2-Visualization/markdown-img-paste-20180514000255337.png)
    1. The system automatically creates a map display: ![](Lab2-Visualization/markdown-img-paste-20180514000346997.png)
    1. Unfortunately, there is some parasistic data with erroneous coordinates that show up in the middle of the ocean at coordinate **(0,0)** below the African continent (This virtual place is known as `Null Island`). Select the `Expand` button at the top right of the widget: ![](Lab2-Visualization/20180925_88ba6a26.png)
    1. Expand the `Start_Station_Latitude`: ![](Lab2-Visualization/markdown-img-paste-20180514001138634.png)
    1. Then select filter ![](Lab2-Visualization/markdown-img-paste-20180514001200251.png)
    1. In the filter definition, select the first `0` value, then `Invert` and OK button. The map will center itself on NYC: ![](Lab2-Visualization/markdown-img-paste-20180514001439241.png)
    1. Drop the `Station_Name` onto the `Label`: ![](Lab2-Visualization/markdown-img-paste-20180514001557213.png)
    1. We see on the map an outlier, south on the ocean, we can filter it out by name, as we can get the `8D OPS 01` label now by hovering over it. Click the Filter button for `Label`, and enter a `Does not begin with` condition for `8D OPS`: ![](Lab2-Visualization/markdown-img-paste-20180514001945589.png). The outlier point will disappear from the display.
    9. Drop the `Trip_Duration` field onto the `Point color`. The default aggregation is `SUM` which will show stations from where the cumulative trip are longer. This shows that a few stations are issuing longer rides than others, as they show in darker colors: ![](Lab2-Visualization/markdown-img-paste-20180514003647696.png)
    10. Change the aggregation used for the coloring, now based on the average trip duration. Select `Trip Duration`->`Summarize`->`Average`:![](Lab2-Visualization/markdown-img-paste-20180514003901391.png).
    11. All points now look similar. You can remove outlier manually by right-click selecting them on the map and selecting `exclude`: ![](Lab2-Visualization/markdown-img-paste-20180514004709109.png)
1. Correlated graphs selections (Widget connections)
    1. Drop the `End_Station_Latitude/Longitude` on the freesapce besides the `Start_Station` map to create a new map.
       Now, when clicking on a Station in the first map, the second map adjusts to show the corresponding `End_Station`: ![](Lab2-Visualization/20180925_e2c8e1ec.png)
    1. The same applies if you drop a label field, for example `Start_Station_Name` and `End_Station_Name`, the fields will reflect the currently selected data points subsets: ![](Lab2-Visualization/20180925_e279305e.png)
    1. Note that the selection groups can be adjusted using the `Widget connections` icon at the top ![](Lab2-Visualization/20180925_f5ea33f5.png)
1. Many other types of graphs can be built, as an exercice, build:
    1. a graph on another tab that will show the distribution of rentals by the hour of the day and user type. You should end up with a graph such as: ![](Lab2-Visualization/markdown-img-paste-20180514005845862.png)
    1. And last, build a graph that shows usage by date: ![](Lab2-Visualization/markdown-img-paste-20180514010132412.png). We see the weekly cycle, and probably the impact of weather conditions.
1. Graph elements can also act on others on the same tab. On the last tab you created, drop a `User_Type` field. This will drive the beahvior of the usage by date graph: ![](Lab2-Visualization/markdown-img-paste-20180514011121345.png)
1. Finally, dashboards can be published:
    1. Click the `Share` icon: ![](Lab2-Visualization/markdown-img-paste-20180514011738472.png)
    2. Enable sharing: ![](Lab2-Visualization/markdown-img-paste-2018051401182447.png)
    3. Open the link from another tab or browser to get a web view on the dashboard
