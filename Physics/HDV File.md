# ISI HDV FILE DOCUMENTATION
## A lot of the work here is credited to the Race Sim Central User "Bristow". Thanks be to him and all other contributors 

Bristows Original Comments:

"The original is shown in regular text. My comments are in bold.

Nomenclature - I use the terms Range and Setting with the same meaning as shown in lines 5 and 6 of the file.  
The term Switch is used to refer to a parameter which is used to toggle between two states, usually whether a particular feature is switched on or off.  
A Multiplier is usually applied to another value or parameter by multiplying them together.  
A Factor may be used in some way to modify a parameter or behaviour defined elsewhere."

Top of File:

// BMW-Sauber F1.06 physics parameter file.  
// This is the high-detail vehicle parameter file.  
// It is pointed to by one or more *.veh files.  
// Any range has the following values: (minimum, step size, number of steps)  
// Any setting refers to the step from 0 to <number of steps - 1>.  

**The value which results is (minimum + step size x setting).** 

//The maximum value is [minimum + step size x (Number of steps - 1)]  
// Everything is in SI units (kg, m, kPa, N, etc.), except:  
// Engine speed is measured in RPM.  
// Angles are measured in degrees.  
//  
// +x = left
// +y = up
// +z = rear  
**In here are inserted three lines from the preamble to a standard pm file to show the positive direction for rotations -**  
**// +pitch = nose up**  
**// +yaw = nose right**  
**// +roll = right**  
**I infer these are viewed from the cockpit, looking forward.**

// Pushrod connections are adjusted from the values found in this file  
// based on the graphical location of the wheels. If the graphical location  
// does not match the physical location (found in a .pm file), then all  
// suspension joints (including the pushrods) are adjusted to match the  
// graphical locations. It should be noted that suspension joints are also  
// adjusted after setting the camber, caster, and toe-in.  
//  
// The "reference plane" is equal to the ride height. Note that we have  
// added a graphical offset because some series' measure the ride heights to the  
// frame of the car, but the bodywork hangs about an inch lower (especially  
// at the air dam). The graphical offset does not affect the physics in any  
// way, just the appearance of how far the vehicle is off the ground. Note  
// that the "undertray" points are where the vehicle bottoms out.  
//  
// Aerodynamic variables:  
// Lift is negative downforce


## [GENERAL]  
Rules=0 // What rules to apply to garage setups (0=none, 1=stock car)

GarageDisplayFlags=47 //How settings are displayed in garage (add): 1=rear downforce value (vs. angle), 2=radiator (vs. grille tape), 4=more gear info, 8+16=front downforce/wing/splitter/air dam, 32+64=rear downforce/wing/spoiler.  
**Flags which define the settings which show up in the garage display of car settings shown in the Garage. The values are chosen so they can be additive and the total then defines the flags which are set without ambiguity.**

**The Official '07 BMW HDV added another level to the flags -**  
**... 128=flip ups (vs. fender flare) and the flags are set to 175.**  
**The value for Flags may contain any or all of the numbers 1, 2, 4, 8, 16, 32, 64 and 128; once each. The total of up to 255 can then be decoded to show which values are present and so set the fashion in which some of the garage settings are shown.**  
**A Flags value of zero gives the following -**  
**On the General page you see this**  
**- The gearset display is simple**  
**- Under Engine you see Grille Tape and a percentage.**  
**- Under Aerodynamics you see Front Downforce showing the setting and Rear Downforce showing the angle.**  
**- On the Advanced page under Front you see Fender Flare.**

**Adding or removing 2 from the Flags total toggles the swap between Grill Tape and Radiator.**  
**Adding or removing 4 from the flags total toggles the swap between the simple and 'more detailed' gearset display.**  
**Adding or removing 128 from the flags total toggles the swap between Fender Flare and Flip Ups.**  
**The aero part is a bit more complicated - I show the component of the display which changes with each switch in Italics.**  
**- Adding 1 to the Flags total toggles the swap from Rear Downforce degrees to Rear Downforce setting.**  
**- Adding 8 to the Flags total toggles the swap from Front Downforce setting to Front Wing setting.**  
**- Adding 16 to the Flags total, when 8 is not present,toggles the swap from Front Downforce setting to Front Splitter setting.**  
**- Adding 16 to the Flags total, when 8 is present,toggles the swap from Front Downforce setting to Front AirDam setting.**  
**- Adding 32 to the Flags total toggles the swap from Rear Downforce degrees to Rear Wing degrees.**  
**- Adding 64 to the Flags total, when 32 is not present,toggles the swap from Rear Downforce degrees to Rear Spoiler degrees.**  
**- Adding 64 to the Flags total when 32 is present is not a supported combination. It returns the rear aero display to the default of Rear Downforce degrees.**

