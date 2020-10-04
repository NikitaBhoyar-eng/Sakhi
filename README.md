# Sakhi
--Sakhi is a mobile based application which is connected to the security-band using wi-fi or Bluetooth. During the start of any journey you have to set a pre-destined route that you will take to reach the destination. The app is connected to the band which requires a sim and is also equipped with various inbuilt sensor with other features including tracker and audio recorder. In case of any deviation from the route the GPS tracker gets triggered and asks if you have willingly changed your route. If the answer is yes, it will ask you to set the new route. Else, it will automatically activate the camera and audio recording , which will then be forwarded to concerned people and authorities.

# Getting Started
-- The project "Sakhi" basically aims to make a Night patrolling Device. Looking at the current situation of crime against women we believe this will be an on-demand app.
The deployed solution given by us for the issue is an App with a Security-Band. This is a GPS and sensor-based Security-Band in collaboration with external application which vouches for safety of women.

Workflow of App: 

Workflow of Security-Band: 
 
# Necessities
-- Smartphone
   Active Internet Connection 

# Installing and App details                 


# Code for Security-Band
--Main Units
Intel Edison Module
Arduino expansion board for Edison

--IDE used for programming is Intel XDK IoT edition

# Code for Displaying Time and Temperature
var lcd = new jsUpmI2cLcd.Jhd1313m1(6, 0x3E, 0x62);

var groveSensor = require('jsupm_grove');

var today = setInterval(function ()
    {
    var d = new Date();
    var b= d.toTimeString();
    lcd.setColor(0, 255, 0);

// Go to the 2nd row, 6th character (0-indexed)

    lcd.setCursor(0,0);
    lcd.write(b);
     var celsius = temp.value();
        var fahrenheit = celsius * 9.0/5.0 + 32.0;
        var t = Math.round(fahrenheit);
        lcd.setCursor(1, 1);
        lcd.write(t+" *F");
       v.saveValue(t);
}, 1000);

# Code for Sending SMS
var twilio = require('twilio');

var TWILIO_ACCOUNT_SID = '' ;

var TWILIO_AUTH_TOKEN = '';

var OUTGOING_NUMBER = '';

var TWILIO_NUMBER = '';

var client = new twilio.RestClient(TWILIO_ACCOUNT_SID, TWILIO_AUTH_TOKEN);


client.sms.messages.create({

    to:OUTGOING_NUMBER,

    from:TWILIO_NUMBER,

    body:'Hi, sending from my Edison SmartWatch'

}, function(error, message) {



    if (!error) {



        console.log('Success! The SID for this SMS message is:');

        console.log(message.sid);


        console.log('Message sent on:');

        console.log(message.dateCreated);

    } else {

        console.log('error: ' + error.message);

    }

});

# Code for Accelerometer and Gyroscope
var accelrCompassSensor = require('jsupm_lsm303');

// Instantiate LSM303 compass on I2C

var myAccelrCompass = new accelrCompassSensor.LSM303(0);

var successFail, coords, outputStr, accel;

var myInterval = setInterval(function()

{

        // Load coordinates into LSM303 object

        successFail = myAccelrCompass.getCoordinates();



        coords = myAccelrCompass.getRawCoorData();


    // Print out the X, Y, and Z coordinate data using two different methods

        outputStr = "coor: rX " + coords.getitem(0)

                                      + " - rY " + coords.getitem(1)

                                      + " - rZ " + coords.getitem(2);

        console.log(outputStr);

        outputStr = "coor: gX " + myAccelrCompass.getCoorX()

                               + " - gY " + myAccelrCompass.getCoorY()

                               + " - gZ " + myAccelrCompass.getCoorZ();

        console.log(outputStr);


    // Get and print out the heading

        console.log("heading: " + myAccelrCompass.getHeading());


    // Get the acceleration

        myAccelrCompass.getAcceleration();

        accel = myAccelrCompass.getRawAccelData();

        outputStr = "acc: rX " + accel.getitem(0)

                               + " - rY " + accel.getitem(1)

                               + " - Z " + accel.getitem(2);

        console.log(outputStr);

        outputStr = "acc: gX " + myAccelrCompass.getAccelX()

                               + " - gY " + myAccelrCompass.getAccelY()

                               + " - gZ " + myAccelrCompass.getAccelZ();

        console.log(outputStr);

        console.log(" ");

}, 1000);



process.on('SIGINT', function()

{

        clearInterval(myInterval);

        myAccelrCompass = null;

        accelrCompassSensor.cleanUp();

        accelrCompassSensor = null;

        console.log("Exiting");

        process.exit(0);

});
# Sending data to Cloud
var ubidots = require('ubidots');

var client = ubidots.createClient('YOUR-API-KEY');


client.auth(function () {

  this.getDatasources(function (err, data) {

    console.log(data.results);

  });

  var ds = this.getDatasource('xxxxxxxx');


  ds.getVariables(function (err, data) {

    console.log(data.results);

  });

  ds.getDetails(function (err, details) {

   console.log(details);

});


  var v = this.getVariable('xxxxxxx');


  v.getDetails(function (err, details) {

    console.log(details);

  });

  v.getValues(function (err, data) {

    console.log(data.results);

  });




# Built with
-- Pandasuite - the most interactive no code platform (for apps)
   

# Team - Gen Z Techies
-- Group Leader  : Nikita Bhoyar
   Team Member 1 : Suchita Mitra
   Team Member 2 : Smrutishikha Das
   Team Member 3 : Shreyashree Dasgupta
   

# Acknowledgements
www.codeproject.com
