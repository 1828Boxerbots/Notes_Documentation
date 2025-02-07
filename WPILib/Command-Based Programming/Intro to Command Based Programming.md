---
tags:
  - Commands
---
# Table of Contents
- [[#What is "Command-Based" Programming]]
- [[#Subsystems and Commands]]
	- [[#Commands]]
	- [[#Subsystems]]
- [[#How Commands Are Run]]
- [[#Composition of Commands]]
---
# What is "Command-Based" Programming
- Command-Based programming is a [[Glossary#Design Pattern|design pattern]]
	- This is not a requirement to write robot code, but is very effective at creating maintainable code
- The command-based paradigm is an example of [[Glossary#Declarative Programming|declarative programming]]
- The command-based tools provided by WPILib allow developers to specify robot behavior without relying on logic within loops
- See the example below of the exact same logic with and without command-based programming
```C++
// Command-Based Programming (using a lambda)
Trigger([&condition] { return condition.Get(); }).OnTrue(frc2::cmd::RunOnce([&piston] { piston.Set(frc::DoubleSolenoid::kForward); }));

// Without Command-Based (placed in robot periodic)
if(condition.Get()) {
  if(!pressed) {
    piston.Set(frc::DoubleSolenoid::kForward);
    pressed = true;
  }
} else {
  pressed = false;
}
```
# Subsystems and Commands
- The command-based pattern is designed around two core abstractions
	- Commands
	- Subsystems
	
	![[Command_Subsystems_Diag.png]]
## Commands
- A command represents an action that the robot can take
- For a command to be run, it has to be scheduled
	- They run until they are interrupted or end
- Commands can also be composed of other commands
	- Allowing the creation of simple commands and achieving more complex behavior by combining actions
- For more info, see [[Commands]]
## Subsystems
- Subsystems represent the independently controlled sections of the robot's hardware
	- Sensors, motor controllers, etc.
# How Commands Are Run
- For more information see [[The Command Scheduler]]
# Composition of Commands