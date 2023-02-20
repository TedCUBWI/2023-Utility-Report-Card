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

For the reliability metrics specifically, we decided to use only the data that corresponded to the "IEEE Standard" and excluded all data that corresponded to an "Other Standard." This unfortunately excludes Hawaii from the state-level charts, since none of the Hawaii utilities submitted data under the IEEE standard in 2021. 

We decided to only use IEEE standard data because "other standard" data can differ on multiple points that makes it impossible to know whether comparisons between data of different standards are valid (we confered with an "electricity data expert" from the EIA who helped us come to this conclusion. One example of a difference between IEEE standard data and "other standard" data is the definition of a "nonmomentary outage." Reliability metrics are calculated by only considering at nonmomentary outages, so this definition is critical. Under the IEEE standard, any outage lasting for over five minutes is "nonmomentary." Meanwhile, utilities using alternative standards sometimes designate all outages lasting over **one** minute as "nonmomentary," while others use the IEEE five minute threshold, and others still simply use an unspecified "other" threshold. There is a column included in the reliability data that notes how utilities using an "other standard" define nonmomentary outages

SAIDI (System Average Interruption Duration Index) and SAIFI (System Average Interruption Frequency Index) data are measured directly each year and are based on all of the "nonmomentary outages" that occur in a year. SAIDI is calculated as the minutes of power outage multiplied by the percent of customers in the system that were affected by the outage. SAIFI, meanwhile, is simply the percent of customers in the system that were affected by the outage. CAIDI (Customer Average Interruption Duration Index), in comparison, is derived from the SAIDI and SAIFI values using the simple calculation of $\frac{SAIDI}{SAIFI}$, resulting in the total minutes of power outage. 

SAIDI, SAIFI, and CAIDI values can be calculated with or without "Major Event Days" (MEDs) and "Minus Loss of Supply." The latter, which covers when transmission lines fail to provide power, is only available within the IEEE standard, so it is excluded from our analysis. When MEDs are included, all outage data, regardless of cause or severity of the outage, are included. "Without MEDs" values remove any data that come from days on which that day's total SAIDI value is deemed an outlier when compared to a threshold calculated for each state using the previous five-years of SAIDI data in that state. It's important to note that because the previous five years of data are incorporated to come up with the MED threshold, a region that consistently faces poor weather that would otherwise increase outages will be penalized for failing to adapt to their average weather patterns. TKTKT if this is true from the email.   (https://www.youtube.com/watch?v=oVH9L0fCMTU) 

The resulting SAIDI "without MEDs" is meant to showcase how reliable a utilities distribution system is on a "day-to-day" basis. That said, SAIDI with and without MEDs can be correlated. For example, if a hurricane were to cause outages towards the end of a day, the SAIDI value for that day may be low enough for the day to not count as an MED, but the next few days may all be MEDs. 

So, maybe we should provide graphs of without MEDs, too? Or graphs organized by w/o MED with an x axis cutoff that makes it easier to read? 

The second major datasource for this report is form EIA-176 ("Annual Report of Natural and Supplemental Gas Supply and Disposition"). All information on natural gas provided in this report, including that on lost gas, and natural gas usage, revenues, and costs by sector are derived from the data provided via EIA-176. 

Other than data from form EIA-861 and form EIA-176, this report also uses data from form EIA-860 ("Annual Electric Generator Report") and form EIA-923 ("Power Plant Operations Report") when discussing the various fuels used for generation by and the emissions from each state's/utility's generators. The emissions data actually comes from the EPA, but is aggregated by EIA and provided at https://www.eia.gov/electricity/data/emissions/ (the 860 file is just necessary to match the plant numbers given in the emissions data with the utility that owns the plant.)

Outside of EIA data and the EPA emissions, this report also uses the U.S. Census' American Community Survey data (https://data.census.gov/table?q=heating+source&g=0100000US$0400000&tid=ACSDT5Y2021.B25040) to calculate the energy source used for heating in households across the U.S. 
