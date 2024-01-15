# ISI HDV FILE DOCUMENTATION
## A lot of the work here is credited to the Race Sim Central User "Bristow". Thanks be to him and all other contributors 

Start HDV Code: (Anything that is meant to be in comments will be commented out by "//", anything that is added by myself will be highlighted in bold and underlined.)

Bristows Original Comments:   
The original is shown in regular text. My comments are in bold.

Nomenclature - I use the terms Range and Setting with the same meaning as shown in lines 5 and 6 of the file.  
The term Switch is used to refer to a parameter which is used to toggle between two states, usually whether a particular feature is switched on or off.  
A Multiplier is usually applied to another value or parameter by multiplying them together.  
A Factor may be used in some way to modify a parameter or behaviour defined elsewhere.

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

//
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