# ISI HDV FILE DOCUMENTATION
A lot of the work here is credited to the Race Sim Central User "Bristow". Thanks be to him and all other contributors 

## Bristows Original Comments:

"The original is shown in regular text. My comments are in **bold**."

>"Nomenclature - I use the terms Range and Setting with the same meaning as shown in lines 5 and 6 of the file.  
The term Switch is used to refer to a parameter which is used to toggle between two states, usually whether a particular feature is switched on or off.  
A Multiplier is usually applied to another value or parameter by multiplying them together.  
A Factor may be used in some way to modify a parameter or behaviour defined elsewhere."

# HDV CODE

// BMW-Sauber F1.06 physics parameter file.  
// This is the high-detail vehicle parameter file.  
// It is pointed to by one or more *.veh files.  
// Any range has the following values: (minimum, step size, number of steps)  
// Any setting refers to the step from 0 to <number of steps - 1>.  

***The value which results is (minimum + step size x setting).*** 

//The maximum value is [minimum + step size x (Number of steps - 1)]  
// Everything is in SI units (kg, m, kPa, N, etc.), except:  
// Engine speed is measured in RPM.  
// Angles are measured in degrees.  
//  
// +x = left
// +y = up
// +z = rear  
***In here are inserted three lines from the preamble to a standard pm file to show the positive direction for rotations -***  
***// +pitch = nose up***  
***// +yaw = nose right***  
***// +roll = right***  
***I infer these are viewed from the cockpit, looking forward.***

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


### [GENERAL]  
Rules=0 // What rules to apply to garage setups (0=none, 1=stock car)

GarageDisplayFlags=47 //How settings are displayed in garage (add): 1=rear downforce value (vs. angle), 2=radiator (vs. grille tape), 4=more gear info, 8+16=front downforce/wing/splitter/air dam, 32+64=rear downforce/wing/spoiler.  
***Flags which define the settings which show up in the garage display of car settings shown in the Garage. The values are chosen so they can be additive and the total then defines the flags which are set without ambiguity.***

***The Official '07 BMW HDV added another level to the flags -***  
***... 128=flip ups (vs. fender flare) and the flags are set to 175.***  
***The value for Flags may contain any or all of the numbers 1, 2, 4, 8, 16, 32, 64 and 128; once each. The total of up to 255 can then be decoded to show which values are present and so set the fashion in which some of the garage settings are shown.***  
***A Flags value of zero gives the following -***  
***On the General page you see this***  
***- The gearset display is simple***  
***- Under Engine you see Grille Tape and a percentage.***  
***- Under Aerodynamics you see Front Downforce showing the setting and Rear Downforce showing the angle.***  
***- On the Advanced page under Front you see Fender Flare.***

***Adding or removing 2 from the Flags total toggles the swap between Grill Tape and Radiator.***  
***Adding or removing 4 from the flags total toggles the swap between the simple and 'more detailed' gearset display.***  
***Adding or removing 128 from the flags total toggles the swap between Fender Flare and Flip Ups.***  
***The aero part is a bit more complicated - I show the component of the display which changes with each switch in Italics.***  
***- Adding 1 to the Flags total toggles the swap from Rear Downforce degrees to Rear Downforce setting.***  
***- Adding 8 to the Flags total toggles the swap from Front Downforce setting to Front Wing setting.***  
***- Adding 16 to the Flags total, when 8 is not present,toggles the swap from Front Downforce setting to Front Splitter setting.***  
***- Adding 16 to the Flags total, when 8 is present,toggles the swap from Front Downforce setting to Front AirDam setting.***  
***- Adding 32 to the Flags total toggles the swap from Rear Downforce degrees to Rear Wing degrees.***  
***- Adding 64 to the Flags total, when 32 is not present,toggles the swap from Rear Downforce degrees to Rear Spoiler degrees.***  
***- Adding 64 to the Flags total when 32 is present is not a supported combination. It returns the rear aero display to the default of Rear Downforce degrees.***

Mass=602.7 // All mass except fuel      
***Total mass of the car and driver, less fuel.***

***Fuel mass is a variable and is defined further down by tank capacity and fuel fill. Fuel load is then dynamically reduced by the rate of consumption.***

Inertia=(626.5, 732.0, 139.2) // All inertia except fuel  
***The moments of inertia for the whole car and driver around the X, Y and Z axes respectively. So these values are for, in turn, pitch, yaw and roll.***

Moment of inertia is the rotational analogue of mass. Please see http://en.wikipedia.org/wiki/Moment_of_inertia.

FuelTankPos=(0.00, 0.215,-1.47) // Location of tank relative to center of rear axle in reference plane  
FuelTankMotion=(560.0, 0.65) // Simple model of fuel movement in tank (spring rate per kg, critical damping ratio)  
***Self explanatory***

Notes=""  
Symmetric=1
***Sets the default for the car to symmetric (i.e. side to side) settings. Set to 0 to enable asymmetric values***

DamageFile=BMW_Damage // .ini file to find physical and graphical damage info
Calls the damage file. Must be in VEHDIR or TEAMDIR as defined in the .gen file.

CGHeight=0.176 // Height of body mass (excluding fuel) above reference plane  
***Defines the height of the Centre of Gravity (CoG) above the reference plane, which is the bottom of the body tub. Height of the CoG above the ground plane is CGHeight plus the Ride Height.***

CGRightRange=(0.480, 0.002, 21) // Fraction of weight on left tires  
CGRightSetting=10  
***Defines the value for the lateral position of the CoG by calculating the proportion on the Left Hand Side, using the standard ISI range and setting process. See the preamble for the range-setting method.***

CGRearRange=( 0.540, 0.002, 21) // Fraction of weight on rear tires  
CGRearSetting=10  
***Defines the value for the longitudinal position of the CoG by calculating the proportion of the weight on the rear axle. The CoG is then this fraction of the wheelbase behind the front axle line.***

WedgeRange=(0.0, 0.25, 1) // Rounds of wedge  
WedgeSetting=0  
WedgePushrod=0.0 // Each round of wedge changes rear-left jacking screw by this amount (0.0 to disable, use Rules to allow FR ride height)  
***This section enables and sets the amount of wedge. These lines are optional.***

GraphicalOffset=(0.0, 0.0, 0.0) // Does not affect physics! This just moves the vehicle body for whatever reasons you may have.  
***Enables the graphics for the body and associated parts like wings to be offset relative to the wheels. The most-used value is the vertical correction using the second parameter to move the appearance of the body up or down.***

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
***Defines the extent of the undertray relative to the centre of the wheels, which is the mid-point between the axles along the centreline of the car at axle height. The X and Z values are defined. The Y value is calculated from the relative Z value and the front and rear ground clearance of the car at the time. There is an example in post #53 of this thread.***

***Undertray points 00 to 04 correspond to the earlier representation using FLUndertray, FRUndertray and so on, and follow the sequence FL, FR, RL and RR.***

UndertrayParams=(300000, 10000, 5.0) // Undertray spring rate, damper rate, and coefficient of friction
***Defines the behaviour of the undertray as a sprung and damped object. This statement is optional.***

TireBrand=BMW_Tires // Must appear before tire compound setting (references *.tbc file)
***Calls the tbc file for the car. It is good practise to name .tbc files with specific unambiguous names. The file will be searched for in the car folder, the Team folder and in other folders under Vehicles, probably on a First In basis.***

FrontTireCompoundSetting=3 // Compound index within brand
RearTireCompoundSetting=3 // Compound index within brand
***Defines the individual compound for the front and rear tyres. If they will always be the same as each other, these lines may be replaced by -***

***TireCompoundSetting=0 // compound index within brand***

FuelRange=(1.0, 1.0, 115)  
FuelSetting=49  
***Fuel quantity per fill (litres)***

NumPitstopsRange=(0, 1, 4)  
NumPitstopsSetting=3  
Pitstop1Range=(1.0, 1.0, 115)  
Pitstop1Setting=49  
Pitstop2Range=(1.0, 1.0, 115)  
Pitstop2Setting=49  
Pitstop3Range=(1.0, 1.0, 115)  
Pitstop3Setting=49  
***Fuel range and settings for each pitstop. The maximum value for the third parameter is the tank capacity in litres.***

***There can be more than three pitstops. I have seen up to five.***

