# hamnets
  CLI tool for managing rigctl capable amateur radios and chat ('Nets)  favorites

# Usage
  The application will display any configured 'Nets, sorted by their rig,
  then by the day, followed by the time.

    $ hamnets
      net for today can be:

        FT-817:
           morning (145.5000 MHz  FM) - 10:00 (UMTWRFS) - Alaska Morning Net
             south (146.5200 MHz  FM) - 19:00 (...W...) - SouthCentral simplex

        FTdx10:
            pacsea ( 14.3000 MHz USB) - 18:00 (UMTWRFS) - Pacific Seafarers Net
           snipers (  3.9200 MHz LSB) - 18:00 (UMTWRFS) - Alaska Snipers Net
              bush (  7.0930 MHz LSB) - 20:00 (UMTWRFS) - Alaska Bush Net
            motley (  3.9330 MHz LSB) - 21:00 (UMTWRFS) - Alaska Motley Net, by KL7G
             akerc ( 14.2920 MHz USB) - 08:30 (.MTWRF.) - Alaska Pacific Emergency Preparedness Net
              noon (  3.9200 MHz LSB) - 12:00 (.MTWRF.) - Old Timers Noontime net

    $ hamnets noon
      Selected noon

      F 3920000 
      M LSB 0 
      F 3920000 
      L ROOFINGFILTER 2 
      L PREAMP 10 
      L NB 0 
      L NB 0.1 
      U NR 1 


# Color
  The application can provide the information above in color, with additional
  information to distinguish between upcoming, in progress, and past Nets
  for today

  This is enabled by either passing the '-c' flag to the application, or
  by creating a symlink to the main application with a trailing 'c', or
  'color',  i.e.,  "hamnetsc", "hamnets-c", "hamnets-color", etc.


# Verbose
  Verbose mode ( '-v' ) enables viewing of all configured nets, instead of
  just those scheduled for today.

