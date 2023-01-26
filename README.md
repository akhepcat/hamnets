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

# Configuration
  hamnets is a perl script, and the configuration file it uses is also pure
  perl code.  An example configuration file [hamnets.cfg] is supplied in
  this repository, and should be placed in the ".config/" directory under
  your user's home.  

  There are two basic sections, the "rigs" and the "nets"

## Config -> rigs
  Each rig is defined by its name, model number, device, and optional
  arguments for rigctl to use for this particular rig.   An example rig
  looks like this

    %{$rigs{"FT-817"}} = ( "model" => 1020, "dev" => "/dev/digirig", "opts" => "-P RTS" );

  The rig name "FT-817" is also used in the 'nets' section to define which
  rig to send configuration parameters to.

  * 'model' is the rigctl model number, found by "rigctl -L | grep (my rig name)"
  * 'dev'  is the unix device name to use.  Use udev rules to make your life easier and the names consistent!
  * 'opts' are any additional rig-specific configurations that rigctl needs

## config -> nets
  This is perhaps the most critical part of the configuration, and has the
  most optional parameters.  If your rig doesn't require or support the optional
  parameter, it's best that you remove it from the config stanza, or your rig
  may generate errors.  Each of the options is documented below.

    %{$nets{"akerc"}} = ( "rig" => "FTdx10",    # Req: The name of the rig that can use this 'Net
                 "freq" => 14292000,            # Req: The Frequency of the 'Net
                 "mode" => "USB",               # Req: Which modulation mode to use
                   "pbf" => 0,                  # Opt: the passband filter width for the mode, 0 uses mode default
                   "nb" => 0,                   # Opt: Noise Blanker depth (0=off, range dependent on rig)
                   "nr" => 0.1,                 # Opt: (Digital) Noise Reduction depth (0=off, range dependent on rig)
                 "rfil" => 2,                   # Opt: Roofing filter width to use (values rig dependent)
               "preamp" => 10,                  # Opt: What preamp level to use (values rig dependent)
               "starts" => "08:30",             # Req: 24h clock, aka military time
               "duration" => "30",              # Opt: duration in minutes, default is 60m
               "days" => "MTWRF",               # Req: s'U'nday, M, T, W, thu'R'sday, F, S
         "desc" => "Alaska Pacific Emergency Preparedness Net",  # Req: The description of the 'Net
                 );


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

