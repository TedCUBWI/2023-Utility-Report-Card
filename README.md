# 2023-Utility-Report-Card
Basic "report card" for utilities produced annually early in the CY. 

The code and data contained in this github repo are provided to encourage transparency and repurposing/modification by other parties to match their own purposes. 

Below is a detailed explanation on the data sources used to create this document as well as the methodology used to generate the particular graphs that use a particular data source. Note that each graph in the report contains its data source, allowing anyone to search for the relevant section of this readme file. 

DATA SOURCES:
EIA-176: https://www.eia.gov/naturalgas/ngqs/ (Next to "Download" select "Download entire data to delimited text file.")
EIA-860: https://www.eia.gov/electricity/data/eia860/
EIA-861: https://www.eia.gov/electricity/data/eia861/
EIA-923: https://www.eia.gov/electricity/data/eia923/
EIA Emissions by Plant Estimates: https://www.eia.gov/electricity/data/emissions/
Census Heating Fuel Type (B25040): https://data.census.gov/table?q=heating+source&g=0100000US$0400000&tid=ACSDT5Y2021.B25040

METHODOLOGY:
**EIA-861**
Much of the data used in this report come from the Annual Electric Power Industry Report, also known as EIA-861. As stated on the EIA website, this survey "is a cenus of all United States electric utilities." A ZIP file of the data gathered from this survey can be downloaded from the eia website at https://www.eia.gov/electricity/data/eia861/. The ZIP file contains numerous files containing data on different subjects. Data on demand response and energy efficiency programs were taken from the "Demand Response" and "Energy Efficiency" files, respectively. SAIDI, SAIFI, and CAIDI metrics were all taken from the "Reliability" file.  Lastly, the "Sales to Ultimate Customers" provided revenue ($000s), energy sales (MWh), and customer numbers disaggregated by sector. All data is at the utility level.

**Reliability Metrics**
*Data Description*
SAIDI (System Average Interruption Duration Index) and SAIFI (System Average Interruption Frequency Index) data are measured directly each year and are based on all of the "nonmomentary outages" that occur in a year. SAIDI is calculated as the minutes of power outage multiplied by the percent of customers in the system that were affected by the outage. SAIFI, meanwhile, is simply the percent of customers in the system that were affected by the outage. CAIDI (Customer Average Interruption Duration Index), in comparison, is derived from the SAIDI and SAIFI values using the simple calculation of $\frac{SAIDI}{SAIFI}$, resulting in the total minutes of power outage. 

The metrics are generally further split to account for "Major Event Days" (MEDs). Using MEDs is a strategy to account for when a utility's outages are caused by a major event (e.g. an earthquake) that is outside of a utility's control. Therefore, SAIDI without MED, for example, is meant to show how reliable a utility is in its day-to-day operations. The reliability data also includes columns that give the metrics with MEDs and "Minus LOS," where LOS stands for loss of supply. These "Minus LOS" metrics account for when the transmission system fails to deliver energy and causes an outage. Transmission systems are often controlled by entities other than a local utility, which generally controls the distribution system, and so this is again a means of accounting for outages that are beyond a utility's control (a helpful explainer on all of these details can be found here: https://www.youtube.com/watch?v=oVH9L0fCMTU).

*Data Quality Considerations*

For the reliability metrics, we decided to use only the data that corresponded to the "IEEE standard" and we excluded all data that corresponded to an "other standard." This unfortunately excludes Hawaii from the state-level charts, since none of the Hawaii utilities submitted data under the IEEE standard in 2021. It also excludes Wisconsin Power & Light from our Wisconsin IOU charts. 

