I designed a sequencer on a 2"x2" PCB with 555 timers and SISO shift registers! 
The user can input up to 8 notes in the shift register and play them back at an adjustable speed (0.5737Hz-2.8Hz) with the potentiometer. 
The three 555 timers are for clocking in current input notes, setting the playback frequency, and outputting the notes stored in the shift registers. 
I currently have one shift register for each note. 

FUTURE IMPROVEMENTS:
- If I get a decoder, I can use each shift register to represent one bit of information and can actually represent 8 notes with only 3 shift registers!
- No decoder--possibly implement an R2R DAC with an antilog amplifier to create a full scale of notes?
