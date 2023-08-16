# 2023 Utility Report Card

This document is a basic "report card" for utilities. Our goal is to produce the report annually early in the calendar year with data from the calendar year two years prior (e.g. 2023 report released in March uses data for the calendar year of 2021).

We included all of the data and code used to generate this report in this github repo for the sake of transparency and to encourage other parties to repurpose/modify the document to match their own purposes.

Below is a detailed explanation of the data sources that we used to create this document as well as the methodology we used to generate the graphs, which is organized by data source. Note that each graph in the report includes its data source, which should allow anyone to search for the relevant section of this ReadMe file.

**RUNNING THE CODE:** First, make sure that you have R and RStudio downloaded on your computer: R - <https://cloud.r-project.org/> RStudio - <https://posit.co/downloads/>

The latest version of the report was created using R version 4.2.3 and RStudio version 2023.03.0 build 386.

Next, go to our github repository (<https://github.com/CUBWI/2023-Utility-Report-Card>) and click on the "Code" dropdown menu. You can go through the process of setting up Github Desktop if you'd like, but you can also simply clikc "Download ZIP." All of the code and data on our github for this project will then download to your computer. Go to your downloads and select the ZIP folder and extract its contents. You can then open the "finalized code.Rmd" file and click "knit" and it will generate the report.

**DATA SOURCES:**

EIA-176: <https://www.eia.gov/naturalgas/ngqs/> (Next to "Download," click the furthest right of the three icons - if you float your cursor over it it will say "Download entire data to delimited text file.")

EIA-861: <https://www.eia.gov/electricity/data/eia861/>

Census Heating Fuel Type (B25040): <https://data.census.gov/table?q=heating+source&g=010XX00US$0400000&tid=ACSDT1Y2021.B25040> (click the CSV icon to download the version that the code is written for).

**METHODOLOGY:**

***EIA-861***

Much of the data used in this report come from the Annual Electric Power Industry Report, also known as EIA-861. As stated on the EIA website, this survey "is a census of all United States electric utilities." A ZIP file of the data gathered from this survey can be downloaded from the eia website at <https://www.eia.gov/electricity/data/eia861/>. The ZIP file contains numerous files containing data on different subjects. Data on demand response and energy efficiency programs were taken from the "Demand Response" and "Energy Efficiency" files, respectively. SAIDI, SAIFI, and CAIDI metrics were all taken from the "Reliability" file. Lastly, the "Sales to Ultimate Customers" provided revenue (\$000s), energy sales (MWh), and customer numbers disaggregated by sector. All data is at the utility-state level (so if a utility operates in multiple states, there are separate rows corresponding to its operations in each state).

**Reliability Metrics**

*Data Description*

Utilities record SAIDI (System Average Interruption Duration Index) and SAIFI (System Average Interruption Frequency Index) data for each "nonmomentary outage" that occurs on their systems (see below for a definition of "nonmomentary"). SAIDI is calculated as the minutes of power outage multiplied by the percent of customers in the system that were affected by the outage. SAIFI, meanwhile, is simply the percent of all customers in the system that were affected by the outage. CAIDI (Customer Average Interruption Duration Index), meanwhile, is derived from the SAIDI and SAIFI values using the simple calculation of $\frac{SAIDI}{SAIFI}$, resulting in the average minutes of power outages per customer for the outage event. These data are submitted to the EIA, which then aggregates cummulatively the values into annual figures for each utility-state combination

The metrics are further split to account for "Major Event Days" (MEDs). Using MEDs is a strategy to account for when a utility's outages are caused by a major event (e.g. an earthquake) that is outside of a utility's control. As a result, SAIDI without MED is meant to show how reliable a utility is in its day-to-day operations.

The reliability data also includes columns that give the metrics "Minus LOS," where LOS stands for loss of supply. These "Minus LOS" metrics account for when the transmission system fails to deliver energy and causes an outage. Transmission systems can be operated by entities other than the local utility that controls the distribution system and so this is again a means of accounting for outages that are beyond a utility's control (a helpful explainer on all of these details can be found here: <https://www.youtube.com/watch?v=oVH9L0fCMTU>).

*Data Quality Considerations*

For the reliability metrics, we decided to use only the data that corresponded to the "IEEE standard" and we excluded all data that corresponded to any "other standard." This unfortunately excludes Hawaii from the 2021 state-level charts, since none of the Hawaii utilities submitted data under the IEEE standard in 2021.

We decided to only use IEEE standard data because "other standard" data can differ on multiple points that makes it impossible to know how exactly to make comparisons between data of different standards (we conferred with an "electricity data expert" from the EIA who helped us come to this conclusion).

One example of a difference between IEEE standard data and "other standard" data is the definition of a "nonmomentary outage." Reliability metrics are calculated by only considering nonmomentary outages, so this definition is critical. Under the IEEE standard, any outage lasting for over five minutes is "nonmomentary." Meanwhile, utilities using alternative standards sometimes designate all outages lasting over **one** minute as "nonmomentary," while others use the IEEE five minute threshold, and others still simply use an unspecified "other" threshold. There is a column included in the reliability data that notes how utilities using an "other standard" define momentary outages (less than 1 minute (L), less than 5 minutes (F) or 'other' (O)), so one might consider including "other standard" data where a momentary outage is equal to less than 5 minutes, but there is at least one other important difference between standards that would continue to jeopardize clear comparisons.

The other major way that standards can differ is in the threshold used to define "Major Event Days" (MEDs). The EIA data does not explain how utilities using non-IEEE standards define their MED thresholds. While the IEEE standard uses the past 5 years of data (or as much data as possible if the utility has less than 5 years of data), under another standard, more or less data may be included. Beyond the amount of data used, the exact equation used to calculate the threshold may differ as well (the equation used for the IEEE standard can be found here: <https://cmte.ieee.org/pes-drwg/wp-content/uploads/sites/61/2003-01-Major-Events-Classification-v3.pdf>).

The one caveat to our exclusion is that we did choose to include Wisconsin Power & Light in our Wisconsin IOU charts despite the fact that they rely on an alternative standard for defining a "major event." WP&L is one of the major utilities in Wisconsin, so any chart that excluded them would have seemed incomplete. Furthermore, we were able to reach out to WP&L directly and were told that the standard that they use results in a very similar categorization of "major events" as the IEEE standard. WP&L uses the definition of a "Major Event" required by the Iowa Utility Board (Iowa's regulatory commission) and defined in Iowa Administrative Code 199 ??20.18(4). The statute reads: "'Major event' will be declared whenever extensive physical damage to transmission and distribution facilities has occurred within an electric utility's operating area due to unusually severe and abnormal weather or event and:

<ol>

<li>Wind speed exceeds 90 mph for the affected area, or</li>

<li>One-half inch of ice is present and wind speed exceeds 40 mph for the affected area, or</li>

<li>Ten percent of the affected area total customer count is incurring a loss of service for a length of time to exceed five hours, or</li>

<li>20,000 customers in a metropolitan area are incurring a loss of service for a length of time to exceed five hours."</li>

</ol>

Again, we chose to include WP&L's data despite their using an alternative standard because of the assurance by WP&L that their MED standard yields similar results to the IEEE standard, the fact that WP&L uses the same definition of a nonmomentary outage as the IEEE standard, and the importance of presenting data on WP&L due to the utility's size.

*Calculating the State-Level Reliability Metrics*

Taking an average of or sum of SAIDI, SAIFI, or CAIDI values across all of the utilities in a state would lead to a false ranking of the states by each metric. Doing so fails to weight the utilities by the number of customers served and, relatedly, states with a greater number of utilities would have their results inflated.

Therefore, to come up with the state-level values, the metrics are broken down into their components for each utility (e.g. the total duration of customer interruptions across customers, the total number of customers that had interruptions), these components are then combined across the state, and then the metric is recalculated with these component parts.

**Sales to Ultimate Customers**

The sales to ultimate customer Excel files have some instructions at the bottom of the file for users of the data to correctly aggregate the data. We provide some extra details here for additional clarity.

*Aggregating the Data Correctly*

The first point to be careful of is to exclude "Part C" entries when aggregating total customer and total energy sales numbers at the state level. Sales to ultimate customers data is split into 4 different parts, as denoted by the "parts" column. These parts correspond to different levels of service that customers receive. Part A corresponds to "full service," which includes both energy and distribution services, Part B to corresponds just to energy services, Part C to delivery-only services "and all other charges", and Part D to "Bundled Service (Energy Service Providers and Power Marketers)". In states that allow retail choice, where a customer can choose who they buy their electricity from, the entity providing energy services (Part B) can differ from the entity that delivers the services (Part C). But, both entities will report the customer as their own and the energy sold/delivered as their own. Excluding Part C for the calculating the customer count and the amount of energy sold therefore allows us to avoid double-counting when aggregating the data to the state level. Part C is included in the calculation of costs, however, since we cannot ignore, for example, the 4 cents/kWh paid for delivery services or the 12 cents/kWh paid for energy services.

Another point to be careful of is that entries with an "Ownership" value of "Behind the Meter" should be excluded when calculating state-level customer counts. "Behind the"Meter" entries correspond to third-party owned solar systems and third-party solar customers generally still have a primary energy-service provider. Counting both entries, therefore, will double count that customer.

**Energy Efficiency**

*Investments by an Efficiency Program Administrator* One thing to look out for when measuring the energy efficiency investments of individual utilities is that in certain instances the utility is contributing to energy efficiency programs that are administered by another entity. In such an instance, the efficiency investments will be reported by, and therefore attributed to, said program administrator. This is the case for Wisconsin's IOUs, which are all statutorily required to contribute to the states energy efficiency program, which is administered by Focus on Energy. A Wisconsin IOU could, and we would argue that they should, invest in energy efficiency beyond the simple statutorily required amount, but it would be inaccurate to conclude from the dataset that they are not investing in efficiency at all.

*Annualizing Life Cycle Values Instead of Using Reporting Year Incremental Annual Values* For our energy efficiency charts, we focus on the reported life cycle savings/costs from efficiency programs rather than using reporting year incremental annual savings/costs. We do this because the costs and savings of a program may not be equal over time. For example, a state or utility may seem like a major investor in energy efficiency in a particular year when in reality they just happened to start multiple programs during that reporting year and all of the costs come in the first year of the program.

Because the lifetime of a single program is the same, when we strictly compare costs and savings we do not need to annualize the values. This fact is made clear by the following equation: $$ \frac{\frac{Costs}{Lifetime}}{\frac{Savings}{Lifetime}} = \frac{Costs}{Savings} $$

For the other, non-sector-level metrics that incorporate data from the "Sales to Ultimate Customer" section, we needed to calculate annualized total savings and total costs since the data did not provide an aggregate average lifetime of all programs across sectors. So, after annualizing the lifecycle values by dividing the value by the expected lifetime, we summed the values together across sectors to come up with the total savings or costs. Unfortunately, if a program had a reported lifetime of zero years, which occurred in some instances, this would result in infinite costs or savings and these values had to be removed - because of this, the annualization process did result in some data loss.

An alternative solution to the fluctuations of values in any single year would be to use a 3-year average of reporting year incremental annual savings/costs (or an average across some other time period). We did not explore this option so we cannot say how it compares to the annualization strategy that we used.

**Demand Response**

Because demand response programs are used primarily to lower the peak load of a utility, understanding the proportion of total peak load enrolled in demand response programs would be a more effective metric at understanding which utilities are successfully using demand response to avoid supply-side solutions to load issues. We have not yet explored a simple way to access the peak load values utilities around the U.S., though. The figure showing demand response program participation rates among Wisconsin utilities shows that over 200% of NSPW industrial customers participate in demand response programs. We reached out to EIA to ask what might be causing the data to indicate a 200% participation rate and received several suggestions in response.

First, NSPW might simply have overcounted. Looking at the text of form EIA-861, one customer enrolled in multiple DR programs should still be counted as one customer, if you follow the letter of the form, but an error could still have been made.

Second, NSPW could be running DR programs for customers that are not retail customers. If NSPW sells energy wholesale to an entity that then sells that energy elsewhere, then that customer would not appear in the "Sales to Ultimate Customers" file for NSPW, but that customer may still participate in a DR program run by NSPW, therefore showing up in its DR data. This would not seem to explain the massive overcounting, but is still a potential source for error to consider.

The third suggestion applies much more broadly to EIA 861 data and is written out below.

**Issues with Combining Data Across EIA 861 Sections**

It is often the case, particularly for large utilities, that different departments fill out different parts of the 861 survey. This can (and is known to) cause issues because the definition used for "industrial" by the group that fills out the "Sales to Ultimate Customer" section may differ from the group that fills out the "Demand Response" section.

While the EIA does provide definitions for the Residential, Commercial, Industrial, and Transportation sectors, they do not conduct any audits to ensure if those definitions are being followed. Apparently, in states with retail choice, the issue of differing definitions is abundantly clear because the the number of commercial vs. industrial customers in a state will differ massively depending on if the energy services provider is providing the information or the delivery services provider.

According to the EIA, this issue of differing sector definitions is intractable. They stated that "residential" is somewhat more easily differentiated from "commercial" and "industrial," but the latter two are particularly difficult to clearly separate.

Despite the issue outlined above, this report provides sector-level charts even when it incorporates data from different sections of EIA 861 (e.g. the demand response participation charts). Still, we may choose to more simply compare residential and non-residential sectors in future iterations of the report if further discussions with the EIA data experts leads us to believe that the sector-level charts are too unreliable.

***EIA-176***

The second major data source used for this report comes from form EIA-176 ("Annual Report of Natural and Supplemental Gas Supply and Disposition"). All information on natural gas presented in this report are derived from the data provided via EIA-176.

Regarding the data file actually provided on GitHub, to allow for the file to be pushed to GitHub I removed the first couple of sheets (to get it below 100MB in size). If you would like to run analyses going back to 1997 you can use the URL at the top of the file to get the original data. 

**Lost Gas and Unaccounted for Gas**

Lost gas is defined as any gas lost as a "natural consequence of distribution activities." In form EIA-176, respondents are requested to report their best estimate of this value, meaning that there is a degree of error associated with the value.

This estimate-error helps clarify the difference between "lost gas" and "unaccounted for gas." While "lost gas" is a specific component of the "total disposition" (see below) of gas by a respondent, "unaccounted for gas" is simply the difference between the reported total supply of gas that the respondent took in or started with and the total disposition of gas that the respondent distributed out. There are multiple figures in EIA-176 that require some degree of estimate from the respondent. The "unaccounted for gas" simply shows how these estimates were inaccurate in aggregate, but it is impossible to attribute the unaccounted for gas to any particular estimate.

A high value of unaccounted for gas relative to the total amount of gas distributed by a respondent could indicate poor book keeping, but it does not necessarily carry the same environmental and financial implications of lost gas.

**Total Disposition**

To put the total lost gas value in context, we present a couple of figures that show lost gas in proportion to the "total disposition" of natural gas. The total disposition value corresponds to the amount of natural gas that a utility has distributed in the year in question. Other reports similar to ours have instead used total sales as the denominator, but we felt that what mattered most was the amount of natural gas that a utility was "in charge of," rather than how much is eventually sold. With the same logic, one could alternatively choose to use "total supply" as the denominator, since in theory total supply and total disposition should be equal ("unaccounted for gas" is the metric given for the difference between supply and disposition).

**Heat Content**

As stated in the code, in some instances the EIA-176 data for certain respondents lacks an entry for the average heat content of the gas that the utility used. Our solution for this is to use a state-average heat content instead. This allows us to discuss gas usage with the more well-used units of therms or MMBTUs rather than cubic feet.

We chose to use the median as the average since the distribution of heat contents across the utilities in the data was not normal and so we did not want to use the mean and allow the average to be skewed by any single value. In any case, the difference between using the mean and median was marginal.

***Other Data Sources***

**Form EIA-923** Form EIA-923 ("Power Plant Operations Report") provides data on the amount of generation from different plants in the U.S., the owners of the plant, and the fuel that the plant uses.

In particular, we use the file that includes schedules 2, 3, 4, and 5 (e.g. "EIA923_Schedules_2\_3_4\_5_M\_12_2021_Final.xlsx").

Only EIA sectors numbers 1, 2, and 3, are included for the calculations of generation and emissions from utilities. The EIA Sector Numbers are organized as follows:

<ol>

<li>Electric Utility</li>

<li>NAICS-22 Non-Cogen</li>

<li>NAICS-22 Cogen</li>

<li>Commercial NAICS Non-Cogen</li>

<li>Commercial NAICS Cogen</li>

<li>Industrial NAICS Non-Cogen</li>

<li>Industrial NAICS Cogen</li>

</ol>

The NAICS two digit code "22" corresponds to utilities. So in addition to "Electric Utility" any generation or emissions associated with a NAICS-22 entity was also included in the calculations (Appendix C to "Electric Power Monthly" confirms that Sectors 1, 2, and 3 make up the "Electric Power Secotr": <https://www.eia.gov/electricity/monthly/pdf/technotes.pdf>)

*Hard-coded calculations* For aggregating different fuel types into single categories (e.g. all the components of renewables), we simply hard coded the equations. For the WI utility charts, this includes removing the categories, such as RFO (residual fuel oil), that did not appear in the data. If an RFO facility appears in subsequent years, it would be easy to accidentally not include that facility in a calculation. We will look to make subsequent versions of the code more change-proof, but in the meantime users will just have to be careful to not accidentally exclude any facilities.

**Emissions Data** The report also uses emissions data that comes from the EPA, but is aggregated by EIA and provided at <https://www.eia.gov/electricity/data/emissions/>.

We only look at the emissions from the "ELECTRIC POWER" sector and ignore the "COMMERCIAL" and "INDUSTRIAL" sectors for our calculations.

*Metrics* For our charts, we choose to use the "Tons of CO2 Emissions," "EIA Model Estimates of SO2 Emissions (Tons)," and "EIA Model Estimates of NOx Emissions (Tons)." We did not do any detailed research into the exact differences between "EIA Model Estimates of SO2 Emissions (Tons)," "CEMS Reported Plant Level SO2 Emissions (Tons)" and "Selected SO2 Emissions (Tons)," and simply chose the former due to the fact that it seemed to be the most complete.

We welcome any arguments for using some of the alternative emissions metrics.

**Form EIA-860** Form EIA-860 ("Annual Electric Generator Report") provides a crosswalk file to know what plants in the U.S. are owned by which utility. We use this information to match the plant numbers given in the emissions data with the utility that owns the plant.

We also use EIA-860's ownership data to attribute generation and emissions to the correct party when a plant is owned by multiple entities (attributions are by ownership share).

**Census Data**

Outside of EIA data and the EPA emissions, this report also uses the **U.S. Census' American Community Survey** data to calculate the energy source used for heating in households across the U.S. Specifically, we look at the 2021 1-year estimate and look at question B25040 ("House Heating Fuel")

The question asked of survey respondents is "Which FUEL is used MOST for heating this house, apartment or mobile home?"

*1-Year vs. 5-Year Estimates*

Census.Gov recommends using 1-Year estimates in moments when the recency of the data is more important than its precision and when you are analyzing larger populations. Because we plan to remake this chart annually and because the data are presented at the state population level, we felt that the 1-Year estimate best served our purposes.

*Other Heating Fuels*

The fuel options that make up the "other heating fuels" category for the heating fuels chart include:

<ul>

<li>"Bottled, tank, or LP gas"</li>

<li>"Fuel oil, kerosene, etc."</li>

<li>"Coal or coke"</li>

<li>"Wood"</li>

<li>"Solar energy"</li>

<li>"Other fuel"</li>

</ul>

As stated in the report, bottled gas and fuel oil are the primary components of "other" for most states.

**Generation and Emissions Data**

Our report does not include data on the generation mix that states or utilities rely upon and does not include any data regarding the emissions associated with energy use. 

*Using EIA 860 and EIA 923 Data*

We had originally hoped to use EIA 860 (https://www.eia.gov/electricity/data/eia860/), EIA 923 (https://www.eia.gov/electricity/data/eia923/), and plant-level emissions data (https://www.eia.gov/electricity/data/emissions/) to illustrate generation mix and emissions associated with energy demand. This remains, as far as we know, the best EIA data to use to come up with an estimate of emissions associated with individual utilities.

There are two sources of error that led us to lose confidence in this strategy. First, using these three sources excludes any data on Power Purchasing Agreements, where a utility purchases power from a generator somewhere. For example, in Wisconsin, the Wisconsin Electric Power Company currently buys a large amount of electricity from the Point Beach Nuclear Plant, which is owned and operated by NextEra Energy. This relationship and any similar relationships are not captured by any EIA data, meaning large portions of a utilities portfolio would be omitted. 

Second, in some instances a plant would be attributed to a utility's subsidiary rather than to the utility itself. For example, according to EIA-860's "Generator Ownership" data, the Elm Road Generating Station is co-owned by Madison Gas & Electric, WPPI Energy, and We Power. We Power is a subsidiary of the Wisconsin Electric Power Company (WEPCO). We need to know that subsidiary relationship ahead of time to ensure that our code accurately attributes the generation and emissions associated with the plant to WEPCO. Otherwise it just assumes that We Power is one of the smaller utilities that we've chosen not to include in our charts. We could catch issues like these on a one off basis, but our goal is to create a fully automatable process. Given these two issues, we decided the resulting charts were not providing accurate enough information to present publicly. 

*Best Data for State Level Generation*

According to EIA staff, the best data to use to answer generation mix and emission questions at the state level is from the State Electricity Profile data (available here: https://www.eia.gov/electricity/state/). We will look to use this data to present charts in future iterations of this report but were unable to do so in time for the release of the current report. 

*Details of the Original Process*

We include the details from our original attempts to create these graphs in case anyone feels that there is value in the more specific result of generation mix/emissions specifically from plants **owned** by utilities. There are some peculiarities to the EIA 923 and EIA 860 data so hopefully this can help yield the results users are looking for. 

**Form EIA-923** Form EIA-923 ("Power Plant Operations Report") provides data on the amount of generation from different plants in the U.S., the owners of the plant, and the fuel that the plant uses.

In particular, the file to use is the one that includes schedules 2, 3, 4, and 5 (e.g. "EIA923_Schedules_2\_3_4\_5_M\_12_2021_Final.xlsx").

Only EIA sectors numbers 1, 2, and 3, are included for the calculations of generation and emissions from utilities. The EIA Sector Numbers are organized as follows:

<ol>

<li>Electric Utility</li>

<li>NAICS-22 Non-Cogen</li>

<li>NAICS-22 Cogen</li>

<li>Commercial NAICS Non-Cogen</li>

<li>Commercial NAICS Cogen</li>

<li>Industrial NAICS Non-Cogen</li>

<li>Industrial NAICS Cogen</li>

</ol>

The NAICS two digit code "22" corresponds to utilities. So in addition to "Electric Utility" any generation or emissions associated with a NAICS-22 entity was also included in the calculations (Appendix C to "Electric Power Monthly" confirms that Sectors 1, 2, and 3 make up the "Electric Power Sector": <https://www.eia.gov/electricity/monthly/pdf/technotes.pdf>)

**Emissions Data** Plant-level emissions data is provided at <https://www.eia.gov/electricity/data/emissions/>.

Note that sectors include the "ELECTRIC POWER," "COMMERCIAL," and "INDUSTRIAL" sectors and so the latter two should be excluded for just looking at utility emissions. 

**Form EIA-860** Form EIA-860 ("Annual Electric Generator Report") provides a crosswalk file to know what plants in the U.S. are owned by which utility. This information can be used to match the plant numbers given in the emissions data with the utility that owns the plant.

EIA-860's ownership data is also helpful for attributing generation and emissions to the correct party when a plant is owned by multiple entities (attributions can be made by ownership share).