We decided to only use IEEE standard data because "other standard" data can differ on multiple points that makes it impossible to know whether comparisons between data of different standards are valid (we conferred with an "electricity data expert" from the EIA who helped us come to this conclusion). One example of a difference between IEEE standard data and "other standard" data is the definition of a "nonmomentary outage." Reliability metrics are calculated by only considering nonmomentary outages, so this definition is critical. Under the IEEE standard, any outage lasting for over five minutes is "nonmomentary." Meanwhile, utilities using alternative standards sometimes designate all outages lasting over **one** minute as "nonmomentary," while others use the IEEE five minute threshold, and others still simply use an unspecified "other" threshold. There is a column included in the reliability data that notes how utilities using an "other standard" define momentary outages (less than 1 minute (L), less than 5 minutes (F) or ‘other’ (O)), so one could simply look only at "other standard" data where a momentary outage is equal to less than 5 minutes, but there is another important difference between standards that would continue to jeopardize valid comparisons. 

The other major way that standards differ, potentially, is in the threshold used to define "Major Event Days" (MEDs). The issue is that it is impossible to know how exactly a MED threshold has been defined by utilities using non-IEEE standards. While the IEEE standard uses the past 5 years of data (or as much data as possible if the utility has less than 5 years of data), under another standard, more or less data may be included which potentially invalidate comparisons between "without MEDs" metrics. Beyond the amount of data used, the exact equation used to calculate the threshold may differ as well (the equation used for the IEEE standard can be found here: https://cmte.ieee.org/pes-drwg/wp-content/uploads/sites/61/2003-01-Major-Events-Classification-v3.pdf).

*Sales to Ultimate Customers*
Sales to ultimate customers data is split into 4 different parts, as denoted by the "parts" column, corresponding to different levels of service that customers receive. Part A corresponds to "full service," which includes both energy and distribution services, Part B to corresponds just to energy services, Part C to delivery-only services "and all other charges", and Part D to "Bundled Service (Energy Service Providers and Power Marketers)". As stated in the instructions for form 861, the "the amount of electricity sold to customers purchasing electricity for their own use and not for resale" is the sum of parts A, B, and D. So, for our calculations, which focus on costs to end-users, we exclude part C values from consideration. For questions though, that use a utility's total revenues as a comparison point for their investments in demand response or energy efficiency, we include Part C since excluding it would understate a single utility's revenues. 

*Energy Efficiency*
One thing to look out for when measuring the energy efficiency investments of individual utilities is that in certain instances the utility is contributing to energy efficiency programs that are administered by another entity. In such an instance, the efficiency investments will be reported by and therefore attributed to said program administrator, rather than the utility itself. This is the case for Wisconsin's IOUs, which are all statutorily required to contribute to the states "Focus on Energy" program, which is administered by Focus on Energy (that said, a Wisconsin IOU could, and we would argue that they should, invest in energy efficiency beyond the simple statutorily required amount).

*Demand Response*
We do not have any notes to include on the demand response data.

**EIA-176**
The second major data source used for this report comes from form EIA-176 ("Annual Report of Natural and Supplemental Gas Supply and Disposition"). All information on natural gas provided in this report, including that on lost gas, and natural gas usage, revenues, and costs by sector are derived from the data provided via EIA-176. 

*Total Disposition*
To put the total lost gas value in context, we present a couple of figures that show lost gas in proportion to the "total disposition" of natural gas. This value corresponds to the amount of natural gas that a utility has distributed in the year in question. Other similar reports have instead used total sales as the denominator, but we felt that what mattered most was the amount of natural gas that a utility was "in charge of," rather than just how much they eventually sell. We alternatively could have chosen to use "total supply" as the denominator, although in theory total supply and total disposition should be equal ("unaccounted for gas" is the metric given for the difference between supply and disposition). 

**Other Data Sources**
Other than data from form EIA-861 and form EIA-176, this report also uses data from **form EIA-860** ("Annual Electric Generator Report") and **form EIA-923** ("Power Plant Operations Report") when discussing the various fuels used for generation by each state's/utility's generators. Emissions data comes from the EPA, but is aggregated by EIA and provided at https://www.eia.gov/electricity/data/emissions/. The EIA-860 file is used simply to match the plant numbers given in the emissions data with the utility that owns the plant.)

Outside of EIA data and the EPA emissions, this report also uses the U.S. Census' American Community Survey data (https://data.census.gov/table?q=heating+source&g=0100000US$0400000&tid=ACSDT5Y2021.B25040) to calculate the energy source used for heating in households across the U.S. 
