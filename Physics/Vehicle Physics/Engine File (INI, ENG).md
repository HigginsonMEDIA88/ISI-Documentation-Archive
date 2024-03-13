# ISI ENGINE FILE DOCUMENTATION
A lot of the work here is credited to the Race Sim Central User "Bristow". Thanks be to him and all other contributors 
## Bristows Original Comments:
The rF engine.ini File

This thread is to record the contribution that the engine file makes to the definition of the cars in rFactor and to their behaviour.

In this thread is a posting at the top that contains an engine file from the original game - I have chosen the Sauber BMW released with version 1.150. Each line in the file is accompanied by the comments in the original. Lines are annotated with additional comments in bold about the purpose and role of the parameter, as the information becomes available. Due to the limits of my information, the data is incomplete and also probably wrong in places.

This thread is based on and updated from a similar thread I wrote for F1C. They may get a little out of synch from time to time. If there are contradictions, this thread will be more current.

Engine.ini files are text files and may be viewed and edited 
in any decent text editor or even Notepad.

Contributions are invited to help fill in the gaps.

## Begin File
// Maximum Torque: 316 NM @ 15500 RPM  
// Maximum Power: 723 horsepower @ 17500 RPM  
**"//" symbols are used to delimit comments in the original file and in other physics files. All characters after // and before the next Carriage Return are ignored by the game**

RPMTorque=( 0, -32.3, -32.3)  
RPMTorque=( 500, -32.1, -20.0)  
RPMTorque=( 1000, -33.4, 3.0)  
RPMTorque=( 1500, -35.2, 29.8)  
RPMTorque=( 2000, -37.2, 59.5)  
RPMTorque=( 2500, -39.1, 84.3)  
RPMTorque=( 3000, -40.9, 99.2)  
RPMTorque=( 3500, -42.8, 114.1)  
RPMTorque=( 4000, -44.7, 130.2)  
RPMTorque=( 4500, -46.6, 162.2)  
RPMTorque=( 5000, -48.6, 175.2)  
RPMTorque=( 5500, -50.7, 184.2)  
RPMTorque=( 6000, -52.8, 193.1)  
RPMTorque=( 6500, -55.0, 208.2)  
RPMTorque=( 7000, -57.2, 219.2)  
RPMTorque=( 7500, -59.4, 225.2)  
RPMTorque=( 8000, -61.7, 237.2)  
RPMTorque=( 8500, -63.9, 252.3)  
RPMTorque=( 9000, -66.2, 260.2)  
RPMTorque=( 9500, -68.5, 272.2)  
RPMTorque=(10000, -70.9, 278.3)  
RPMTorque=(10500, -73.4, 281.2)  
RPMTorque=(11000, -76.0, 287.3)  
RPMTorque=(11500, -78.9, 293.9)  
RPMTorque=(12000, -82.0, 296.4)  
RPMTorque=(12500, -85.4, 298.3)  
RPMTorque=(13000, -89.3, 301.3)  
RPMTorque=(13500, -93.6, 307.4)  
RPMTorque=(14000, -98.3, 310.3)  
RPMTorque=(14500, -103.4, 313.3)  
RPMTorque=(15000, -109.1, 315.3)  
RPMTorque=(15500, -114.9, 316.2)  
RPMTorque=(16000, -120.9, 310.3)  
RPMTorque=(16500, -127.0, 304.2)  
RPMTorque=(17000, -133.3, 301.3)  
RPMTorque=(17500, -139.6, 294.2)  
RPMTorque=(18000, -146.0, 281.2)  
RPMTorque=(18500, -152.7, 266.3)  
RPMTorque=(19000, -160.1, 243.2)  
RPMTorque=(19500, -168.8, 207.8)  
RPMTorque=(20000, -179.4, 157.7)  
RPMTorque=(20500, -192.8, 52.8)  
RPMTorque=(21000, -210.6, 0.0)  
RPMTorque=(21500, -233.8, -24.8)  
RPMTorque=(22000, -265.6, -87.3)  
RPMTorque=(22500, -309.4, -164.7)  
RPMTorque=(23000, -353.1, -275.8)  
**The table above defines the torque characteristics of the engine. On each line there is**
- **The rpm at which these values apply**
- **The maximum Back-torque, or drag, in Newton-metres from the engine at closed throttle**
- **The maximum Torque in Nm from the engine at full throttle. These torque values will be less (closer to zero) at part-throttle openings.**