AIAimSpeedsPerWP=(30.0, 54.0, 68.0, 82.0, 100.0, 120.0, 150.0, 185.0) // Speeds at which to look ahead X waypoints (spaced roughly 5 meters apart).  
***Enables management of the distance the AI looks ahead to manage braking and cornering. Fast cars with less grip, like early racing cars, can use higher values to help stay on the track.***

AISlipReaction=(500.0, 30.0)  // prediction factor for front wheel grip loss (higher numbers increase sensitivity), how quickly AI increase throttle after grip loss has occurred (higher numbers reduce "coasting")
AICornerReductionBase=165.0 // (pointspeed/this number)= % deceleration we can expect through a point
***Fudge factors to enable tuning the AI***

AIMinPassesPerTick=3 // Minimum passes per tick (can use more accurate spring/damper/torque values, but takes more CPU)
AIRotationThreshold=0.15 // Rotation threshold (rads/sec) to temporarily increment passes per tick
***Enables tuning the CPU load associated with running the AI***

AIEvenSuspension=0.0 // Averages out spring and damper rates to improve stability (0.0 - 1.0)  
AISpringRate=1.0 // Spring rate adjustment for AI physics  
AIDamperSlow=0.5 // Contribution of average slow damper into simple AI damper  
AIDamperFast=0.5 // Contribution of average fast damper into simple AI damper  
AIDownforceZArm=0.050 // Hard-coded center-of-pressure offset from vehicle CG  
AIDownforceBias=0.0 // Bias between setup and hard-coded value (0.0-1.0)  
AITorqueStab=(1.0, 1.0, 1.0) // Torque adjustment to keep AI stable  
***Fudge factors to enable tuning the AI***

AIFuelMult=-1.0 // PLR file override for AI fuel usage - only positive value will override, see PLR for default  
AIPerfUsage=(-1.0, -1.0, -1.0) // PLR file overrides for (brake power usage, brake grip usage, corner grip usage) used by AI to estimate performance - only positive values will override, see PLR for defaults  
AITableParams=(-1.0, -1.0) // PLR file overrides for (max load, min radius) used when computing performance estimate tables - only positive values will override, see PLR for defaults  
***Enable the Player level AI defaults in the PLR file to be adjusted at the car level.***

FeelerFlags=0 // How collision feelers are generated (add): 1=box influence 2=reduce wall-jumping 4=allow adjustment hack 8=top directions  
***Set of flags to define collision feeler actions***

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
***Defines location of the virtual outside of the car, relative to the CoG, adjusted by the offset. Feelers are used to determine when the outside of the car touches another car or object, triggering some action defined by the damage file, described here.***

### [PITMENU]

***This section seems fairly well documented as it is***

***This section is optional***

StopGo=1 // Whether stop/go pit menu item is available (highly recommended); default=1  

Fuel=1 // Whether fuel pit menu item is available (recommended); default=1  

AllTires=1 // Option for changing all tires (all other tire choices should be 0); default=0  

FrontRearTires=(0,0) // Option for changing front tires, rear tires (all other conflicting tire choices should be 0); default=(1,1)  

LeftRightTires=(0,0) // Option for changing left tires, right tires (all other conflicting tire choices should be 0); default=(0,0)  

IndividualTires=(0,0,0,0) // Option for changing individual tire FL, FR, RL, RR (all other conflicting tire choices should be 0); default=(0,0,0,0)  

FenderFlare=(0,0) // Options for changing left fender flare, right fender flare; default=(0,0)  

FrontWing=1 // Front wing adjustment (front wing repair is covered under Damage); default=1  

RearWing=0 // Rear wing adjustment (rear wing repair is covered under Damage); default=0  

Driver=0 // Driver change; default=1  

Wedge=0 // Wedge adjustment; default=0  

Radiator=0 // Radiator or grille tape adjustment; default=0  

TrackBar=0 // Track bar adjustment; default=0  

Pressure=(1,1,1,1) // Tire pressure adjustment FL, FR, RL, RR; default=(0,0,0,0)  

SpringRubber=(0,0,0,0) // Spring rubber adjustment FL, FR, RL, RR; default=(0,0,0,0)  

Damage=2 // Number of options to fix damage (0=none, 1=bodywork, 2=bodywork+suspension); default=1  

StopGoSimultaneous=0 // Whether stop/go penalties can be served during a regular pit stop (time is added at end); default=0  

PressureOnTheFly=0 // Whether tire pressures can be adjusted WITHOUT changing tires; default=0  

DamagedTiresOnly=0 // Tire change restrictions: 0=any tire can be changed 1=only damaged tires can be changed; default=0  

CompoundRestrictions=3 // Whether tire compounds have restrictions: 0=unrestricted 1=one dry compound from qualifying on, 2=front/rear compounds must match, 3=both; default=0  

Preparation=(150.0,24.0,0.5,4.5) // When crew gives up after request, crew prep time, delay multiplier for how much more time was needed to prep, max delay; default=(150.0,25.0,0.5,4.5)  

FuelTime=(12.0,2.0,1.0,0.5,1.0) // Fuel fill rate (L/s), random delay, nozzle insertion time, nozzle removal time, concurrent fuel filling (0.0=separate, 1.0=concurrent); default=(12.0,2.0,1.0,0.5,1.0)  

TireTime=(5.5,5.5,2.5,1.0) // Time to change two tires, time to change four tires, random delay on any tire, concurrent tire changes (0.0=separate, 1.0=concurrent); default=(5.5,5.5,2.0,1.0)  

FenderFlareTime=0.0 // Time to adjust fender flare; default=3.5  

FrontWingTime=(8.0,11.0) // Time to adjust front wing, time to replace front wing; default=(8.0,8.0)  

RearWingTime=(12.0,33.0) // Time to adjust rear wing, time to replace rear wing; default=(8.0,33.0)  

DriverTime=(20.0,1.5,4.0,1.0) // Time to change driver, random delay, extra delay if vehicle is damaged, concurrent driver changes (0.0=separate, 1.0=concurrent); default=(11.0,1.5,4.0,1.0)  

WedgeTime=0.0 // Time to adjust wedge; default=3.5  

RadiatorTime=0.0 // Time to adjust radiator/grille tape; default=5.0  

TrackBarTime=0.0 // Time to adjust track bar; default=3.5  

PressureTime=2.5 // Time to adjust tire pressure WITHOUT changing tire; default=2.5  

SpringRubberTime=3.0 // Time to adjust spring rubber; default=3.0  

DamageTime=(12.5,4.0,720.0,1.0) // Time to fix aero damage, random delay, fix suspension including broken off wheels, concurrent damage fixing (0.0=separate, 1.0=concurrent); default=(8.5,1.0,90.0,1.0)

### [AIDPENALTIES]
***Also seems quite clearly documented.***  
***This section is optional.***

TC=(0.00,0.00,0.00) // Weight penalties for using different  
ABS=(0.000,0.005,0.010) // levels of aids. First value is typically  
Stability=(0.000,0.005,0.010) // with the aid off so it should be 0.0.  
Autoshift=(0.00,0.00,0.00,0.00) // Penalties should only be applied to  
Steering=(0.000,0.005,0.008,0.020) // aids that the vehicle would not be  
Braking=(0.00,0.00,0.00) // allowed to run with. Penalties should  
Invulnerable=(0.00,0.00) // typically only be used if the aid improves  
Opposite=(0.00,0.00) // laptimes for a decent driver.  
SpinRecovery=(0.00,0.00) // Values are fractions of the total vehicle  
AutoPit=(0.00,0.00) // mass, and are modeled as extra weight in  
AutoLift=(0.00,0.00) // the fuel tank. Do not use negative values.  
AutoBlip=(0.00,0.00)

## AERODYNAMICS

This deals with the parts of the car which develop aerodynamic lift and drag. The total drag for the car is the aggregate of the drag calculated in this section plus any additional amounts assumed in the underlying physics. Lift works the same way. This section also defines where those forces act upon the car.

The main aerodynamic objects which may be defined are the front and rear wings, the fenders, the body, the radiator, the brake ducts and the diffuser. Each has a location through which their forces act. The aggregation of forces these act through the centre of pressure for the car. The relationship between the centre of pressure and the centre of gravity and the centres of correcting forces from tyres (sideways) and the tyres and springs which hold the car up are all very important in determining stability while moving.

