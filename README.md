<!DOCTYPE html>
<html>
<body>

<h2> 1.Installation</h2>
<h3>1.1 Add the repository to your project's build.gradle:</h3>
<p>
    
    allprojects {
    repositories {
         maven {   
             url = uri("https://maven.pkg.github.com/Thinkexamsdk/libPass")
              credentials {
                  username = "<username>"
                  password = "<token>"
              }
        }
  
}</p>

<h3>1.2 Add dependency to module's build.gradle:</h3>
<p>
    
    dependencies {implementation("com.ginger.te:sdk:0.0.1")} 
</p>

<h2> 2.Getting started</h2>
<h3> 2.1 Register your application </h3>
<p>Register your application by following the steps at Register your app with Thinkexam.com
</p>

<h3> 2.2.1 Create a ProctorSDK object </h3>
<p>
    Include the following permission in AndroidManifes.xml
    
    <uses-permission android:name="android.permission.ACTION_MANAGE_OVERLAY_PERMISSION" />      
</p>

  <h3> 2.2.2 Create a ProctorSDK object </h3>
  <p>
    <uses-permission android:name="android.permission.ACTION_MANAGE_OVERLAY_PERMISSION" />      
    ProctorSDK proctorSdk = new ProctorSDK();
</p>

<h3> 2.3 Setup Proctoring details </h3>
<p>           
             
    proctorSdk.registerBroadcast ( this );
    
    proctorSdk.setupClientConfiguration ( clientBaseURL, clientRequestUrl );

    proctorSdk.setupStudentDetails ( studentName , studentEmail, studentImageUrl );
    
    proctorSdk.setupTestDetails ( testName , testStartDate , testStartTime , testDuration, attemptCount);
    
    proctorSdk.setupStreamingDetails ( streamRecordingMode, streamingType, imageInterval, proctoringType, ufmType );
    
    proctorSdk.enableSettings(String aiEnable, String enableMic, String enableLocation, String enableRoomSanitisation, String enableUfmCount, String enableUfmMatrix, String enableSuspendOpt, String enableSecondaryCam, String unfairMeans, String enableFaceVerification, String enableAutoEventMessaging, String enableIdAuth, String showNetwork, String hideCameraView, String fldTerminateTestOnPopUp, String enableAsService, String allowAuthenticationAttempts) ;
    
    proctorSdk.enableUFMSettings ( fm, fnp, mfd, sfl, pr, vd, od, la );
</p>

<h3> 2.4 Start Validation Process </h3>
<p>
    
    proctorSdk.initializeProctorInfo ( this );
</p>

<h3> 2.5 Implement and set ProctorInfo Result Listener (ProctoringInfoListener) </h3>
<p>
    
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

    @Override
    public void onTestExit(String message) {
        Toast.makeText(this, message, Toast.LENGTH_LONG).show();
    }

    @Override
    public void onUfmTerminate(String message) {
        Toast.makeText(this, message, Toast.LENGTH_LONG).show();
    }
</p>
<h2> 3.Start Proctoring</h2>
<h3> 3.1 Use the following method if you are in the same activity/fragment </h3>
<p> 
        
    proctorSdk.startProctoring ( this, rootView,resultProctoringInfo);
</p>
<h3> 3.2 Use the following method if you are in a different activity/fragment, delegate ResultProctoringInfo received earlier. </h3>
<p>         
    
    ProctorSDK proctorSdk = new ProctorSDK ();
    
    proctorSdk.registerBroadcast ( this );
    
    proctorSdk.setupClientConfiguration ( clientBaseURL, clientRequestUrl );

    proctorSdk.setupTestDetails ( testName , testStartDate , testStartTime , testDuration);
    
    proctorSdk.startProctoring ( this, rootView,resultProctoringInfo);

    proctorSDK.setTestSubmitListener(this);
    
    proctorSDK.setProctoringInfoListener(this);
</p>
<h3> 3.3 Use lifecycle methods </h3>
<p> 
    
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
</p>

<h3> 3.4 At last Submit the test </h3>
<p>
    
    proctorSdk.submitTest()
</p>

</body>
</html>