**For the first line where RPM=0, values for engine torque which are less than brake torque will cause an error report in the log file trace.txt. The error is not fatal.**

**Horsepower developed may be calculated from these numbers. Imperial horsepower as commonly used in the US (33,000 ft-lb/min) is (RPM * torque / 7121). Please note there are a variety of horsepowers with differing sizes, among them the metric PS which is slightly smaller than the Imperial. Please see references here and here.**

FuelConsumption=3.110e-005 // affected by throttle position and engine speed  
**A factor which defines fule consumption, not further documented by ISI.**

**Thanks to Carham for wanting to understand and then Kangaloosh and Kalma for exposing the facts -**

**This factor has the units of litres/radian. The "FuelConsumption=" rate is multiplied by filtered throttle position (to take account of Traction Control and other interventions) and engine speed in radians/sec to deplete the fuel mass remaining in the tank. The answer is in litres/sec. Filtered throttle values are within range 0-1.0.**

**Some rough numbers using F1 as a basis-**

**At 15,000 rpm and 66% throttle for 1hr 40min:**  
**15,000 rpm is ~1571 rads/sec**  
**1571 * 0.66 * 3.11x10^-5 * 100 x 60 is ~193 (litres/sec)**

FuelEstimate=1.745 // fudge factor for differences between vehicle types (used for lap estimates and AI pit scheduling)  
**Even less documentation than above.**

EngineInertia=0.0518 // rotational inertia of engine components  
**Defines the inertia of the engine so that it can be used as part of the calculations for net torque available to the wheels for acceleration. For modelling engine sizes and types (and maybe from time periods) for which we have no examples, the values in the files supplied by ISI could be amended according to capacity, engine type (road car, sports car etc) and age to provide values for other engine types.**

IdleThrottle=1.0 // throttle multiplier to help maintain idle speed  
**? Maybe used with a manual transmission with clutch to assist with not stalling the engine. Not applicable to F1. Note also that engine torque at idle speed must be greater than ClutchFriction in the hdv to prevent stalling.**

IdleRPMLogic=(3925.0, 4150.0) // attempt to maintain idle speed between these RPMs  
**Defines the idle speed aim range, in rpm. Affects the pitch of the idle sound - faster is higher.**

LaunchEfficiency=0.993 // efficiency (0.0-1.0) of launch control, or 0.0 if N/A  
LaunchRPMLogic=(7800.0, 11000.0) // holds RPM in this range before launch (used for AI even if launch control is N/A!)  
LaunchVariables=3 // level of traction control used (0-3) and whether auto-upshifting is enabled (add 4); default=7  
**This section defines the values used to manage launch control for the player car, if enabled, and for the AI at all times. Note that F1 cars do not use auto-upshift, so the default LaunchVariables flag of 7 does not apply to this car.**

**The LaunchVariables line is optional.**

RevLimitRange=(18000.0, 50.0, 21)  
RevLimitSetting=15  
**Defines the rpm at which the rev limiter cuts in and the aim point for max revs for auto-upshifting.**

**This is a typical set of ISI Range and Setting lines. The first line has three values - the first is the base or start value of the range, the second is the size of the increase for each step of the range and the third is the number of steps. The settings start from zero and go to 20, which is the 21st value, so the RevLimit can be set to any of 21 values from 18000 to (18000 + 20 x 50) or 19000 in 50 rpm increments.**