In particular, if the centre of pressure is in front of the centre of lateral resistance, the car will tend to become unstable at speed (wandering and so on) as the centre of lateral pressure tries to get behind the centre of lateral resistance. This is why arrows and aircraft have stabilizer fins at the back.

ISI have disclosed a number of available statements in the Aero section which enabled the management of the effects of drafting. This included a set of statements which can override the drafting section found in the rfm files for a number of mods. The HDV is a more appropriate place for these control statements. edits made to include these statements in there proper place.

The parameters which enable the management of drafting effects look to be arbitrary factors which are changed to modify the effect. The very limited documentation suggests that they are arbitrary and not well-linked to actual physics values.

The original is shown in regular text. Bristows comments are in ***bold***.


## [FRONTWING]
***The [FRONTWING] and [REARWING] sections define the forces which are associated with the aerodynamic forces from the front and rear of the car. They are separate from the fenders, body and diffuser sections.***

***There is a connection between these sections and any [FWING] and [RWING] instances in the gen file. By default [FWING] and [RWING] are defined as objects that may become detached by a collision. In the event that happens, the aero effects of the detached objects are also lost. So a car which loses it's front wing in a collision also loses the aero benefit of the lost wing.***

***This section is optional. If the car has no front wing the entire section may be deleted***

FWRange=(0.0, 1.0, 40) // Front wing range  
FWSetting=29 // Front wing setting  

***Defines FrontWing range and setting. FWSetting is also used to index into other settings below as well as FWRange - for example FWLiftParams.***

***For cars with no wing, set FWSetting to zero if you want to be able to adjust later in the garage, or remove the section completely to disable them.***

***In Real Life, Lift and drag are proportional to the density of the air (kg/m^3), the area of the object (sq metres), the Coefficient (of lift or drag respectively) and the square of the velocity (m/sec).***

>Lift= 0.5 x dens x area x CoL x vel^2

***rF reduces this calculation to a simplified form by providing lift and drag factors. Lift and drag forces are calculated by using the formula:***

>Lift or drag (Newtons) = rF_Factor x vel^2 (velocity in m/sec)

FWMaxHeight=(0.30) // Maximum height to take account of for downforce  
**No height-related changes in aero from the front wing when it is located above this height.**

FWDragParams=(0.0190, 0.00322, 0.000016) // Base drag and 1st and 2nd order with setting  
>rF_Factor for Drag from Front Wing = FWDP_1 + (FWDP_2 x FWSetting) + (FWDP_3 x FWSetting^2) for travel straight ahead.

FWLiftParams=(-0.240,-0.0119, 0.000027) // Base lift and 1st and 2nd order with setting  
>rF_Factor for Lift = FWLP_1 +( FWLP_2 x FWSetting ) + (FWLP_3 x FWSetting ^2) for travel straight ahead.

**That is -0.5986 for this car. Being negative, this provides downforce.**

FWLiftHeight=(0.930) // Effect of current height on lift coefficient
**Reduction in downforce for the front wing due to front ride-height, in lift-factor units per metre. So**  
>rF_Factor for Lift(actual) = rF_Factor for Lift(Calculated) + FWLiftHeight x Front_RideHeight

**This is a dynamic parameter, so it varies with actual rideheight.**

FWDraftLiftMult=4.95 // Effect of draft on front wing's lift response (larger numbers will tend to decrease downforce when in the draft)  
**A factor to change the lift of the Front Wing when drafting. Default is 1.0.**

FWLiftSideways=(0.335) // Dropoff in downforce with yaw (0.0 = none, 1.0 = max)  
**? Proportion of downforce lost when the car gets sideways. How far sideways is not documented.**

FWLiftPeakYaw=(0.0, 1.0) // Angle of peak, multiplier at peak  
**Defines the yaw angle at which the front wing force is at its highest. First value is the horizontal angle to the centre line of the car at which the forces peak. The second is a multiplier to apply at that angle.**

FWLeft=(-0.05, 0.0, 0.0) // Aero forces from moving left  
FWRight=(0.05, 0.0, 0.0) // Aero forces from moving right  
**Force (Newtons) to the Left or Right resulting from linear translation in m/sec (as distinct from rotation) to the left or right. The numbers in the bracket are the forces in the X, Y and Z directions and you can see that FWLeft produces 0.05 N/(m/s) to the right as it is negative. This tends to stabilise the car a bit. Similarly to the right.**

FWUp=( 0.0,-0.168, 0.020) // Aero forces from moving up  
FWDown=(0.0, 0.168,-0.012) // Aero forces from moving down  
**Change in forces from translation up or down. Works like FWLeft and FWRight. FWUp has forces down and reawards.**

FWAft=( 0.0, 0.045,-0.04) // Aero forces from moving rearwards  
**Forces from moving rearwards**

FWFore=(0.0, 0.0, 0.0) // Aero forces from moving forwards (recomputed from settings)  
**Change in forces from translation up or down.**

FWRot=(0.15, 0.06, 0.22) // Aero torque from rotating  
**Torque (Nm) from rotating around the X, Y or Z axis. Per degree of rotation?**

FWCenter=(0.00, 0.11, -0.50) // Center of front wing forces (offset from center of front axle in ref plane)  
**Position of the centre of action of front wing forces relative to the centre of the front axle and at the bottom of the body tub, aka at ride height.**

## [LEFTFENDER]
**// Not applicable to open-wheelers**  
**Fender parameters are analogous to the front wing settings in the way they are applied.**

**This section is optional, or it may be commented out like this one. Maybe it is here in the BMW hdv file as an example?**

**The 2007 version of this section in the BMW F1.07.hdv had a different comment -**  
// Not applicable to open-wheelers **is replaced by** // Used to simulate flick-up's  
//FenderFlareRange=(0.0, 0.00635, 1) // Front fender flare  
//FenderFlareSetting=0  
//FenderCenter=(0.80, 0.28, -0.38) // Center of fender forces (offset from center of front axle in ref plane)  
//FenderDragParams=(0.0, 0.2965, 0.0) // Base, 1st, and 2nd order drag per meter flare  
//FenderLiftParams=(0.0,-1.0306, 3.782) // Base, 1st, and 2nd order lift per meter flare  
//FenderDraftLiftMult= 1.15 // Effect of draft on fender's lift response  
//FenderSideways=(0.1) // Dropoff in downforce with yaw (0.0 = none, 1.0 = max)  
//FenderPeakYaw=(3.0, 1.02) // Angle of peak, multiplier at peak  

## [RIGHTFENDER]  
//FenderFlareRange=(0.0, 0.00635, 1) // Front fender flare  
//FenderFlareSetting=0  
//FenderCenter=(-0.80, 0.28, -0.38) // Center of fender forces (offset from center of front axle in ref plane)  
//FenderDragParams=(0.0, 0.2965, 0.0) // Base, 1st, and 2nd order drag per meter flare  
//FenderLiftParams=(0.0,-1.0306, 3.782) // Base, 1st, and 2nd order lift per meter flare  
//FenderDraftLiftMult= 1.15 // Effect of draft on fender's lift response  
//FenderSideways=(0.1) // Dropoff in downforce with yaw (0.0 = none, 1.0 = max)  
//FenderPeakYaw=(3.0, 1.02) // Angle of peak, multiplier at peak  

## [REARWING]  
**Rear wing parameters are analogous to the front wing settings in the way they are applied. This section is optional or may be commented out.**

RWRange=(0.0, 1.0, 40) // Rear wing range  
RWSetting=29 // Rear wing setting  
RWDragParams=( 0.045, 0.00547, 0.000023) // Base drag and 1st and 2nd order with setting  
RWLiftParams=(-0.242,-0.01445, 0.000065) // Base lift and 1st and 2nd order with setting  
RWDraftLiftMult=1.25 // Effect of draft on rear wing's lift response  
RWLiftSideways=(0.325) // Dropoff in downforce with yaw (0.0 = none, 1.0 = max)  
RWLiftPeakYaw=(0.0, 1.0) // Angle of peak, multiplier at peak  
RWLeft=(-0.10, 0.0, 0.0) // Aero forces from moving left  
RWRight=(0.10, 0.0, 0.0) // Aero forces from moving right  
RWUp=( 0.0,-0.192, 0.050) // Aero forces from moving up  
RWDown=(0.0, 0.192,-0.030) // Aero forces from moving down  
RWAft=( 0.0, 0.10, -0.10) // Aero forces from moving rearwards  
RWFore=(0.0, 0.0, 0.0) // Aero forces from moving forwards (recomputed from settings)  
RWRot=( 0.20, 0.18, 0.30) // Aero torque from rotating  
RWCenter=(0.00, 0.62, 0.35) // Center of rear wing forces (offset from center of rear axle at ref plane)  

