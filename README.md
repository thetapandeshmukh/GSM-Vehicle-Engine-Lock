# GSM-Vehicle-Engine-Lock

The goal of this system is to enhance vehicle security by integrating a GSM-based alert and engine locking system. If unauthorized access is detected (such as incorrect password attempts), the engine is automatically locked, and a notification is sent to a designated mobile number via SMS. The system also requires password verification to start the engine.

Key Components and Their Roles
PIC18F4520 Microcontroller: Acts as the central processing unit for the system, handling password verification, controlling the relay for the engine lock, and managing communication with the GSM module.
GSM Module (SIM800L): Sends an SMS alert when unauthorized access is detected. The microcontroller communicates with the GSM module through UART.
4x4 Keypad: Allows the user to enter a password to start the engine. This input is read by the microcontroller and checked against the preset password.
Relay Module: Connected to the engine control circuit, the relay allows the microcontroller to lock or unlock the engine based on the password verification.
Step-by-Step Working of the System
System Initialization:

The microcontroller initializes the UART to communicate with the GSM module.
The engine starts in an unlocked state (relay is activated).
A preset password is stored in the microcontroller’s memory.
Password Entry:

The user enters a password using the keypad. Each keypress is registered and stored temporarily in the entered_password array.
Once the user has entered the complete password, the microcontroller calls the Check_Password() function to validate it.
Password Validation:

If the entered password matches the correct password, the Unlock_Engine() function is called, keeping the relay active and allowing the engine to start.
If the password does not match, the attempt_count variable increments by 1.
Handling Unauthorized Access:

If the user enters the wrong password three times in a row, the system calls the Lock_Engine() function:
This function deactivates the relay, which effectively locks the engine, preventing it from starting.
An SMS alert is sent via the GSM module to a preset mobile number to notify the owner of unauthorized access attempts. The SMS is sent using standard AT commands to set the GSM module in text mode, enter the message content, and send it.
Engine Control:

The engine can only be unlocked and started if the correct password is entered.
Once the engine is locked after three failed attempts, it remains locked until the system is reset or reprogrammed (though this behavior can be modified if needed).
Continuous Monitoring:

The system continuously monitors for new password entries and processes them as described above. This ensures that any attempt to start the engine is always verified.
Summary of the Workflow
User attempts to start the engine by entering the password on the keypad.
The microcontroller verifies the password:
Correct password → Engine remains unlocked.
Incorrect password → Increments attempt counter.
After three failed attempts:
The relay deactivates, locking the engine.
An SMS alert is sent to the authorized user via the GSM module.
This system provides a simple, cost-effective approach to improve vehicle security by using password verification and remote alert capabilities via GSM communication.