Mass=602.7 // All mass except fuel      
**Total mass of the car and driver, less fuel.**

**Fuel mass is a variable and is defined further down by tank capacity and fuel fill. Fuel load is then dynamically reduced by the rate of consumption.**

Inertia=(626.5, 732.0, 139.2) // All inertia except fuel  
**The moments of inertia for the whole car and driver around the X, Y and Z axes respectively. So these values are for, in turn, pitch, yaw and roll.**

Moment of inertia is the rotational analogue of mass. Please see http://en.wikipedia.org/wiki/Moment_of_inertia.

FuelTankPos=(0.00, 0.215,-1.47) // Location of tank relative to center of rear axle in reference plane  
FuelTankMotion=(560.0, 0.65) // Simple model of fuel movement in tank (spring rate per kg, critical damping ratio)  
**Self explanatory**

Notes=""  
Symmetric=1
**Sets the default for the car to symmetric (i.e. side to side) settings. Set to 0 to enable asymmetric values**

DamageFile=BMW_Damage // .ini file to find physical and graphical damage info
Calls the damage file. Must be in VEHDIR or TEAMDIR as defined in the .gen file.

CGHeight=0.176 // Height of body mass (excluding fuel) above reference plane  
**Defines the height of the Centre of Gravity (CoG) above the reference plane, which is the bottom of the body tub. Height of the CoG above the ground plane is CGHeight plus the Ride Height.**

CGRightRange=(0.480, 0.002, 21) // Fraction of weight on left tires  
CGRightSetting=10  
**Defines the value for the lateral position of the CoG by calculating the proportion on the Left Hand Side, using the standard ISI range and setting process. See the preamble for the range-setting method.**

CGRearRange=( 0.540, 0.002, 21) // Fraction of weight on rear tires  
CGRearSetting=10  
**Defines the value for the longitudinal position of the CoG by calculating the proportion of the weight on the rear axle. The CoG is then this fraction of the wheelbase behind the front axle line.**

WedgeRange=(0.0, 0.25, 1) // Rounds of wedge  
WedgeSetting=0  
WedgePushrod=0.0 // Each round of wedge changes rear-left jacking screw by this amount (0.0 to disable, use Rules to allow FR ride height)  
**This section enables and sets the amount of wedge. These lines are optional.**

GraphicalOffset=(0.0, 0.0, 0.0) // Does not affect physics! This just moves the vehicle body for whatever reasons you may have.  
**Enables the graphics for the body and associated parts like wings to be offset relative to the wheels. The most-used value is the vertical correction using the second parameter to move the appearance of the body up or down.**

Undertray00=( 0.20, 0.0, -1.00) // Corner offsets from center of wheels in reference plane
Undertray01=(-0.20, 0.0, -1.00)
Undertray02=( 0.20, 0.0, 1.30)
Undertray03=(-0.20, 0.0, 1.30)
Undertray04=( 0.58, 0.025,-0.50)
Undertray05=(-0.58, 0.025,-0.50)
Undertray06=( 0.58, 0.025, 0.80)
Undertray07=(-0.58, 0.025, 0.80)
Undertray08=( 0.58, 0.025, 0.0)
Undertray09=( 0.0, 0.0, 0.0)
Undertray10=(-0.58, 0.025, 0.0)
**Defines the extent of the undertray relative to the centre of the wheels, which is the mid-point between the axles along the centreline of the car at axle height. The X and Z values are defined. The Y value is calculated from the relative Z value and the front and rear ground clearance of the car at the time. There is an example in post #53 of this thread.**

**Undertray points 00 to 04 correspond to the earlier representation using FLUndertray, FRUndertray and so on, and follow the sequence FL, FR, RL and RR.**

UndertrayParams=(300000, 10000, 5.0) // Undertray spring rate, damper rate, and coefficient of friction
**Defines the behaviour of the undertray as a sprung and damped object. This statement is optional.**

TireBrand=BMW_Tires // Must appear before tire compound setting (references *.tbc file)
**Calls the tbc file for the car. It is good practise to name .tbc files with specific unambiguous names. The file will be searched for in the car folder, the Team folder and in other folders under Vehicles, probably on a First In basis.**

FrontTireCompoundSetting=3 // Compound index within brand
RearTireCompoundSetting=3 // Compound index within brand
**Defines the individual compound for the front and rear tyres. If they will always be the same as each other, these lines may be replaced by -**

**TireCompoundSetting=0 // compound index within brand**

