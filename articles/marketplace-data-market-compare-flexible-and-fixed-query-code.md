   
<properties 
   pageTitle="Compare Flexible and Fixed Query Code" 
   description="How to Compare Flexible and Fixed Query Code" 
   services="cloud-services" 
   documentationCenter="" 
   authors="kevinscharpenberg" 
   manager="manager-alias" 
   editor=""/>

<tags
   ms.service="marketplace"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="data-services" 
   ms.date="02/13/2015"
   ms.author="kevsch"/>
#   Compare Flexible and Fixed Query Code 
 
 -----------

Compare consuming data from a flexible query dataset and a fixed query dataset side by side.

 -----------
###Flexible and Fixed Queries

The following console application access a flexible query dataset (Dat.gov U.S. City Crime) and a fixed query dataset (Alteryx Census Demographic Data) so you can easily compare the similarities and differences.


	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Net;                                       // needed for authentication
	using FlexibleAndFixedQueries.USCrime_FlexibleQuery;    // service reference for flexible query
	using Alteryx;                                          // namespece of service class for fixed query

	namespace FlexibleAndFixedQueries
	{
    	class Program
    	{
        	// ----------------------------------------------------- CONSTANTS
        	private const string CRIME_ROOT_SERVICE_URL = "https://api.datamarket.azure.com/Data.ashx/data.gov/Crimes";
        	private const string CENSUS_ROOT_SERVICE_URL = "https://api.datamarket.azure.com/Data.ashx/Alteryx/CensusDemographicData";
        	private const string USER_ID = "yourLiveIdUserName";
        	private const string SECURE_ACCOUNT_KEY = "yourSecureMarketplaceAccuntKey";  // not your Live Id password

        	// ----------------------------------------------------- CONSTANTS FOR CENSUS QUERY
        	private const double LATITUDE = 47.604;
        	private const double LONGITUDE = -122.337;
        	private const double? RADIUS = 10.0;
        	private const double? MINUTES = null;

        	static void Main(string[] args)
        	{
            	// ------------------------------------------------- IDENTIFIERS FOR BOTH QUERIES

            	// ------------------------------------------------- IDENTIFIERS FOR FLEXIBLE QUERYY
            	IList<CityCrime> flexibleList;
            	datagovCrimesContainer flexibleContext;
            	IEnumerable<CityCrime> flexibleQuery;

            	// ------------------------------------------------- IDENTIFIERS FOR FIXED QUERY
            	IList<CensusDemographicDataEntity> fixedList;
            	CensusDemographicDataContainer fixedContext;
            	IEnumerable<CensusDemographicDataEntity> fixedQuery;

            	// ------------------------------------------------- INITIALIZE FLEXIBLE QUERY VARIABLES
            	flexibleContext = new datagovCrimesContainer(new Uri(CRIME_ROOT_SERVICE_URL));
            	flexibleContext.IgnoreMissingProperties = true;
            	flexibleContext.Credentials = new NetworkCredential(USER_ID, SECURE_ACCOUNT_KEY);

            	// ------------------------------------------------- INITIALIZE FIXED QUERY VARIABLES
            	fixedContext = new CensusDemographicDataContainer(new Uri(CENSUS_ROOT_SERVICE_URL));
            	fixedContext.IgnoreMissingProperties = true;
            	fixedContext.Credentials = new NetworkCredential(USER_ID, SECURE_ACCOUNT_KEY);

            	// ------------------------------------------------- QUERY FLEXIBLE DATASET
            	try
            	{
                	flexibleQuery = flexibleContext.CityCrime.Where(x => x.City == "Newport").OrderBy(x => x.City);

	//  ----------- equivalent LINQ query ... LINQ queries may be used with flexible query datasets
	//              flexibleQuery = from c in CityCrime
	//                                where c.City == "Newport"
	//                                orderby c.City
	//                                select c;

                	flexibleList = flexibleQuery.ToList();
            	}
            	catch (Exception ex)
            	{
                	Console.WriteLine("Flexible Error: {0}\n{1}", ex.Message, ex.InnerException.Message);
                	flexibleList = null;
                	Console.ReadKey();
            	}

            	// ------------------------------------------------- QUERY FIXED DATASET
            	try
            	{
                fixedQuery = fixedContext.GetCensusDemographicData(LATITUDE, LONGITUDE, RADIUS, MINUTES);  
                                                                   // Either RADIUS or MINUTES may have a value, at least one must be null
                fixedList = fixedQuery.ToList();
            }
            catch (Exception ex)
            {
                Console.WriteLine("Fixed Error: {0}\n{1}", ex.Message, ex.InnerException.Message);
                fixedList = null;
                Console.ReadKey();
            }


            // ------------------------------------------------- PRINT FLEXIBLE RESULTS
            Console.WriteLine("Crime Data");
            Console.WriteLine("{0,-15} {1,-15} {2,4} {3,10} {4,13}", "City", "State", "Year", "Population", "Violent Crime");
            if (flexibleList != null)
            {
                foreach (CityCrime crime in flexibleList)
                    Console.WriteLine("{0,-15} {1,-15} {2,4} {3,10} {4,13}", crime.City,
                                                                             crime.State,
                                                                             crime.Year,
                                                                             crime.Population,
                                                                             crime.ViolentCrime);
            	}

            	// ------------------------------------------------- PRINT 	FIXED RESULTS
            	Console.WriteLine("\nDemographic Data");
            	Console.WriteLine("{0,-35} {1,15} {2,6} {3,6}", "Name", 	"Population", "Female", "Male");
            	if (fixedList != null)
            	{
                	foreach (CensusDemographicDataEntity entity in fixedList)
                    Console.WriteLine("{0,-35} {1,15} {2,6} {3,6}", entity.NAME,
                                                                     entity.POP00,
                                                                     entity.SEX00FEM,
                                                                     entity.SEX00MAL);
            	}

            	// ------------------------------------------------- HOLD OUTPUT ON SCREEN UNTIL KEY IS STRUCK
            	Console.Write("Tap any key to end. ");
            	Console.ReadKey();

        	}
    	}
	}


 -----------
##See Also

###Tasks
Compare Fixed and Flexible Query Types <br>
Create a Flexible Query Application <br>
Create a Fixed Query Application