## [BODYAERO]
BodyDragBase=(0.3555) // Base drag  
BodyDragHeightAvg=(0.345) // Drag increase with average ride height  
BodyDragHeightDiff=(0.878) // Drag increase with front/rear ride height difference  
BodyMaxHeight=(0.22) // Maximum ride height that affects drag/lift  
**Drag from the body is calculated as three parts. BodyDragBase is constant. BodyDragHeightAvg is that portion of the drag which is dependant on average ride height in metres. BodyDragHeightDiff is that portion which is dependant on the (absolute value of) ride height difference, also in metres. All calculations are performed on actual on-track values, not unloaded or stationary in the pits.**

**All calculations are limited by BodyMaxHeight. Total Drag Factor is the sum of all three BodyDrags.**

**For this car, when RideHt_F and RideHt_R are <= 0.22m, Total Drag = (0.3555 + 0.345(RideHt_F + RideHt_R)/2 + 0.878 x ABS(RideHt_F - RideHt_R)) x speed^2 Newtons.**

DraftBalanceMult=0.75 // Effect of draft on aerodynamic downforce balance of car (bigger numbers exaggerate the effect)  
BodyDraftLiftMult=2.00 // Effect of draft on body's lift response  
**These lines are optional.**

**Two factors for managing the effect of drafting on the body.**

**DraftBalanceMult was functionally equivalent to 0.0 in builds prior to 1.250, meaning that the draft was calculated once for each vehicle and affected all aerodynamic components equally. Now the draft is calculated at the front and rear of the vehicle, and components are affected based on their location in the draft. This multiplier allows you to exaggerate or remove the effect.**
<br>

**All the following parameters starting with Body... are analogous to the front wing settings in the way they are applied.**  
BodyLeft=(-0.70, 0.03, 0.0) // Aero forces from moving left  
BodyRight=(0.70, 0.03, 0.0) // Aero forces from moving right  
BodyUp=( 0.0,-1.7, 0.0) // Aero forces from moving up  
BodyDown=( 0.0, 1.7, 0.0) // Aero forces from moving down  
BodyAft=( 0.0, 0.105,-0.95) // Aero forces from moving rearwards  
BodyFore=( 0.0,-0.171, 0.370) // Aero forces from moving forwards (lift value important, but drag overwritten)  
**The Z (drag ) value is overwridden by the use of total BodyDrag calculated as shown at the top of the section.**

BodyRot=(4.1, 2.7, 1.9) // Aero torque from rotating  
BodyCenter=(0.0, 0.254,-1.392) // Center of body aero forces (offset from center of rear axle at ref plane)

RadiatorRange=(0.0, 1.0, 7) // Radiator range (front grille tape)  
RadiatorSetting=3 // Radiator setting  
RadiatorDrag=(0.0022) // Effect of radiator setting on drag  
**Contributes to the overall drag by a coefficient value of RadiatorDrag x RadiatorSetting**

RadiatorLift=(0.0048) // Effect of radiator setting on lift  
**Contributes to the overall lift by a coefficient value of RadiatorLift x RadiatorSetting**

BrakeDuctRange=(0.0, 1.0, 7) // Brake duct range  
BrakeDuctSetting=3 // Brake duct setting  
BrakeDuctDrag=(0.00315) // Effect of brake duct setting on drag  
BrakeDuctLift=(0.00686) // Effect of brake duct setting on lift  
**Brake duct drag and lift contributions to lift and drag work like the Radiator contributions. Brake duct lines are optional.**

BaseDropoff=0.140 // RFM Drafting override: Higher number -> more drafting effect (default=0.185)  
LeadingExponent=80.00 // RFM Drafting override: Higher number -> lower effect on leader (default=2.0)  
FollowingExponent=1.75 // RFM Drafting override: Higher number -> lower effect on followers (default=2.0)  
VehicleWidth=2.10 // RFM Drafting override: Helps determine base width of wake (default=1.9)  
SideEffect=0.35 // RFM Drafting override: Negative effects of side-by-side drafting (default=0.35, used to be ~3.0 which was way too strong!)  
SideLeadingExponent=2.0 // RFM Drafting override: Added to regular LeadingExponent to affect the side wake  
SideFollowingExponent=3.5 // RFM Drafting override: Added to regular FollowingExponent to affect the side wake  
**These lines are optional.**

**A set of factors which define values which will provide management of drafting effects on the body. This set of statements override statements that are optional in the rfm file and may be used for the same purpose.**

## [DIFFUSER]
**The diffuser section is used to define the parameters for modelling the effects of under-body aerodynamic features of the car, if it has any. Although expressed in terms of a diffuser, which is one or more under-car tunnels with exit venturis at the rear of the car, the section can handle other configurations such as various shapes under the car, skirts of various types and so on. The areas for which the most imagination will be required are for those configurations which produce significant non-linear responses.**

**The section is optional and can be removed for those cars with no significant under-body aero. If you choose to include a Diffuser section, not all line are required.**

**The diffuser is formed by the undertray and so the values for X and Z and the calculated values for Y from the first four Undertray points 00 to 03 define the location of the FL, FR, RL and RR corners. This is found in the [GENERAL] section dealt with in post #2. See post #53 as well.**

DiffuserBase=(-1.045, 2.15, 85.0) // Base lift and 1st/2nd order with rear ride height  
DiffuserFrontHeight=(1.450) // 1st order with front ride height  
**Defines the diffuser lift just like the Front Wing, with the first and second order contributions responding to rear ride height and first order contribution from the front ride height.**  
>CoL = DiffuserBase_1 + DiffuserBase_2 x Rear_RideHeight + DiffuserBase_3 x Rear_RideHeight^2 + DiffuserFrontHeight x Front_RideHeight

DiffuserRake=(-0.003, -20, 450.0) // Optimum rake (rear - front ride height), 1st order with current difference from opt, 2nd order  
**This line is optional within the section.**

**Defines the effect of the difference in ride height front to rear. First value is the optimum difference - slightly nose-down. The second parameter is the 1st order coefficient contribution - multiply it by the deviation from optimum. The third parameter is the second order contribution to the coefficient - multiply it by the deviation squared.**

DiffuserLimits=(0.013, 0.105, 0.044) // Min ride height before stalling begins (0.0=disabled), max rear ride height for computations, max rake difference for computations  
**Defines the limits for the diffuser calculations. At ride heights below the stall boundary, the effect is reduced. As ride height increases or rake increases beyond the optimum, the diffuser effect is reduced.**

DiffuserStall=(0.1, 0.60) // Function to compute stall ride height (0.0=minimum, 1.0=average), downforce lost when bottoming out (0.0=none, 1.0=complete stall)  
**This line is optional within the section.**

**Factors which are applied to two somewhat related functions. The first is the (rear?) ride height at which the diffuser stalls. The second is to define the proportional reduction in downforce from the car bottoming out, from zero to 100% loss.**

DiffuserDraftLiftMult=1.40 // Effect of draft on diffuser's lift response  
**This line is optional within the section.**

**Multiplier-type factor for the effect of draft on the lift response. Bigger provides more effect.**

DiffuserSideways=(0.332) // Dropoff with yaw (0.0 = none, 1.0 = max)  
**? Proportion of downforce lost when the car gets sideways. How far sideways is not documented.**

DiffuserPeakYaw=(0.0, 1.0) // Angle of peak, multiplier at peak  
**This line is optional within the section.**

**Defines the yaw angle at which the diffuser force is at its highest. First value is the horizontal angle to the centre line of the car at which the forces peak. The second is a multiplier to apply at that angle.**

DiffuserCenter=(0.0, 0.01, -1.265) // Center of diffuser forces (offset from center of rear axle at ref plane)  
**Position of the centre of action of diffuser forces relative to the centre of the rear axle and at the bottom of the body tub, aka at ride height.**

# SUSPENSION
This post covers the [SUSPENSION] section. It deals with the suspension settings for the sprung parts of the car and some of the relationships between graphics and physics.

