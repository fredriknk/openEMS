# openEMStesting
Testing the OpenEMS FDTD solver for antenna optimization.

The entire simulation stack is opensource and free to use for anyone commercial or private, allowing you to create matched antennas for your designs.  

The Mifa_groundplane.py is an automated IFA/MIFA generator which allows for automated optimization of antenna design

The antenna generation is optimized for the avaliable groundplane so in essence you can just design a pcb, input the groundplane parameters and the script will generate a ifa/mifa for you based on the avalible space on the pcb.

Avaliable paramaters are as follows:
 |------------- substrate_width -------------------|
  _______________________________________________      _ substrate_thickness
 | A             |----------ifa_l(total length)-| |\   \-gndplane_position 
 | |              _______________     __________| | |   \_0 point
 | |             |    ___  ___   |___|  ______  | | |
 | |ifa_e  ifa_h |   |   ||   |_________|    |  | | |_ mifa_meander_edge_distance (minimum value)
 | |             |   |   ||  mifa_meander    |__| | |_ mifa_tipdistance (minimum value)
 | |             |   |   ||                   w2  | | |                  
 |_V_____________|___|___||_______________________| |_|
 | <---ifa_e---->| w1|   wf\                      | |
 |               |__fp___|  \                     | |
 |                       |    feed point          | |
 |                       |                        | | substrate_length
 |<- substrate_width/2 ->|                        | |
 |                                                | |
 |________________________________________________| |
  \________________________________________________\|

 Note: It's not checked whether your settings make sense, so check
       graphical output carefully.

The antenna generator makes an IFA antenna if ifa_l < substrate_length, if it is longer it will meander down to mifa_tipdistance, and if it is even longer than it will start to create meanders with a minimum distance of mifa_meander_edge_distance going back towards the feedpoint.

there arent any checks and balances, so please check the "extreme cases" if you use the optimization script 

The antenna generator also meshes the antenna elements and groundplane using the 2/3 1/3 rule, so each element will get a centerline and a box of size min_size going 1/3 the element and 1/3 outside it. A

If gndplane_position < 0, then the script will move the groundplane down the specified distance and place a via at the short ciruit stub

## installation
You need to follow the instructions on the [openEMS website](https://docs.openems.de/install/package.html#install-readymade-windows-package-src) to install the software, and then you can run the script by running the following command in the terminal:

I would reccomend unzipping to this location, then you install the CSXCAD and openEMS python packages using the following commands:
```bash
cd C:\opt\openEMS\python
pip install CSXCAD-0.6.2-cp310-cp310-win_amd64.whl
pip install openEMS-0.0.33-cp310-cp310-win_amd64.whl
```

You will need to make an .env file in the same directory as the script with the following parameters:
```bash
# openEMS ENV file
# ----------------
rootdir = 'C:/opt/openEMS'
```
