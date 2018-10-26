# problem_set_3
zoo6927 Problem Set 3
## Problem 1:

#!/usr/bin/env python3
import io, re
import numpy

#Create empty lists to store water level and date/time information later
water_level_list = []
date_time_list = []

#Open the file for reading and skip the first line
fh = open('CO-OPS__8729108__wl.csv', 'r')
next(fh)

#Read the file line by line, remove the new line character,
#and create an array by splitting the lines at the commas
#Assign the second column of the data to the variable water_level
#Assign the first column of the data to the variable date_time
#Try to convert each water level to a decimal value, if possible add the water level value to th$
#Also add the date_time information to the date_time list if the above was possible
for line in fh:
        line = line.strip()
        commalist = numpy.array(line.split(','))
        water_level =  (commalist[1])
        date_time = (commalist[0])
        try:
            	water_level_list.append(float(water_level))
                date_time_list.append(date_time)
        except:
               	pass
#Find the maximum water level in the water level list
        max_water_level = max(water_level_list)

#Find the index associated with the max water level and print the max water level
#Print the corresponding date_time found at the same index value
index_of_interest = (int(water_level_list.index(max(water_level_list))))
print(max_water_level)
print(date_time_list[index_of_interest])

## Problem 2:
!/usr/bin/env python3
import pandas


#Read the file into a pandas data frame
df = pandas.read_csv("CO-OPS__8729108__wl.csv")
#Print the max water level
print(df[' Water Level'].max())
#Determine the index for the max water level
index_of_interest = df[' Water Level'].idxmax()
#Print the date and time at the index where the max water level is found
print(df['Date Time'].get_value(index_of_interest))

#Note to reviewer: This code runs and does print the answer, however it will also cause error me$
#The answer prints inbetween the error messages, which is a little tricky to see at first

## Problem 3
#!/usr/bin/env python3
import io, re
import numpy

#Open the file for reading and skip the first line
fh = open('CO-OPS__8729108__wl.csv', 'r')
next(fh)

#Create empty lists to hold information later. Define the variable previous_water_level for use later
water_level_list = []
date_time_list = []
rate_list = []
previous_water_level = 0.00

#Read the file line by line. Remove the new character, make an array using commas as the delimiter.
#Define the second column as the water level
#Define the first column as the date and time
for line in fh:
        line = line.strip()
        commalist = numpy.array(line.split(','))
        water_level =  (commalist[1])
        date_time = (commalist[0])
#Try to convert each water level value to a float. If this is possible, make a new variable called numerical water level.
#Add the numerical water level value to the water level list
#Add the corresponding date and time to the date and time list
        try:
            	numerical_water_level = float(water_level)
                water_level_list.append(numerical_water_level)
                date_time_list.append(date_time)

        except:
               	pass

#If the previous water level is not zero, calculate the rate of water level change by subtracting the previous water level from
#The current water level. Then add the rate to the rate list.
#If the previous water level is zero (only applies to the first iteration through the loop), append 0 to the rate list as an index place$
#Finally, define the previous water level as the current water level before iterating through the loop again
        if previous_water_level != 0.00:
                rate = numerical_water_level - previous_water_level
                rate_list.append(rate)
        else:
             	rate_list.append(0)
        previous_water_level = numerical_water_level


#Print the max rate from the rate list.
#Determine the index associated with the max rate.
#Print the date and time associated with the same index as the max rate
print(max(rate_list))
index_of_interest = (int(rate_list.index(max(rate_list))))
print(date_time_list[index_of_interest])
