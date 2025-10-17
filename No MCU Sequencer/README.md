I designed a sequencer on a 2"x2" PCB with 555 timers and SISO shift registers! 
The user can input up to 8 notes in the shift register and play them back at an adjustable speed (0.8754Hz to 2Hz) with the potentiometer. 
The three 555 timers are for clocking in current input notes, setting the playback frequency, and outputting the notes stored in the shift registers. 
I currently have one shift register for each note. 

**TO USE: **
Loop the 3 notes for a spooky tune! Use record button to clock in notes. 

**FUTURE IMPROVEMENTS:**
- If I get a decoder, I can use each shift register to represent one bit of information and can actually represent 8 notes with only 3 shift registers!
- No decoder--possibly implement an R2R DAC with an antilog amplifier to create a full scale of notes?
- Find more slide switches...to replace the push buttons for the notes

**Detailed Description:**
I designed a simple sequencer using 3 shift registers and 3 555 timers, where the user is able to “store” up to eight “beats” from a selection of three distinct notes in the SISO shift registers in the pulse mode and play them back at a configurable frequency in the playback mode. 

Each shift register stores the memory of one note and is configured to “correspond to” one of three notes: A3, C4, and D#4. When these notes are played in sequence, it should output a spooky tune. 

The first 555 timer is configured in its monostable mode, with a pulse width of 1.1(1kOhm)(1uF) = 110ms. I chose these specific values so that the pulse width would be longer than the time it takes for the button to settle after debouncing. The purpose of this component lies in the functionality of the SPDT switch (which I call the mode switch) connected to the SRCLKpin 11 input of the shift registers connected to it, which toggles between two modes: pulse mode and playback mode. 

When the mode switch is toggled to pulse mode and the button connected to this timer is pressed, the current state of the push buttons associated with each shift register/note are clocked in. 

The second 555 timer is configured in astable mode, with a variable frequency of 0.8754Hz to 2Hz because of the 10k potentiometer as our R2 in this formula:
 

When the mode switch is toggled to playback mode, notes will play back at this specified frequency. 

The third 555 timer controls the tone of the outputted notes. When the mode switch is toggled to pulse mode, the state of the push buttons connected to each shift register controls whether a “play” or “silent” signal gets stored in the shift register for the corresponding note. When the mode switch is toggled to playback mode, the output of the shift registers determines whether the corresponding nMOS gate for each tone is open or closed. 

To elaborate on the input to SERpin 14 for the shift registers: When the 555 timer is in pulse mode, SERpin 14 takes the button input branch as its input. When the 555 timer is in playback mode, SERpin 14 takes the output of QH’pin 9 as its input (it loops the values stored in the shift register). This is controlled via the SPDT switches connected to each shift register.

The reset button resets the shift registers. 

Let us say that we want to play a simple sequence of notes: A3, C4, D#4, silence, A3, C4, D#4, silence. Because the shift register can only store eight bits of data, the melody will loop once these eight notes have been played. 
Ensure all 4 SPDT switches are toggled to pulse/record mode. Also press the reset button to ensure the shift registers are fully cleared. 
Press down on the push button corresponding to the note A3, and without releasing it, press down on the push button connected to the first 555 timer to send a pulse to the shift registers. Because A3 is the only button pressed down, a ‘1’ will be clocked into the 8th bit slot of the A3 shift register. 
Now release all buttons. Press down on the push button corresponding to C4, and clock it in the same way as in step 2. Now, a ‘1’ will be clocked into the 8th bit slot of the C4 shift register. The bit in ‘A3’ will “move up” to the 7th slot. 
Now repeat this until the remaining 6 notes are clocked into the shift registers. 
Toggle the three SPDT switches connected to the shift registers to playback mode now in no particular order. This means that the shift registers will no longer take inputs from the corresponding buttons but will loop the data already stored in them. 
Now flip the SPDT switch connected to the SRCLKpin 11 input to playback mode so that notes are clocked in periodically at a frequency corresponding to that of the playback frequency of the second shift register. 
The inputted notes should now loop until the reset button is pressed or power is disconnected!