The original is shown in regular text. My comments are in **bold**.

## [SUSPENSION]
PhysicalModelFile=BMWF106_Susp.pm  
**Calls the .pm file. Must be in VEHDIR or TEAMDIR as defined in the .gen file.**

CorrectedInnerSuspHeight=0.245 // Instead of moving inner susp height relative with ride height, use this offset (set to -1 for original behavior)

**CorrectedInnerSuspHeight *(CISH)* resets the height of the origin for the vertical location of the inner suspension points. The value is the vertical distance of that point above the reference plane. The reference plane is the bottom of the body as defined by the ride height.**

**Setting CISH to any value other than -1 attaches the inner suspension points to the body. Changes in RideHeight then take the inner points up or down with the body, which is more like what happens with real cars. Setting CISH = -1 delivers the 'original behaviour', which is to fix the inner suspension points relative to the static wheel locations defined in the pm. They stay there even if you move the body up and down.**

**The "original behaviour" uses the wheel radius to set the height above the ground of the line through the axles at each end of the car. The "centre" of that line is used as the (0.0, 0.0, 0.0) point for the pm file. The height above ground of that point is then reduced by the ride height to get the value for the original InnerSuspHeight which delivers the "original behaviour".**

**This gets a bit tricky when the wheels have different radii between front and rear and/or the ride heights are different. Also I observe that the origin for the pm is not usually at the geometric centre of the wheelbase for cars with uneven weight distributions, but close to the longitudinal position of the Centre of Gravity. So I presume we should adjust for those factors.**

**In any event, once the value which reproduces the "original behaviour" has been calculated, presumably one can place a bigger or smaller value in CorrectedInnerSuspHeight and move the inner points of the suspension arms up or down by the difference. Much nicer than having to recalculate the pm if you lower the car. Makes lowering as part of an upgrade much easier to handle.**

ApplySlowToFastDampers=0 // Whether to apply slow damper settings to fast damper settings  
**A switch to change between permitting separate settings for slow and fast dampers (0) and applying the slow settings to the fast values (1). This is to permit modelling of cars which have or do not have dual-range dampers, respectively.**

LimitFastDampers=0 // Whether to limit the fast damper rate to be less than or equal to the slow damper rate (actual rate, not numerical setting)  
**A switch to limit the upper values of the fast dampers relative to slow dampers - whether to enforce the typical damper constraint that the fast damper rate must be lower than or equal to the slow damper rate. I presume 1=yes.**

AdjustSuspRates=1 // Adjust suspension rates due to motion ratio (0 = direct measure of spring/damper rates, 1 = wheel rates)
**Switch to permit the spring and damper rates at the wheels to be changed between two modes.**

**=0 means the wheel rates are adjusted for the geometry of the pushrod and the location of the lower end of the pushrod relative to the inner and outer mounts of the wishbones.**

**=1 means the wheel rates are adjusted only for the location the lower end of the pushrod relative to the inner and outer mounts of the wishbones.**

**Note that =1 does not remove all the geometric implications from the pushrod definition. Only removing the definitions of the pushrods themselves from the [CORNER] sections will do that.**

AlignWheels=1 // Correct for minor graphical offsets
**Switch to permit the game to correct minor greaphical glitches which may affect the horizontal position of the wheel images relative to the body. This one aligns the wheels with the centre line.**

CenterWheelsOnBodyX=0 // Correct for minor unintentional graphical offsets  
**Turns out a bit more was needed in addition to AlignWheels. This switch aligns the wheels with the body in the X direction when the value is set to =1.**

**The way it does this can lead to unintentional results. The body width is measured and then the body is aligned along the Z axis with an equal amount of the body on either side. This works fine if the body is symmetrical. If the body is asymmetrical because, say a mirror on one side sticks out beyond any other part of the car, then the result is misaligned. Thanks to NEChris for discovering this behaviour on a Porsche 911 with only one mirror.**

FrontWheelTrack=1.3733 // If non-zero, forces the front wheels to be specified track width  
RearWheelTrack=1.3719 // If non-zero, forces the rear wheels to be specified track width  
LeftWheelBase=3.0593 // If non-zero, forces the left side to use specified wheelbase  
RightWheelBase=3.0593 // If non-zero, forces the right side to use specified wheelbase  
**If these parameters are set to zero, the wheel positions are set according to the location of the wheel images in the graphics. If set to non-zero then the explicit values define the positions of the images.**

**These positions may affect the physical behaviour. If you want to use the graphics for car "A" to develop car "X", then make sure that you have the proper values to go in this section to ensure the physics represent the target car.**

SpringBasedAntiSway=1 // 0=diameter-based, 1=spring-based
**Switch to swap between spring-based or torsion-bar antisway for the whole car**

AllowNoAntiSway=0 // Whether first setting gets overridden to mean no antisway bar
**Switch to permit disabling antisway**

FrontAntiSwayBase=0.0 // extra anti-sway from tube twisting
**This line is optional.**

**Additional antisway at zero displacement - sort of pre-load.**

FrontAntiSwayRange=(80000.0, 1000.0, 116)  
FrontAntiSwaySetting=60  
**Front antisway for spring-based as a regular pair of range-and-setting line. Being spring-based it is denominated in N/m.**

**As the result of some great experimental work by Kangaloosh and Niels_at_home, published here, it has been confirmed by ISI that there is a bug in the way spring-based antisway is applied to the car. The calculated spring-based antisway is assigned across the axle, which effectively halves the rate at the wheel by comparison with what it should be. Accordingly any calculated spring-based antisway-rate, front or rear, should be doubled when applied, as rF will halve it for you.**

FrontAntiSwayRate=(1.00e11, 4.0) // Not applicable with spring-based antisway  
**This value is used for tube-based antisway. Tube-based antisway uses the range and setting to define the diameter of tube and the AntiSwayRate line provides the base and the power values for this equation -**

>**antisway rate = base * (diameter in meters ^ power).**<br> 

**There is a comment from ISI that the power is always 4.**

RearAntiSwayBase=0.0 // extra anti-sway from tube twisting  
**This line is optional.**

RearAntiSwayRange=(20000.0, 1000.0, 76)  
RearAntiSwaySetting=35  
RearAntiSwayRate=(1.00e11, 4.0) // Not applicable with spring-based antisway 
**Rear antisway works like the front.**

FrontToeInRange=(-1.0, 0.025, 73)  
FrontToeInSetting=36  
RearToeInRange=(-0.8, 0.025, 73)  
RearToeInSetting=34  
**Toe ranges and settings, front and rear. Toe is denominated in degrees. Note that positive numbers are toe-in. For comparison with the method using difference between the distances measured across the car, at the axle and front edges of the tyres; For a 300mm radius wheel, 3mm or 1/8th inch of toe across both wheels is just under 0.3 degrees for each wheel, and that number is how it would would be presented in the garage.**

LeftCasterRange=(-1.5, 0.1, 71) // Front-left caster  
LeftCasterSetting=25  
RightCasterRange=(-1.5, 0.1, 71) // Front-right caster  
RightCasterSetting=25  
**Caster is mechanical trail and is defined in the hdv. It is denominated in degrees. Positive caster is "lead", ahead of the contact patch. Any caster defined in the pm file is updated by these values. Please see the pm file thread for the effeect of that on the location of the outer front suspension points.**

LeftTrackBarRange=(0.0, 0.0, 1) // rear-left track bar  
LeftTrackBarSetting=0  
RightTrackBarRange=(0.0, 0.0, 1) // rear-right track bar  
RightTrackBarSetting=0  
**The track bar - otherwise known as a panhard rod - is used to provide lateral location for a solid rear axle. These values are activated when a solid axle is define in the pm file. These ranges and settings permit the longitudinal location of the ends to be defined relative to the back axle, updating the locations defined in the pm.**
>This Option within the HDV from rFactor, is unfortunately not able to be edited within the Automobilista Setup Screen, as the option had been removed from the UI. it can still be edited via upgrades.

**The trackbar statements are optional.**

//THIRD SPRING  
**Third springs were created for cars with high downforce. The strategy is to run a third spring and/or damper on either axle, in order to separate out roll characteristics from those controlling vertical wheel motion. This permits single-wheel motion to have a relatively soft spring rate, whereas moving both wheels at the same end in the same direction, say up, causes the 3rd spring to be compressed so the effective spring rate at the wheel appears to be much higher. This permits improved control over ride height and hence downforce, and improved handling.**

