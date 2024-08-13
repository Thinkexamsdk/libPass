1. **Installation**

1.1 Add the repository to your project's build.gradle:

allprojects {
    repositories {
         maven {   
             url = uri("https://maven.pkg.github.com/Thinkexamsdk/libPass")
              credentials {
                  username = "<username>"
                  password = "<token>"
              }
        }
  
}


1.2 Add dependency to module's build.gradle:

dependencies {
    //Ginger proctor sdk
    implementation("com.ginger.te:tesdk:0.0.1")
}

2. **Getting started**

2.1 Register your application
Register your application by following the steps at Register your app with Thinkexam.com

2.2 Create a ProctorSDK object
ProtorSDK proctorSdk = new ProctorSDK();

2.3 Setup Proctoring details -
            proctorSdk.registerBroadcast ( this );
            proctorSdk.setupClientConfiguration ( "https://vikrant.thinkexam.com" , "vikrant.thinkexam.com" );
            proctorSdk.setupStudentDetails ( studentDataPojo.getSTUDENT_NAME () , "tarun1245663@gamil.com" , "https://dn2d9bgg1d2qf.cloudfront.net/studentTestLiveImages/535/13/32956902/1/13_1714634403903.png" );
            proctorSdk.setupTestDetails ( "Test Tarun 10Jun2024" , "10-06-2024" , "" , "100" );
            proctorSdk.setupStreamingDetails ( "1" , "0" , "5000" , "0" , "1" );
            proctorSdk.enableSettings ( "1" , "1" , "1" , "0" , "1" , "1" , "1" , "1" , "1" , "1" , "1" );
            proctorSdk.enableUFMSettings ( "1" , "1" , "1" , "1" , "1" , "1" , "1" );
2.4 Start Validation Process
            proctorSdk.initializeProctorInfo ( this );
2.5 Implement and set ProctorInfo Result Listener (ProctoringInfoListener)-
            proctorSdk.setProctoringInfoListener ( this );
            
             
    @Override
    public void onProctoringInfoSuccess(ResultProctoringInfo resultProctoringInfo) {
        if (resultProctoringInfo != null){
            //Start Proctoring
          
        }

    }

    @Override
    public void onProctoringInfoFailure(String errorMessage) {
        Toast.makeText(this, errorMessage, Toast.LENGTH_LONG).show();
    }

3. **Start Proctoring**
3.1 Use the following method if you are in the same activity/fragment
   
3.2 Use the following method if you are in the same activity/fragment
        proctorSdk.startProctoring ( this, testMainLayout,resultProctoringInfo);
3.3 Use the following method if you are in a different activity/fragment, delegate ResultProctoringInfo received earlier.
        ProctorSDK proctorSdk = new ProctorSDK ();
        proctorSdk.setupClientConfiguration("https://vikrant.thinkexam.com", "vikrant.thinkexam.com");
        proctorSdk.setupTestDetails("Test Tarun 10Jun2024", "10-06-2024", "", "100");
        proctorSdk.startProctoring ( this, parentLayout,resultProctoringInfo);

3.4 Use lifecycle methods

 @Override
  public void onResume() {
        super.onResume();
         proctorSdk.resumeProctoring ();
        }
        
  @Override
  public void onPause() {
        super.onPause();
         proctorSdk.pauseProctoring ();
        }

  @Override
  public void onDestroy() {
        super.onDestroy();
         proctorSdk.closeProctoring ();
        }
        
3.5 At last Submit the test
  proctorSdk.submitTest()
    

            
