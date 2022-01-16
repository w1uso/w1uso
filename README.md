- 👋 Hi, I’m Rich @w1uso. I am currenly designing and building a HF amateur band receiver. Incorporated is a modified Richard Visokey (AD7C) ARDUINO NANO VFO. The modification uses 3 additinal hardware switches to select 1 of the frequency bands. 
I have come up with the foolowing approach to decode and implement the function:

bandswitchmask is a global variable

void bandswitch();    // Read the state of the band switches and set vfo frequency
   {
 byte bandswitchstate1 = digitalRead(A1);
 byte bandswitchstate2 = digitalRead(A2);
 byte bandswitchstate3 = digitalRead(A3);
 byte bandswitchstate = 0;
   if (bandswitchstate1 == LOW); {
          bandswitchstate = 00000001;
  };
  if (bandswitchstate2 == LOW); {
          bandswitchstate + 000000010;
  }; 
  if (bandswitchstate3 == LOW); { 
          bandswitchstate + 00000100;
  };
        for  (int bandswitchmask = 0; bandswitchmask <= 7; bandswitchmask ++) { //scan and compare switchstate  to a mask 
          if (bandswitchmask == bandswitchstate & bandswitchmask != oldbandswitchmask) { // if a match do the case if no change exit
            switch(bandswitchmask) {
              case 0: rx = b80m;
              break;
              case 1: rx = b40m;
              break;
              case 2: rx = b30m;
              break;
              case 3: rx = b20m;
              break;
              case 4: rx = b17m;
              break;
              case 5: rx = b15m;
              break;
              case 6: rx = b12m;
              break;
              case 7: rx = b10m;
              break;
              oldbandswitchmask = bandswitchmask;
            };//switch
           };//if
          };//for
   }; //bandswitch 
   
   Looking for comments or better solution