**In this section you have the full spectrum of suspension settings; travel, bump stop, bump stop damper - slow and fast, rebound, packers and spring. Then the full set of slow and fast bump and rebound dampers.**

**Third springs are applicable to cars with relatively high downforce that were created after 1996. They started to appear in 1997 and are available today on certain off-the-shelf sports racing cars as options or standard fittings. For modelling of other cars or classes for which they are banned (most Touring cars), third springs should be zeroed out (preferred) or removed entirely.**

**By using a 3rd spring, it is possible to achieve stiffer suspension whilst the car's tyres are being displaced by the same amount (eg. travelling down a straight), yet at the same time it is possible to still reap the benefits from a softer suspension setup whilest cornering (bump or rolling motion). The trick is in the ''T-bar'' linking the springs/dampers to each other and to the bellcranks.**

**When both tyres are displaced by the same amount (as they would through aerodynamic forces pushing the car down on the straight), all 3 springs/dampers work together, as the T-bar does not rotate about any of it's pivots, providing a very stiff system.**

**When only one tyre is displaced, the T-bar rotates about it's central
pivot, resulting in only the spring/damper that corresponds to that wheel being worked. (note: the rotation of the T-bar will cause the other side of the suspension to be ''extended'' however)**

**Please see the [FRONTLEFT] section for a discussion of the parameters for springs, bump stops and dampers in the context of the regular suspension. The parameters in this section work the same way.**

Front3rdBumpTravel=-0.005 // Travel to bumpstop with zero packers and zero ride height (5mm compression)  
Front3rdReboundTravel=-0.065 // prevents rebound travel (for example, when upside down), 55mm max front ride height plus 10mm leeway  
Front3rdBumpStopSpring=150000.0 // Initial spring rate of bumpstop  
Front3rdBumpStopRisingSpring=7.00e6 // Rising spring rate of bumpstop (multiplied by deflection squared)  
Front3rdBumpStopDamper=2400.0 // Initial damping rate of bumpstop  
Front3rdBumpStopRisingDamper=7.00e5 // Rising damper rate of bumpstop (multiplied by deflection squared)  
Front3rdBumpStage2=0.060 // Speed where damper bump moves from slow to fast  
Front3rdReboundStage2=-0.060 // Speed where damper rebound moves from slow to fast  
Front3rdPackerRange=(0.000, 0.001, 41)  
Front3rdPackerSetting=5  
Front3rdSpringRange=(0.0, 2000.0, 101)  
Front3rdSpringSetting=35  
Front3rdSlowBumpRange=(0.0, 125.0, 25)  
Front3rdSlowBumpSetting=6  
Front3rdFastBumpRange=(0.0, 125.0, 21)  
Front3rdFastBumpSetting=2  
Front3rdSlowReboundRange=(0.0, 250.0, 33)  
Front3rdSlowReboundSetting=4  
Front3rdFastReboundRange=(0.0, 250.0, 29)  
Front3rdFastReboundSetting=2  
Rear3rdBumpTravel=-0.010 // Travel to bumpstop with zero packers and zero ride height (10mm compression)  
Rear3rdReboundTravel=-0.090 // Prevents rebound travel (for example, when upside-down), 80mm max rear ride height plus 10mm leeway  
Rear3rdBumpStopSpring=150000.0 // Initial spring rate of bumpstop  
Rear3rdBumpStopRisingSpring=7.00e6 // Rising spring rate of bumpstop (multiplied by deflection squared)  
Rear3rdBumpStopDamper=2400.0 // Initial damping rate of bumpstop  
Rear3rdBumpStopRisingDamper=7.00e5 // Rising damper rate of bumpstop (multiplied by deflection squared)  
Rear3rdBumpStage2=0.060 // Speed where damper bump moves from slow to fast  
Rear3rdReboundStage2=-0.060 // Speed where damper rebound moves from slow to fast  
Rear3rdPackerRange=(0.000, 0.001, 61)  
Rear3rdPackerSetting=10  
Rear3rdSpringRange=(0.0, 2000.0, 101)  
Rear3rdSpringSetting=40  
Rear3rdSlowBumpRange=(0.0, 125.0, 25)  
Rear3rdSlowBumpSetting=6  
Rear3rdFastBumpRange=(0.0, 125.0, 21)  
Rear3rdFastBumpSetting=2  
Rear3rdSlowReboundRange=(0.0, 250.0, 33)  
Rear3rdSlowReboundSetting=6  
Rear3rdFastReboundRange=(0.0, 250.0, 29)  
Rear3rdFastReboundSetting=2  

# [CONTROLS], [ENGINE], [DRIVELINE]
This covers the [CONTROLS], [ENGINE] and [DRIVELINE] sections.  
The original is shown in regular text. Bristows comments are in **bold**.

## [CONTROLS]
SteeringFFBMult=1.5  
**Factor to increase or decrease the force feedback effect for this car. Presumably included to cater for the low feedback from cars with low(er) grip than GP cars.**

SteerLockRange=(5.0, 0.5, 51)  
SteerLockSetting=20  
**Defines steering lock range and setting. This one provides 15 degrees, which gives a car with a 3.0m wheelbase a turning circle of about 24m, so this is not too quick a ratio. The issue comes from game controller wheels which only turn 270 deg and the aim of some drivers to have them mimic Real World sensitivity. Either one has to buy a wheel with more turns, or put up with less sensitive steering. Given that the sim situation is one of relative calm without the noise and fury of a real racetrack with its sounds and the bumping about from the travel of the car, I suspect we could put up with less sensitivity. A car with a 3.0 m wheelbase which has a turning circle of about 40 feet/12 m would have a steering lock of around 30 degrees. You know - you need enough lock to catch those slides as well.**

RearBrakeRange=(0.250, 0.002, 226)  
RearBrakeSetting=100  
**Defines the proportion of braking applied to the rear of the car. This one is 45%.**

BrakePressureRange=(0.60, 0.01, 41)  
BrakePressureSetting=36  
**Defines the brake pressure as a percentage of the brake torque defined in the [FRONTLEFT] and so on sections. The way of managing the braking effort at the car level.**

HandbrakePressRange=(0, 0.05, 1) // Disabled... intended for rally-type cars
HandbrakePressSetting=0  
**Defines the handbrake pressure.**

Handbrake4WDRelease=2.0 // Represents the handbrake value where the center diff will be completely disconnected. See "Rhez06.hdv" for more details.

**The following is from the Rhez 06 hdv:**

**HandbrakePressRange=(0.0, 0.05, 21) // intended for rally-type cars. Handbrake4WDRelease represents the**  
**HandbrakePressSetting=15 // handbrake value where the center diff will be completely disconnected.**  
**Handbrake4WDRelease=0.5 // It will *start* disconnecting at half that value, range is 0.0 (disconnect immediately with any handbrake) to 2.0 (default value which means to never even partially disconnect).**  

UpshiftAlgorithm=(0.975,0.0) // Fraction of rev limit to auto-upshift, or rpm to shift at (if 0.0, uses rev limit algorithm)  
DownshiftAlgorithm=(0.91,0.70,0.60) // High gear downshift point, low gear downshift point, oval adjustment  
**A switch to permit toggling between 2 options for managing upshift and downshift under Autoshift.**

AutoUpshiftGripThresh=0.65 // Auto upshift waits until all driven wheels have this much grip (reasonable range: 0.4-0.9)  
AutoDownshiftGripThresh=0.60 // Auto downshift waits until all driven wheels have this much grip (reasonable range: 0.4-0.9)  
**Manages Autoshift while sliding.**

TractionControlGrip=(1.01, 0.18) // Average driven wheel grip multiplied by 1st number, then added to 2nd  
TractionControlLevel=(0.47, 0.83) // Effect of grip on throttle for low TC and high TC  
**Manages traction control factors.**

ABS4Wheel=1 // 0 = old-style single brake pulse, 1 = more effective 4-wheel ABS  
**Defines ABS type.**

ABSGrip=(1.00, 0.20) // Grip multiplied by 1st number and added to 2nd
ABSLevel=(0.40, 0.95) // Effect of grip on brakes for low ABS and high ABS
**Factors to permit tuning ABS**

