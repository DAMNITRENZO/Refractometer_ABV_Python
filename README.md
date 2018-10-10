# Refractometer_ABV_Python

#Bugsy's Refractometer ABV Calculator
#Version 1.04.2
#10-10-2018
#Created By: Bugsy

from decimal import Decimal #decimal function used with round to manage decimal places
import time #time function used to pause calculations in command prompt
import os #used to clear screen when recalculating

num = 1 #used to count while loop iterations

#while loop allows new calculations once an iteration is complete
while num == 1:
	
	gravity = 0 #used to count while loop iterations - *must be placed within num while loop*
	count = 0 #used to count while loop iterations - *must be placed within num while loop*
	
	#display tool name
	print("BUGSY'S REFRACTOMETER ABV CALCULATOR")
	print('------------------------------------')

	#store input numbers
	while gravity == 0: #while loop checks the gravity readings
		og = input('Enter original gravity? ') #prompts user to enter original gravity
		og = float(og) #converts the string value to float
		if og > 1.000 and og <= 1.200: #checks that the input value is within the acceptable range
			gravity = gravity + 1 #ends the loop
		else:
			print(' ')
			print("ERROR: ***Please Enter a value between 1.001 and 1.200***") #instructs user to enter correct values
			print(' ')
			
	while gravity == 1:	#while loop checks the gravity readings
		fg = input('Enter final gravity? ') #prompts user to enter original gravity
		fg = float(fg) #converts the string value to float
		if fg > 1.000 and fg <= 1.200: #checks that the input value is within the acceptable range
			gravity = gravity + 1 #ends the loop
		else:
			print(' ')
			print("ERROR: ***Please Enter a value between 1.001 and 1.200***") #instructs user to enter correct values
			print(' ')
			
	#main calculations
	#convert original gravity to original brix
	brixog = (((182.4601 * float(og) - 775.6821) * float(og) + 1262.7794) * float(og) - 669.5622)
	brixog_output = round(brixog,2) #round function used to adjust decimal places

	#convert preadjusted final gravity to preadjusted final brix
	brixfg = (((182.4601 * float(fg) - 775.6821) * float(fg) + 1262.7794) * float(fg) - 669.5622)
	brixfg_output = round(brixfg,2) #round function used to adjust decimal places

	#adjust measured final gravity
	adjusted_fg = Decimal(1.0000 - 0.00085683 * float(brixog) + 0.0034941 * float(brixfg))
	adjusted_fg_output = round(adjusted_fg,3) #round function used to adjust decimal places

	#calculate ABV with OG and adjusted FG
	abvCalc = float(og) - float(adjusted_fg)
	abv = Decimal(abvCalc * 131.25)
	abv_output = round(abv,2) #round function used to adjust decimal places

	#calculate attenuation with OG and adjusted FG
	attnCalc = (float(og) - 1) * 1000 - (float(adjusted_fg) - 1) * 1000
	attn = Decimal(attnCalc / ((float(og) - 1) * 10))
	attn_output = round(attn,2) #round function to adjust decimal places

	#calculate calories using OG and adjusted FG
	calAbv = 1881.22 * float(adjusted_fg) * (float(og) - float(adjusted_fg)) / (1.775 - float(og))
	calCarb = 3550 * float(adjusted_fg) * ((0.1808 * float(og)) + (0.8192 * float(adjusted_fg)) - 1.0004)
	calories = Decimal(float(calAbv) + float(calCarb))
	calories_output = round(calories,2) #round function used to adjust decimal places

	#display functions
	print('-------------------------------')
	print('BEER ROBOT IS CONVERTING GRAVITY TO BRIX...')
	time.sleep(1) #sleep funtion is used to pause between calculations
	print('BRIX OG: {0}'.format(brixog_output))
	print('BRIX FG: {0}'.format(brixfg_output))
	print('-------------------------------')
	print('BEER ROBOT IS ADJUSTING FINAL GRAVITY READING...')
	time.sleep(1) #sleep funtion is used to pause between calculations
	print('Adjusted FG: {0}'.format(adjusted_fg_output))
	print('-------------------------------')
	print('BEER ROBOT IS CALCULATING BEER STATISTICS...')
	time.sleep(1) #sleep funtion is used to pause between calculations
	print('ABV: {0}%'.format(abv_output))
	print('Attenuation: {0}%'.format(attn_output))
	print('Calories: {0} Per 12oz'.format(calories_output))
	print('-------------------------------')
	robot = input('Press Enter to Continue')
	print('-------------------------------')
	print('BEER ROBOT: "ENJOY YOUR BREW"')
	print(' ')
	print('                    .sssssssss. ')
	print('                .sssssssssssssssssss ')
	print('              sssssssssssssssssssssssss ')
	print('             ssssssssssssssssssssssssssss ')
	print('              @@sssssssssssssssssssssss@ss ')
	print('              |s@@@@sssssssssssssss@@@@s|s ')
	print('       _______|sssss@@@@@sssss@@@@@sssss|s ')
	print('     /         sssssssss@sssss@sssssssss|s ')
	print('    /  .------+.ssssssss@sssss@ssssssss.| ')
	print('   /  /       |...sssssss@sss@sssssss...| ')
	print('  |  |        |.......sss@sss@ssss......| ')
	print('  |  |        |..........s@ss@sss.......| ')
	print('  |  |        |...........@ss@..........| ')
	print('   \  \       |............ss@..........| ')
	print('    \   ------+...........ss@...........| ')
	print('     \________ .........................| ')
	print('              |.........................| ')
	print('             /...........................\ ')
	print('            |.............................| ')
	print('               |.......................| ')
	print('                   |...............| ')
	print(' ')
	while count == 0: #while loop checks to continue
		answer = input("Would You Like to Run Another Calculation? 'yes' or 'no': ") #prompts user
		answer = answer.lower() #lower function used to adjust input
		if answer == "yes":
			num = num + 0 #continues the initial while loop, starts program over
			count = count + 1 #exits the while loop
			print(' ')
			clear = lambda: os.system('cls') #used to clear console for new calculations
			clear() #clears the console
		elif answer == "no":
			num = num + 1 #ends the while loop closing the program
			count = count + 1 #exits the while loop
		else:
			print(' ')
			print("ERROR: ***Please Enter 'yes' or 'no'***") #instructs user to enter correct values
			print(' ')