FuelRange=(1.0, 1.0, 115)
FuelSetting=49
Fuel quantity per fill (litres)

NumPitstopsRange=(0, 1, 4)
NumPitstopsSetting=3
Pitstop1Range=(1.0, 1.0, 115)
Pitstop1Setting=49
Pitstop2Range=(1.0, 1.0, 115)
Pitstop2Setting=49
Pitstop3Range=(1.0, 1.0, 115)
Pitstop3Setting=49
Fuel range and settings for each pitstop. The maximum value for the third parameter is the tank capacity in litres.

There can be more than three pitstops. I have seen up to five.

AIAimSpeedsPerWP=(30.0, 54.0, 68.0, 82.0, 100.0, 120.0, 150.0, 185.0) // Speeds at which to look ahead X waypoints (spaced roughly 5 meters apart)
Enables management of the distance the AI looks ahead to manage braking and cornering. Fast cars with less grip, like early racing cars, can use higher values to help stay on the track.

AISlipReaction=(500.0, 30.0) // prediction factor for front wheel grip loss (higher numbers increase sensitivity), how quickly AI increase throttle after grip loss has occurred (higher numbers reduce "coasting")
AICornerReductionBase=165.0 // (pointspeed/this number)= % deceleration we can expect through a point
Fudge factors to enable tuning the AI

AIMinPassesPerTick=3 // Minimum passes per tick (can use more accurate spring/damper/torque values, but takes more CPU)
AIRotationThreshold=0.15 // Rotation threshold (rads/sec) to temporarily increment passes per tick
Enables tuning the CPU load associated with running the AI

AIEvenSuspension=0.0 // Averages out spring and damper rates to improve stability (0.0 - 1.0)
AISpringRate=1.0 // Spring rate adjustment for AI physics
AIDamperSlow=0.5 // Contribution of average slow damper into simple AI damper
AIDamperFast=0.5 // Contribution of average fast damper into simple AI damper
AIDownforceZArm=0.050 // Hard-coded center-of-pressure offset from vehicle CG
AIDownforceBias=0.0 // Bias between setup and hard-coded value (0.0-1.0)
AITorqueStab=(1.0, 1.0, 1.0) // Torque adjustment to keep AI stable
Fudge factors to enable tuning the AI

AIFuelMult=-1.0 // PLR file override for AI fuel usage - only positive value will override, see PLR for default
AIPerfUsage=(-1.0, -1.0, -1.0) // PLR file overrides for (brake power usage, brake grip usage, corner grip usage) used by AI to estimate performance - only positive values will override, see PLR for defaults
AITableParams=(-1.0, -1.0) // PLR file overrides for (max load, min radius) used when computing performance estimate tables - only positive values will override, see PLR for defaults
Enable the Player level AI defaults in the PLR file to be adjusted at the car level.

FeelerFlags=0 // How collision feelers are generated (add): 1=box influence 2=reduce wall-jumping 4=allow adjustment hack 8=top directions
Set of flags to define collision feeler actions

FeelerOffset=(0.0, 0.0, 0.0) // Offset from cg to use when generating feelers  
FeelersAtCGHeight=1 // Whether corner and side feelers are automatically adjusted to CG height  
FeelerFrontLeft=( 0.850,0.384,-1.950) // Front-left corner collision feeler  
FeelerFrontRight=(-0.850,0.384,-1.950) // Front-right corner collision feeler  
FeelerRearLeft=( 0.860,0.384,2.260) // Rear-left corner collision feeler  
FeelerRearRight=(-0.860,0.384,2.260) // Rear-right corner collision feeler  
FeelerFront=(0.0,0.384,-2.090) // Front side collision feeler  
FeelerRear=( 0.0,0.384, 2.420) // Rear side collision feeler  
FeelerRight=(-0.850,0.384,0.000) // Right side collision feeler  
FeelerLeft=( 0.850,0.384,0.000) // Left side collision feeler  
FeelerTopFrontLeft=(-0.1,1.010,0.720) // Top front-left collision feeler  
FeelerTopFrontRight=(0.1,1.010,0.720) // Top front-right collision feeler  
FeelerTopRearLeft=(-0.500,0.850,2.500) // Top rear-left collision feeler  
FeelerTopRearRight=(0.500,0.850,2.500) // Top rear-right collision feeler  
FeelerBottom=(0.000,0.080,-0.05) // Bottom feeler  
**Defines location of the virtual outside of the car, relative to the CoG, adjusted by the offset. Feelers are used to determine when the outside of the car touches another car or object, triggering some action defined by the damage file, described here.**