OnboardBrakeBias=1 // Whether brake bias is allowed onboard  
**Switch to enable brake bias settings from the cockpit**

## [ENGINE]
Normal=BMWP86_Engine // Unrestricted engine  
**Regular engine**

RestrictorPlate=BMWP86_Engine // Restrictor plate engine  
**Restrictor engine when required by track or season.**

## [DRIVELINE]
ClutchEngageRate=1.2 // How fast to engage clutch  
**A factor regulating clutch engagement rate.**

ClutchInertia=0.0085 // Inertia of parts between clutch and transmission  
**Another part of the rotating inertias in the driveline.**

ClutchTorque=700.0 // Maximum torque that can be transferred through clutch  
**Torque capacity of the clutch.**

ClutchWear=0.0 // Unimplemented  
ClutchFriction=8.40 // Friction torque of parts between clutch and transmission when in gear (automatically reduced in neutral)BaulkTorque=500.0 // Maximum torque transferred through gears while engaging them  
AllowManualOverride=1 // Whether to allow manual shift overrides when using auto shifting  
SemiAutomatic=1 // Whether throttle and clutch are operated automatically (like a high-end car)  
**Seems simple to me...**

UpshiftDelay=0.032 // Delay in selecting higher gear (low for semi-automatic, higher for manual)  
UpshiftClutchTime=0.005 // Time to ease auto-clutch in AFTER upshift  
UpshiftLiftThrottle=0.00 // Lift to this throttle fraction while upshifting (if controlled by game not player)  
DownshiftDelay=0.046 // Delay in selecting lower gear (low for semi-automatic, higher for manual)  
DownshiftClutchTime=0.034 // Time to ease auto-clutch in AFTER downshift (used to be SemiAutoClutchTime)  
DownshiftBlipThrottle=0.95 // Amount of throttle used to blip if controlled by game (instead of player)  
WheelDrive=REAR // Which wheels are driven: REAR, FOUR (even torque split), or FRONT  
**Likewise**

GearFile=BMW_gears.ini // Must come before final/reverse/gear settings!  
**Calls the gears file. Must be located in the TEAMDIR or the VEHDIR.**

AllowGearingChanges=1 // Whether to allow gear ratio changes  
**Switch to enable gear ratio changes in the garage.**

AllowFinalDriveChanges=1 // Whether to allow final drive ratio changes
**Switch to enable final drive ratio changes in the garage - there have to be some ratios available in xxx_gears.ini as well.**

FinalDriveSetting=1 // Indexed into GearFile list  
ForwardGears=7  
ReverseSetting=3  
Gear1Setting=3  
Gear2Setting=18  
Gear3Setting=26  
Gear4Setting=33  
Gear5Setting=39  
Gear6Setting=43  
Gear7Setting=47  
**The ratios are read from the xxx_gears.ini file. The entries are rearranged in descending order if required befoer being read. The entries are read by counting down from under the [GEAR RATIOS] line, starting with 0 at the first line. The final drive ratio counts down from just under [FINAL_DRIVE], ignoring the bevel= line and counting from 0 from the next line.**

DiffPumpTorque=250.0 // At 100% pump diff setting, **this value is** the **amount of** torque redirected per wheelspeed difference **between the driven wheels** expressed in radians/sec (**which is** roughly 1.2kph)  
DiffPumpRange=(0.00, 0.01, 101) // Differential acting on all driven wheels  
DiffPumpSetting=30  
**DiffPump torque and setting defines the rate at which torque transmitted between wheels by the differential increases with the wheelspeed difference.**

**The DiffPumpTorque is the amount of torque in Nm transmitted for each wheelspeed difference of ~1.2kph, at 100% pump setting. The range and setting lines define how much of that max torque value is actually applied.**

**As one wheel starts to slip relative to the other, the wheelspeed difference increases. As it goes up, the amount of torque which can be redirected goes up in direct proportion. The amount is the DiffPumpTorque x the fraction from the DiffPump range and setting - in this case 0.30. So at ~1.2kph difference in wheelspeed, the diff can transmit up to 75 Nm. At maximum engine torque in 3rd gear, the torque into the diff is 607.7 Nm, so the diff pump could handle this load at ~9.7 kph wheelspeed difference - which is not much at all, less than 5% at 200kph.**


DiffPowerRange=(0.00, 0.01, 101) // Fraction of power-side input torque transferred through diff  
DiffPowerSetting=15 // (not implemented for four-wheel drive)  
**The percentage of the driving torque applied to the diff which is distributed to both axles. Setting to 100% means that when you apply throttle the torque is applied equally to both wheels. A setting of 0% means that power will follow the path of least resistance and you will have something like an open differential. Intermediate values give you partial application.**

DiffCoastRange=(0.00, 0.01, 101) // Fraction of coast-side input torque transferred through diff  
DiffCoastSetting=20 // (not implemented for four-wheel drive)  
**The percentage of the coasting torque applied to the diff which is distributed to both axles. Works like the previous parameter but on coast or overun or whatever you call it.**

DiffPreloadRange=(80.0, 4.0, 26) // Preload torque that must be overcome to have wheelspeed difference  
DiffPreloadSetting=5 // (not implemented for four-wheel drive)  
**The torque difference between the wheels which must be overcome before they can spin at different speeds. Up until this value, the diff acts as if it is locked. After that the other factors apply.**

**Setting Preload to a suitably high value creates a locked diff. Create a range like (0.0, 2000,0, 1) enable one to have a locked diff which can be turned on of off by choosing a setting of 0 or 1.**

RearSplitRange=(1.00, 0.10, 1) // Torque split to the rear, defaults to  
RearSplitSetting=0 // 50:50 if these entries aren't here.  
Pump4WDEffect=( 1.0, 1.0, 1.0) // Effect of various diff settings on  
Power4WDEffect=( 0.0, 0.0, 0.0) // the center diff, then the front diff,  
Coast4WDEffect=( 0.0, 0.0, 0.0) // and then the rear diff. Sorry, no  
Preload4WDEffect=(0.0, 0.0, 0.0) // separate settings for each diff.  
**Diff settings for 4WD and rally cars. Better than before but not complete yet.**

# [CORNERS]
This covers the [FRONTLEFT] and the following [CORNER] sections for the other corners of the car.

The original is shown in regular text. Bristows comments are in **bold**.

## [FRONTLEFT]

BumpTravel=-0.005 // Travel to bumpstop with zero packers and zero ride height (5mm compression)  
ReboundTravel=-0.057 // Prevents rebound travel (for example, when upside-down), 45mm max front ride height plus 12mm leeway  

**Defines the limits of distance over which the wheel can travel vertically, relative to the reference plane.**

**BumpTravel is the extreme upward extent to which the suspension can move, relative to the "reference plane", which is usually the bottom of the body tub, before the suspension runs out of travel.**

**ReboundTravel is the extreme downward extent over which the suspension can move, relative to the tub, before it runs out of travel.**

**Do not misinterpret these values as the distance the suspension can move up or down. They define the location of a limit, not a distance.**

**Suspension travel up (a positive number) is RideHeight plus BumpTravel (Algebraic sum). For this car, Suspension travel up is 0.038 + (-0.005), which is 0.033**

**Suspension travel down (a negative number) is RideHeight plus ReboundTravel (Algebraic sum). For this car, Suspension travel down is 0.038 + (-0.057), which is -0.019**

**Total suspension travel is the algebraic sum of BumpTravel minus ReboundTravel. That total is 0.033 - (-0.019) or 0.520 (metres).**

**Packers will reduce the available bump travel before running out of travel.**

**This car has the BumpTravel value at -0.005, which means the suspension limit of travel is when the body tub is 5mm off the ground.**

**If the suspension runs out of travel during a corner the car behaviour becomes erratic and it can spin out of control. Bump stops may be leaned on during cornering, but their values have to very carefully matched to the spring values so there is a smooth transition.**

**In F1C, Other symptoms of inadequate suspension travel or ride height values outside the available travel range occurred. They were rapid side-to-side head movement by the driver and a reduction in frames per second displayed. This was an ISI engine issue that can be quite severe to the point of making a car unusable in groups. I do not know if it happens in rF.**

BumpStopSpring=150000.0 // Initial spring rate of bumpstop  
BumpStopRisingSpring=7.00e6 // Rising spring rate of bumpstop (multiplied by deflection squared)  
BumpStopDamper=2400.0 // Initial damping rate of bumpstop  
BumpStopRisingDamper=7.00e5 // Rising damper rate of bumpstop (multiplied by deflection squared)  
**Spring and damper properties of the bumpstop**

BumpStage2=0.060 // Speed where damper bump moves from slow to fast  
ReboundStage2=-0.060 // Speed where damper rebound moves from slow to fast  
**Defines the speed of vertical wheel movement (m/s) at which transition from slow to fast dampers takes place, separately for bump (up) and rebound (down)**

FrictionTorque=2.40 // Newton-meters of friction between spindle and wheel  
SpinInertia=0.9040 // Inertia in pitch direction including any axle but not brake disc  
**Adequately commented.**

**There is also an old HDV variable "SpinInertiaAI" which allows a different wheel spin inertia for AI. If this value is NOT used, the AI by default have twice as much spin inertia to help the physics deal with their lower sampling frequency. If you choose to use this value and make it more realistic, be careful to make sure that the AI wheels don't jitter at low speeds.**

CGOffsetX=0.000 // X-offset from graphical center to physical center (NOT IMPLEMENTED)

PushrodSpindle=(-0.030,-0.120, 0.00) // Spring/damper connection to spindle or axle (relative to wheel center)  
PushrodBody=( -0.560, 0.195, 0.10) // Spring/damper connection to body (relative to wheel center)  
**Defines the virtual location of the spring/damper pushrod connection points at the wheel carrier and at the body. The pushrod is the member which transmits suspension movements and forces to the primary and 3rd spring/damper units mounted in the body of a modern F1 car. For other cars, the pushrod's end locations define the upper and lower mounting points of the coil-over damper unit used on many cars. Note that this implies that the coils are mounted on the same axis as the dampers and separately located springs and shocks, as found on certain "blade suspensions" are not supported.**

**Pushrods were designed for a suspension system like an F1 car. In F1, often the front pushrod is attached at or very close to the kingpin axis and this is buried inside the front wheel quite close to the upright.**

**In rF the pushrod is attached to the spindle and moves with it, including rotation. This may lead to steering action causing a response from the springs with steering and jacking effects effects as a result if the pushrod is not very close to the kingpin axis.**

**If you wish to minimise the the leverage effect of pushrod spindle-end placement the pushrods need to be close to the wheel, and to minimise steering effects at the front they need to be close to the spindle. This may compromise modelling actual real car layouts.**

**Defining pushrods in these sections permits the AdjustSuspRates parameter in the [SUSPENSION] section to work as documented.**

**Pushrods are optional, but are present by default in all ISI-supplied cars. If not pushrods are defined then the effective location is assumed to be vertically over the wheel centre, and the spring and damper rates are applied at the wheels.**

CamberRange=(-5.0, 0.1, 56)  
CamberSetting=16  
**Camber range and setting. Relates to the limits and factors set by CamberLatLong in the tbc file.**

PressureRange=(90.0, 1.0, 106)  
PressureSetting=42  
**Tyre pressure range and setting, in kPa. Incorrect tire pressures can lead to overheating, loss of grip, uneven wear and premature failure.**

PackerRange=(0.000, 0.001, 31)
PackerSetting=13
**Packers are a field/track method for trimming suspension movement before the bump rubbers are reached. Denominated in metres of suspension movement.**

SpringMult=1.0 // Take into account suspension motion if spring is not attached to spindle (affects physics but not garage display)  
**A multiplier-factor which is applied to the spring rate defined just below. This factor permits the spring rate to be adjusted for the fact that the spring is mounted somewhere inboard of the lower outer suspension point. By comparison, AdjustSuspRates back up in [SUSPENSION] is a switch which enables rF to make the calculation based on analysis of suspension and pushrod locations. This factor is available individually for each wheel. The switch in [SUSPENSION] is applied across the car.**

SpringRange=(68000.0, 2000.0, 101)  
SpringSetting=13  
**The spring range and setting for this wheel, sets the spring rate in N/m. These spring are linear in action, as the spring rate is constant through the permitted movement. Any progressive effects have to come from somewhere else.**

SpringRubberRange=(5000.0, 5000.0, 1) // Spring rubbers can potentially be changed at pitstops if available, first value is automatically detached  
SpringRubberSetting=0  
**Spring rubbers are inserts which may be inserted between the coils of coil-springs, connecting the coils and so reducing the effective number of coils in the spring. This causes the effective spring rate to increase. Spring rubbers seem to come from stock car racing where they provide an easy field change option to increase or decrease spring rate in the pits. The other option would be to change the spring itself, a slower operation.**

**I am guessing, but I expect that rF treats these rubbers as if they added their spring rate to the that of the main springs.**

RideHeightRange=(0.020, 0.001, 26)  
RideHeightSetting=18  
**Ride height range and setting. This sets the height the car rides above the ground. Typically set to about half the available suspension travel defined by the difference between the locations defined in BumpTravel and ReboundTravel.**

**rF applies a virtual preload to the suspension to locate the car at this ride height when stationary. Changing the ride height in here or the garage changes the amount of the preload to achieve the desired result. Please see CorrectedInnerSuspensionHeight at the top of post #4 to see what a change in ride height may do to the location of the inner suspension points.**

DamperMult=1.00 // Take into account suspension motion if damper is not attached to spindle (affects physics but not garage display)  
**Similar to SpringMult, but for the shocks.**

SlowBumpRange=(3000.0, 125.0, 29)  
SlowBumpSetting=12  
FastBumpRange=(1500.0, 125.0, 25)  
FastBumpSetting=8  
SlowReboundRange=(5250.0, 250.0, 28)  
SlowReboundSetting=15  
FastReboundRange=(3000.0, 125.0, 29)  
FastReboundSetting=12  
**Full set of four ranges and settings for the front left shocks (dampers). Denominated in Newtons per metre/sec.**

BrakeDiscRange=(0.026, 0.001, 3) // Disc thickness  
BrakeDiscSetting=2  
BrakePadRange=(0, 1, 5) // Pad type (not implemented)  
BrakePadSetting=2  
BrakeDiscInertia=0.820 // Inertia per meter of thickness  

BrakeOptimumTemp=650.0 // Optimum brake temperature in Celsius (peak brake grip)  
BrakeFadeRange=1240.0 // Temperature outside of optimum that brake grip drops to half (too hot or too cold)  
**These values permit definition of the best brake disc temperature and the rate of fall-off when the disc is off-temperature. I presume the fall-off is symmetrical on the hot and cold sides.**

**More complex brake response to temperature is possible from v1.250. To use, replace "BrakeOptimumTemp" and "BrakeFadeRange" with "BrakeResponseCurve=(<cold>,<min_optimum>,<max_optim um>,<hot>)", where each value is a temperature in Celsius. At <cold> temperature, brake torque is half of optimum. Between <min_optimum> and <max_optimum>, brake torque is optimum. At <hot> temperature, brake torque is half of optimum.**

**V1.250 added "BrakeGlow" for each wheel in the HDV file to define at what temperatures the brake glow ramps up. Default legacy values are (in Celsius): BrakeGlow=(750.0,1000.0).**

BrakeWearRate=5.850e-011 // Meters of wear per second at optimum temperature  
BrakeFailure=(1.45e-02,7.00e-04) // Average and variation in disc thickness at failure
**Underlying values for brake wear and, eventually, failure.**

BrakeTorque=4050.0 // Maximum brake torque at zero wear and optimum temp  
**And at 100% braking effort.**

**New HDV variable "BrakeTorqueAI" supported in v1.250 and after, allows a different brake torque for AI. This might be used to compensate for differences with the player's car, as the AI is not currently affected by cold or faded brakes.**

BrakeHeating=0.00191 // Heat added linearly with brake torque times wheel speed (at max disc thickness)  
BrakeCooling=(3.650e-02,4.500e-04) // Minimum brake cooling rate (base and per unit velocity) (at max disc thickness)  
BrakeDuctCooling=0.8000e-04 // Brake cooling rate per brake duct setting (at max disc thickness)  
**These values underly the balance of heating and cooling which decides the brake disc's operating temperature.**


## [FRONTRIGHT]
**Repeats the first wheel.........**

**.............and so on for the other corners of the car.**
